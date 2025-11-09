---
layout: "post.njk"
title: "Cài đặt quan hệ thứ tự trong C++"
date: 2018-01-03
tags:
    - vi
    - cpp
---

Bài viết dưới đây mô tả một giải pháp để cài đặt các quan hệ giữa các cấu trúc
dữ liệu (CTDL) khác nhau trong C++. Ứng dụng của quan hệ giữa các đối tượng đóng vai
trò quan trọng trong các thuật toán, dưới đây có thể nêu lên 1 số ví dụ:

- Total Order (Quan hệ thứ tự): Đây là một trong những quan hệ quen thuộc nhất,
có vai trò quan trọng trong các thuật toán sắp xếp.
- Equivalence relation (Quan hệ tương đương): được sử dụng trong các thuật toán
hashing.

Tuy nhiên trong bài này thay vì đề cập trực tiếp đến quan hệ thứ tự (Total Order),
ta thử sử dụng quan hệ tổng quát hơn chút **weak order**. Điều khác biệt duy nhất
của Weak Order so với Total Order nằm ở chỗ weak order không có tính đối xứng.
Và trong "thực tế đời sống", Weak Order chính là dấu `<`.

Vậy có điều gì khó khăn khi phải cài đặt dấu `<` này? Giả sử ta có một hàm như
sau:

```cpp
template<typename T> bool f(const T& lhs, const T& rhs) { return lsh<rhs; }
```

Giả sử ta viết một thư viện trong đó chứa hàm `f` và mong muốn bất kì ai sử
dụng cũng phải cài đặt dấu `<` cho CTDL của mình. Bởi đôi khi, dấu `<` mặc
định của C++ chưa chắc mang ngữ nghĩa đúng, hay bất kì một CTDL tự tạo nào
không chứa dấu `<` cũng gặp lỗi. Vậy nếu có cơ chế nào giúp trình biên dịch
phát hiện được LTV quên cài đặt dấu này. Cụ thể hơn ta, muốn có:

```cpp
template<typename T>
bool f(const T& lhs, const T& rhs) {
    // Error if T does not have `<` operator
    // otherwise
    return lsh<rhs;
}
```

Trong C++11, ta có 1 cơ chế khá giống như vậy:

```cpp
template<typename T>
bool f(const T& lhs, const T& rhs) {
    static_assert(has_less_operator<T>::value, "Please implement < operator");
    return lsh<rhs;
}
```

Kỹ thuật sử dụng `struct<T>::value` được gọi là [type traits](https://accu.org/index.php/journals/442),
được sử dụng rất
phổ biến trong STL, metaprogramming, các thư viện như BOOST, dlib. Tiếp, `::value`
ở đây phải là static, không có gì phải bàn. Đồng thời, `::value` trả về yes/no
khi lớp T chứa/ hoặc không chứa `<`, nên kiểu phải là `bool`. Do giá trị này được
kiểm tra lúc trình biên
dịch thực thi, nên hẳn là `constexpr`. Xong tạm thời ta có 1 cài đặt:

```cpp
template<typename T>
class has_less_operator{
    private:
        // stuff
    public:
        static constexpr bool value = // and other stuff;
};
```

Và giờ đến phần khoai nhất khi cài đặt. Ta buộc phải gán "cái gì đó" vào `value`,
nhưng ngay tại thời điểm cài đặt ta còn không biết nó có giá trị gì, và hoàn toàn
phụ thuật vào CTDL `T` nào đó do LTV khác viết. Hay nói một cách khác, chính giá
trị boolean cũng bị tham số hóa theo kiểu. May mắn thay, STL có hỗ trợ vụ này:

```cpp
#include <type_traits>

using namespace std;

typedef true_type yes;
typedef false_type no;
```

Lúc này ta có thể viết :

```cpp
static constexpr bool value = is_same<yes, /* X */>::value;
```

Như vậy `value` sẽ phụ thuộc vào `is_same<yes, X>::value`. Vấn đề X ở đây là gì?
Ta xem trong STL, `is_same` nhận 2 datatype làm input. Vậy X chính là 1 datatype
khác. Nhưng cụ thể hơn nó có thể là yes/no để `value` trở thành yes/no.

Tới đây là một đoạn cực kì fancy, nhưng mình không biết giải thích trước thế nào
nhưng trước hết cứ viết ra đã:

```cpp
static constexpr bool value = is_same<yes,
                                    decltype(test<T>(nullptr))
                                    >::value;
```

`decltype` trả về kiểu dữ liệu `return type` của hàm `test` và ta cố tình đưa
toàn bộ cài đặt vào trong `test` này. Bởi toán tử `<` trong C++ yêu cầu 1 tham
số đầu vào nên ta để 1 tham số hàm `test` làm dummy. Như vậy ta biết chắc chắn
`test<T>` trả về 1 trong 2 kiểu dữ liệu : `yes` hoặc `no` như được typedef phía
trên. Đồng thời, ta biết rằng mặc định mọi kiểu dữ liệu `T` sẽ trả về `no`.

Tức ta có :

```cpp
template<typename> static no test(...);
```

Xong cho phần sai. Giờ làm thế nào để trả về `yes` khi dữ liệu thực sự đã cài
đặt `<`. Ta có 1 hàm test thứ 2:

```cpp
template<typename P> static auto test (P *p)
    -> decltype(declval<T>()<(*p), yes());
```

WTF =))) Điều gì đang xảy ra ở đây? Nhờ một khái niệm [SFINAE](https://en.wikipedia.org/wiki/Substitution_failure_is_not_an_error),
chúng ta được chứng kiến sự điên rồ của C++.

Hãy phân tích câu lệnh trên.
Phần `template<typename T> static` không có gì khác với `test` của `no`. Kết
quả trả về là `auto` để "nhường" phần quyết định cho `decltype`. `decltype` làm
chuyện như sau, nếu biểu thức `declval<T>()<(*p), yes()` biên dịch được thì
`auto` sẽ trở thành `yes` nhờ vào "comma-separated list": trả về kết quả của term
cuối cùng trong list. Vậy vấn đề nằm ở `declval`. Hàm nào giúp ta gọi được
`<` mà không cần thông qua constructor. Chính xác hơn `declval<T>()` là
template function với tham số kiểu dữ liệu `T`, trả về kiểu reference X nào đó,
nhờ đó ta gọi được `<(*p)`: chính là phép `<` thần thánh của chúng ta. Nếu như
không tồn tại `<`, biểu thức này fail nhưng sẽ không bị báo lỗi biên dịch mà thay
vào đó trình biên dịch gán `test` cho `static no test(...)`.

Tổng kết lại ta có code như sau:

```cpp

#include <iostream>
#include <type_traits>

using namespace std;
typedef std::true_type yes;
typedef std::false_type no;

template<typename T>
class has_less_operator {
    private:
    template<typename P> static auto test(P *p) -> decltype(std::declval<P>()<(*p), yes());
    template<typename> static no test(...);


    public:
    static constexpr bool value = is_same<
                                    yes,
                                    decltype(test<T>(nullptr))
                               >::value;
};

template<typename T>
bool f(const T& lsh, const T& rhs) {
    static_assert(has_less_operator<T>::value, "Please implement <");
    return lsh<rhs;
}

struct s1 {
    int i;
    s1(int _i): i(_i) {  }
    inline bool operator<(const s1& other) const {
        return i < other.i;
    }
};

struct s2 {
    int i;
    s2(int _i): i(_i) {  }
};

int main(int argc, char const* argv[])
{
    s1 a(10);
    s1 b(20);
    f(a, b);
    /* s2 c(10), d(20); */
    /* f(c, d); */
    return 0;
}

```

Nếu ta uncomment s2 và f bên dưới, ta có thông báo lỗi như sau:

```
a.cpp: In instantiation of ‘bool f(const T&, const T&) [with T = s2]’:
a.cpp:47:11:   required from here
a.cpp:24:5: error: static assertion failed: Please implement <
     static_assert(has_less_operator<T>::value, "Please implement <");
     ^~~~~~~~~~~~~
```

Thông báo cực kì dễ hiểu. Với việc sử dụng một số IDE thông minh, thậm chí thông
báo lỗi sẽ được thông báo ngay lúc cài đặt `s2` và gọi `f`. Quan trọng hơn,
nhờ đó ta có thể viết mã theo "Design by Contract" hay theo phong cách interface
của Java và C++. Sắp tới C++ sẽ giới thiệu khái niệm `concept` và theo tác
giả của C++ là sẽ giải quyết vấn đề suốt 35 năm qua của Generic Programming
([link](https://developers.slashdot.org/story/17/01/23/003247/c-creator-wants-to-solve-35-year-old-generic-programming-issues-with-concepts)).

# Các toán tử khác

Sau khi cài đặt toán tử `<`, thông thường ta sẽ có nhu cầu cài đặt các toán
tử so sánh khác như `>`, `<=`, `>=`. May mắn thay ta có thể quy đổi các toán tử
này dễ dàng thông qua `<`:

- `>`: chính là `rhs<lsh`.
- `<=`: là `!(rhs<lsh)`.
- `>=`: `!(lhs<rhs)`.

Trong thâm ta ta có cảm giác rằng thể nào cũng có rất nhiều CTDL ta cài đặt
kiểu này: chỉ cần định nghĩa `<` và 3 toán tử còn lại tự nội suy. Nhờ vào kỹ
thuật [Curiously recurring template pattern](https://en.wikipedia.org/wiki/Curiously_recurring_template_pattern),
ta có một code khá gọn:

```cpp
template<typename T>
struct order {
    virtual bool operator<( const T& rhs) const = 0;
    bool operator>( const T& rhs) const
        {return rhs<static_cast<const T&>(*this);}
    bool operator>=( const T& rhs) const
        {return !((*this)<rhs); }
    bool operator<=( const T& rhs) const
        {return !(rhs< static_cast<const T&>(*this));}
};
```

Như vậy chỉ cần kế thừa `order` và cài đặt `<`, ta sẽ có luôn 3 toán tử còn lại.
Điều duy nhất mình ức chê là phải sử dụng `static_cast`.
