---
layout: "post.njk"
title: "Tìm kiếm theo chuỗi Fibonacci"
date: 2017-12-19
tags:
    - vi
    - algorithms
---
# Tìm kiếm theo chuỗi Fibonacci

Mình không tìm được từ nào tiếng Việt có thể dịch được từ "Fibonaccian Searching",
nếu "binary searching" có thể dịch là "tìm kiếm nhị phân", thì "Fibonaccian Searching"
không có ngữ nghĩa gì nhiều.

Nguồn gốc thuật toán này xuất phát từ bài tập 1.4.22 (Algorithms, Fourth Edition, Sedgewick). Ngoài
ra đây cũng là một nội dung được đề cập trong TAoCP - Vol 3.

# Lịch sử

Thuật toán được để xuất bởi Devid E. Ferguson (CACM-1960, [link](https://dl.acm.org/citation.cfm?id=367496)).
Một số phát hiện liên quan, chủ yếu về nguồn gốc cây Fibonacci có thể tham khảo tại TAoCP - Vol 3 (Mục 6.2.1).

# Thuật toán

Điểm thú vị của thuật toán này nằm ở chỗ thuật toán không sử dụng phép chia, nhưng vẫn đạt được
độ hiệu quả của binary search. Tuy nhiên, ưu điểm này thực sự có tác dụng
vào thời điểm thuật toán này được đề xuất (1960) khi mà các chép chia, hay
shift bit tốn nhiều chi phí hơn so với phép cộng trừ. Tuy nhiên, `fibsearch`
còn được sử dụng khi tốn ưu thời gian tìm kiếm khi mà dữ liệu quá lớn không
thể đọc lên được toàn bộ lên RAM hoặc cache, khi đó thời gian đọc trên bộ
lưu trữ ngoại vi trở nên tốn kém (()[]). Tuy nhiên mình khá `fibsearch`
sẽ là một câu hỏi phỏng vấn cực kì thú vị.

> Thiết kế một thuật toán tìm kiếm nhị phân không sử dụng phép chia hoặc
> dịch bit với độ phức tạp $\mathcal{O}(\lg N)$

### Cài đặt

Phần dưới đây là giải thuật lấy từ TAoCP, mình nghĩ là cực kì dễ hiểu, tạm thời
mình chỉ trình bày mã giả. Có thể tham khảo phần cài đặt bằng C, trong phần
[References](#references). Một phiên bản cải tiến với kích thức mảng $N$ bất
kì sẽ được update sau.

```
Input: mảng $K_0, K_2, ..., K_(N-1)$ được sắp xếp và phần tử $X$ cần tìm. Giả sử
$N = F_{N+1}$

P1. [Khởi tạo] i = F[k], p = F[k-1], q = F[k-2]
P2. [So sánh].
        If K[i] < K: go to P3.
        else if K[i] > K: go to P4.
        else: return i;
P3. [Xét cây con Fibonacci bên trái]
    if q = 0 : return -1
    else: i -= q
          (p, q) = (q, p-q)
          go to P2
P4. [Xét cây con Fibonacci bên phải]
    if p = 1: return -1
    else:
        i += q
        p -= q
        q -= p
        go to P2
```

## Bài tập

- Thiết kế thuật toán cho trường hợp $N \leq 0$.

# Phân tích

Phần dưới đây là mô tả ngắn gọn cách mà thuật toán này thực thi. Khác với tìm
kiếm nhị phân chia các nhánh tìm kiếm thành các cây nhị phân, `fibsearch` thay
vào đó xây dựng cây Fibonacci. chính xác hơn là với $N = F_k$, nhánh con bên
trái sẽ là $F_{k-1}$ và nhánh phải sẽ là $F_{k-2}$. Trường hợp $N \neq F_k$
có hơi "tricky" một chút nhưng cũng khá dễ giải quyết và không ảnh hưởng
đến tính đúng đắn của thuật toán.

Một chứng minh cụ thể và chi tiết hơn sẽ được cập nhật sau, kèm theo đó là mã
nguồn C++ của thuật toán.

# References

- [C implementation](http://users.ics.forth.gr/~lourakis/fibsrch/)
- TAoCP.
- Algorithms - Sedgewick, phần [web exercises](https://algs4.cs.princeton.edu/14analysis/)
có đề cập solution.-
