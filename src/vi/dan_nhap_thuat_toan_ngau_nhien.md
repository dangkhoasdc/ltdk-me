---
layout: "post.njk"
title: "Dẫn nhập thuật toán ngẫu nhiên"
date: 2016-10-23
tags:
    - vi
    - algorithms
---

Hôm rồi học course _Introduction to Algorithm (2006-MIT)_ mình được biết qua khái niệm _Randomized Algorithms_, dành một buổi tìm hiểu về họ thuật toán thú vị này vậy.

# Định nghĩa

_Randomized Algorithms_ (viết gọn là `randalgs`) là những thuật toán mà trong các bước xử lý có sử dụng số ngẫu nhiên để quyết định cho các bước tính toán tiếp theo.

Điểm thú vị của `randalgs` chính là nó không quan tâm đến trường hợp xấu nhất mà chỉ quan tâm đến _kì vọng trong trường hợp xấu nhất_.

Tưởng tượng ta có một hệ thống nghiêm trọng, nếu như hệ thống đó bị crash thì sẽ kích hoạt [Cheget](https://en.wikipedia.org/wiki/Cheget) và [Nuclear football](https://en.wikipedia.org/wiki/Nuclear_football) cùng một lúc. Hệ thống quá lớn và phức tạp, quan trọng hơn, nó sẽ không hoạt động được khi liên tục phải chạy `quicksort` trong $\mathcal{O}(n^2)$ - dữ liệu đầu vào là mảng được sắp xếp sẵn.

Hacker, bằng một cách nào đó biết được điều này và tấn công hệ thống bằng cách đưa vào hệ thống những mảng đã sắp xếp sẵn. Và bùm, apocalyptic diễn ra.

Và để ngăn chặn thảm hoạ đó xảy đến, ta tạo ra một phiên bản gọi là `randomized quicksort`: trước khi được xử lý, mảng đầu vào sẽ được xáo trộn. Và cho dù hacker có cố tình tấn công bằng chuỗi đã sắp xếp thì sau bước tiền xử lý này , mảng được sắp xếp ngẫu nhiên.

Nếu một input có trật tự ngẫu nhiên, sau khi xáo trộn trở thành một chuỗi thứ tự thì sao? [Murphy’s law](https://en.wikipedia.org/wiki/Murphy%27s_law)

> Nếu đã xui, thì hẳn phải xui nhất có thể.

# Ví dụ

Một biến thế nổi tiếng của _Quick sort_ chính là _Randomized Quicksort_, có hai phiên bản chính:

1. Chọn ngẫu nhiên pivot để xử lý.
2. Xáo trộn mảng đầu vào trước khi sắp xếp.

_Randomized Quicksort_ được tạo ra nhằm tránh trường hợp xấu nhất của thuật toán _quicksort_ là $\mathcal{O}(n^2)$.

# Phân loại

> In Las Vegas, the dealer can tell you whether you’ve won or lost, but in Monte Carlo, le croupier ne parle que Français, so you have no idea what he’s saying

## Las Vegas algorithm

Thuật toán nằm trong họ _Las Vegas_ _luôn luôn_ đảm bảo kết quả trả ra đúng với mong muốn. Quicksort là một ví dụ điển hình.

Nói cách khác, _Las Vegas_ không chơi hên xui ở kết quả trả về, nó chỉ sử dụng yếu tố ngẫu nhiên trong các phép tính toán để cho ra kết quả đúng.

## Monte Carlo algorithm

Khác với _Las Vegas_, _Monte Carlo_ không đảm bảo kết quả sẽ luôn luôn đúng. Nhưng _Monto Carlo_ có xác suất kết quả sai thấp có thể.

Thay vì sử dụng xác suất như một trong những quá trình tính toán, _Monte Carlo_ hên xui ngay cả kể quả trả về.

## Phân biệt

### Bài toán

Cho một chuỗi có độ dài `2n` trong đó có `n` kí tự `a` và `n` kí tự `b`. Nhiệm vụ là tìm ra một vị trí bất kì trong chuỗi chứa kí tự a

```python
    import sys
    import random

    # Las Vegas version
    def find_a_lv(string):
        while True:
            pos = random.randint(0, len(string)-1)
            if string[pos] == 'a': return pos

    # Monte Carlo version
    def find_a_mc(string, k):
        pos = 0
        while k and string[pos] != 'a':
            k = k -1
            pos = random.randint(0, len(string)-1)

        return pos

    if __name__ == '__main__':
        string = sys.argv[1]
        if len(string) % 2 == 1:
            raise ValueError("Wrong input")

        print find_a_lv(string)
        print find_a_mc(string, len(string)/2)
```

Ta dễ dàng nhận thấy `find_a_lv` luôn luôn cho ra kết quả, tuy nhiên đôi khi nó lại không thực sự hiệu quả. Ví dụ như nếu ta có chuỗi đầu vào là “ab” và `find_a_lv` mất 2 triệu vòng lặp mới pick đúng `pos=0`.Dĩ nhiên xác suất để xảy ra chuyện đó rất thấp, nhưng không có nghĩa là nó không xảy ra.

Còn trong trường hợp `find_a_mc`, kết quả sẽ sai với xác suất khá dễ tính: $\frac{1}{2^k}$ - khi trong `k` lần thử để chọn đúng vị trí chứa `b`.

# Các kĩ thuật cơ bản

![Methodologies](http://i.imgur.com/0YSlgjJ.png)

1. Avoiding adversarial inputs:
    * Trong các thuật toán online.
    * Hashing.
    * Trong các thuật toán sắp xếp.
2. Verification:
    * Phát sinh số ngẫu nhiên trong các bài toán kiểm thực.
3. Random sampling:
    * Trong các bài toán tìm kiếm (tìm median..)
    * Trong các thuật toán geometry.
4. Load balancing:
    * Parallel algorithms.
    * Hashing problems.
5. Symmetry breaking:
    * Dùng trong hệ thống distributed.
6. Probabilistic existence proofs:
    * Thông qua các thực nghiệm.
    * Đảm bảo trong bài toán tìm kiếm đối tượng cần tìm tồn tại.

# Tài liệu

## Khoá học

1. [Randomized Algorithms and Probabilistic Analysis - Washington](https://courses.cs.washington.edu/courses/cse525/13sp/)
2. [Probabilistic Methods in Computer Science](http://cs.brown.edu/courses/cs155/slides/slides.html)
