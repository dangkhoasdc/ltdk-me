---
layout: "post.njk"
title: "Một số biến thể Quicksort"
date: 2018-01-04
tags:
    - vi
    - algorithms
---

Trước tiên là ôn lại một chút về quicksort. Dưới đây là bản implement (đơn giản) của thuật toán nổi tiếng này:

```cpp
// quicksort implement
template<typename T>
int partition(vector<T>& a, int lo, int hi) {
    int i = lo, j = hi;
    T v = a[lo];
    while (true) {
        while (a[++i]<=v) if (i == hi) break;
        while (v<=a[--j]) if (j == lo) break;
        if (i >= j)  break;
        swap(a[i], a[j]);
    }
    swap(a[lo], a[j]);
    return j;
}

template<typename T>
void quicksort(vector<T>& a, int lo, int hi) {
    if (lo >= hi-1) return;
    int j = partition(a, lo, hi);

    quicksort(a, lo, j);
    quicksort(a, j+1, hi);
}
```

### Phân tích

Độ phức tạp được đánh giá thông qua hàm:

$$ C(N) = n-1 + {1\over n}\sum_{i=0}^{n-1} ( C(i) + C(n-i-1)) $$

Trong phần `partition` thực hiện $n-1$ phép so sánh, sau đó gọi 2 lần quicksort với kích thước lần lượt là $i$ và $n-i-1$, xác suất cho mỗi phần tử trong mảng theo phân phối đều là ${1\over n}$ vậy nên ta được biểu thức như trên.

Cách giải được đề cập chi tiết trong các sách như Introduction to Algorithms, Concrete Mathematics, Introduction to Analysis of Algorithms. Sơ qua cách giải:

1. Nhân hai vế cho $n$.
2. Viết biểu thức cho $n-1$.
3. Tính $C(n) - C(n-1)$ ta được 1 quan hệ đệ quy tuyến tính, giải một chút sẽ ra.

## Hạn chế trường hợp worst-case

Một trong những phương pháp chống worst-case nổi tiếng của quicksort là xáo trộn mảng input trước khi dùng quicksort. Dùng [Knuth shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle) với độ phức tạp $\mathcal{O}(N)$ ta có thể đảm bảo hiệu quả của thuật toán. Ngoài ra, việc xáo trộn mảng input khiến cải tiến này, thường được gọi với cái tên randomized quicksort, trở thành ví dự kinh điển trong việc phân tích các thuật toán ngẫu nhiên. Mình có một [bài viết](http://dkhoa.me/post/randalgs_ex/) đề cập tới phân tích randomized quicksort.

Ngoài cách xáo trộn mảng ra, còn có một số cách tiếp cận khác:

* Thay vì chọn pivot ở đầu hoặc cuối dãy, chọn giá trị median.
* Một trường hợp worst-case khác là khi tất cả các giá trị giống nhau, lúc nay ta dùng 3way-quicksort để giải quyết.

## Khử đệ quy với mảng nhỏ

Đây là 1 chiêu có thể dùng được với mọi thuật toán sử dụng chia để trị: khi vòng đề quy đủ nhỏ khiến cho mảng input của hàm đó nhỏ hơn 1 ngưỡng cho phép (10-15 phần tử), sử dụng `insertion sort` sẽ cải thiện hiệu năng đáng kể. Chỉ cần thêm vào trong hàm quicksort

```cpp
///...
if (hi-lo < CUTOFF) {
 insertion_sort(a, lo, hi);
 return;
}
///...
```

## Khử phép so sánh giá trị 2 đầu dãy

Với phiên bản được implement bên trên, ta có thể bỏ đi câu lệnh `if` trong  `while` như sau:

* Ta có thể bỏ `if` khi kiểm tra `j` bởi a[lo] &lt; a[lo] không bao giờ xảy ra.
* Để bỏ `if` trong `i`. Trước khi gọi quicksort, ta đặt 1 giá trị cờ là `MAX_INT` chẳng hạn. Như vậy luôn đảm bảo tồn tại 1 giá trị lớn hơn a[lo].

## Median-of-three và median-of-five

Thủ thuật khá kinh điển để tránh worst-case: sample 3 hay 5 phần tử, lấy giá trị median và lấy median đó làm pivot.

### Tukey ninther quicksort

Dùng 9 phần tử thay cho 3/5 phần tử.

## 3way Quicksort

Đây là thuật toán nổi tiếng do Dijkstra đề xuất cùng với [Dutch flag problem](https://en.wikipedia.org/wiki/Dutch_national_flag_problem). Dùng để tránh trường hợp có quá nhiều giá trị trùng nhau trong dãy. Điểm thú vị là phiên bản quicksort này được chính mình là tối ưu về mặt entropy. Một chứng minh sơ lược có được đề cập trong Algorithms, R. Sedgewick.

Nếu có ai đó hỏi vì sao trong post này nhắc đến Sedgewick nhiều quá vậy, thì đơn giản là luận văn tiến sĩ của ông có tiêu đề: "[Quicksort](http://searchworks.stanford.edu/view/870273)".

Một phiên bản khá ảo diệu của Jon Bentley (tác giả Programming Pearls, cộng tác với Sedgewick để chứng minh phiên bản tối ưu entropy của quicksort):

```c
void quicksort(int l, int u){
    int i, m;
    if(l >= u) return;
    m = l;
    for(i = l+1; i<= u; i++)
        if(x[i] < x[l])
            swap(++m, i); //this is where I'm lost. Why the heck does it preincrement?

    swap(l, m);

    quicksort(l, m-1);
    quicksort(m+1, u);
}
```

## Phiên bản khử đệ quy

Cũng là một cải tiến được đề xuất bởi Sedgewick khi dùng stack thay cho gọi recursive. Một phiên bản cài đặt bằng C cực kì chi tiết được mô tả [đây](http://www.cs.columbia.edu/~hgs/teaching/isp/hw/qsort.c).  Trong phiên bản này gồm có các cải tiến được đề cập phía trên:

* CUTOFF
* Median-of-three
* Khử đệ quy đồng thời optimize kích thước stack.

Phiên bản này cũng chính là phiên bản `qsort` trong GNU C.

Phiên bản Java của Sedgewick cũng rất đáng để tìm hiểu: [source code QuickX](https://algs4.cs.princeton.edu/23quicksort/QuickX.java.html).

## Samplesort

Đây là một bản chế lại của quicksort để chạy được trong các thuật toán song song. Tư tưởng ở đây là sử dụng quicksort để tìm các pivot cho từng process. Rồi sau đó chạy quicksort trên từng pivot được phân phối đó. [Bài viết này](http://parallelcomp.uw.hu/ch09lev1sec5.html) mô tả cụ thể và phân tích độ phức tạp của thuật toán.

# Tham khảo

1. Cormen, Thomas H. Introduction to algorithms. MIT press, 2009.
2. Graham, Ronald L., et al. "Concrete mathematics: a foundation for computer science." Computers in Physics 3.5 (1989): 106-107.
3. Sedgewick, Robert, and Philippe Flajolet. An introduction to the analysis of algorithms. Pearson Education India, 1996.
4. Sedgewick, Robert, and Kevin Wayne. Algorithms. Addison-Wesley Professional, 2011.
5. Bentley, Jon. Programming pearls. ACM, 1986.
