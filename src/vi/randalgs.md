---
layout: "post.njk"
title: "Các ví dụ về thuật toán ngẫu nhiên"
date: 2016-07-10
tags:
    - vi
    - algorithms
---

# Các ví dụ về thuật toán ngẫu nhiên

Tiếp tục series về thuật toán ngẫu nhiên, trong bài viết này mình ghi lại 3 ví dụ điển hình trong họ bài toán này. Tất cả các ví dụ đều nằm trong cuốn sách [Randomized Algorithms](https://www.amazon.com/Randomized-Algorithms-Rajeev-Motwani/dp/0521474655)

# Randomized Quicksort

Thuật toán quicksort có lẽ là một trong những thuật toán khá dễ hiểu khi tìm hiểu về các thuật toán ngẫu nhiên. Thử tưởng tượng ta cho quicksort thông thường chạy 10 lần với dữ liệu đã sắp xếp với randomized-quicksort cũng với cấu hình như vậy, ta sẽ thấy sự khác biệt lớn.

## Thuật toán

<script src="https://gist.github.com/dangkhoasdc/e7ad5caa46b7bad12ae4f5ff221d707d.js"></script>

## Chứng minh

Cho dữ liệu đầu vào gồm $n$ phần tử khác nhau. Gọi $S_i, 1 \leq i \leq n$ là phần tử *rank i* (phần tử nhỏ thứ *i*) trong mảng, đồng thời ta có $X_{ij}$ biến ngẫu nhiên bằng $1$ nếu xuất hiện phép so sánh của 2 phần tử $S_i$ và $S_j$ trong quá trình thực thi, bằng không nếu không xuất hiện phép so sánh nào.

Như vậy, độ phức tạp của `randomized-quicksort` được tính thông qua quá trình sắp xếp mảng theo pivot mà chi phí chính nằm ở phép so sánh các phần tử, tổng chi phí chính là $\sum_{i=1}^n \sum_{j>i} X_{ij}$.

Tuy nhiên, điều ta quan tâm hơn ở đây là *kì vọng* chi phí trong các lần thực thi:

$$ E \left [ \sum_{i=1}^n \sum_{j>i} X_{ij} \right ] = \sum_{i=1}^n \sum_{j>i} E[X_{ij}] $$

Công thức trên được xây dựng dựa vào một tính chất của kì vọng: [tính tuyến tính của kì vọng](https://brilliant.org/wiki/linearity-of-expectation/). Như vậy kì vọng của tổng các chi phí so sánh chính bằng tổng của từng kì vọng của biến ngẫu nhiên $X_{ij}$. Gọi $p_{ij}$ là xác suất để $X_{ij}=1$. Ta có:

$$
E[X_{ij}] = p_{ij} * 1 + (1-p) * 0 = p_{ij}
$$

$$
E \left [ \sum_{i=1}^n \sum_{j>i} X_{ij} \right ] = \sum_{i=1}^n \sum_{j>i} p_{ij}
$$

Bài toán được qui về việc tính xác suất khi nào phép so sánh giữa hai phần tử $S_i$ và $S_j$ xuất hiện.

Nếu ta xem quá trình thực thi của `randomized-quicksort` là quá trình xây dựng cây nhị phân: với mỗi node chính là 1 pivot tại thời điểm gọi hàm `partition`, kết quả hàm `partition` ta có được 2 cây con bên trái và phải của node pivot dùng để so sánh. Nếu $S_i$ và $S_j$ nằm ở hai nhánh con trái-phải thì phép so sánh giữa hai phần tử này chắc chắn không xảy ra. Như vậy $S_i$ và $S_j$ có quan hệ cha con - một trong hai phần tử phải thuộc node cấp lớn hơn của node kia. Một giả thuyết khác cần xem xét đó là xác suất các số được chọn làm pivot phải bằng nhau (uniform distribution) - có được giả thuyết này ta mới tính được độ phức tạp trong thời gian trung bình được.

Như vậy, để $X_{ij}=1$ khi và chỉ khi một trong hay vị trí $S_i$ hoặc $S_j$ được chọn, và đó là $p_{ij} = \frac{2}{j - i + 1} $ (Xác suất này được tính khi loại đi xác suất chọn phải những pivot nằm bên trái của $S_i$ hoặc nằm bên phải của $S_j$)

Như vậy ta có:

$$
E \left [ \sum_{i=1}^n \sum_{j>i} X_{ij} \right ] =  \sum_{i=1}^n \sum_{j>i} \frac{2}{j - i + 1}
$$

Đặt $k = j - i + 1$, ta được:

$$
\sum_{i=1}^n \sum_{j>i} p_{ij} \leq \sum_{i=1}^n \sum_{k=1}^{n-i+1} \frac{1}{k}
$$

$$
\leq 2 \sum_{i=1}^n \sum_{k=1}^{n} \frac{1}{k}
$$

$$
= 2n \sum_{k=1}^{n} \frac{1}{k}
$$

$\sum_{k=1}^{n} \frac{1}{k}$ chính là [chuỗi harmony](https://en.wikipedia.org/wiki/Harmonic_series_(mathematics)#Rate_of_divergence) và tổng này sẽ hội tụ về xấp xỉ của $ln(n)$. Và như vậy

$$
E \left [ \sum_{i=1}^n \sum_{j>i} X_{ij} \right ] \leq 2n\log n
$$

# Random Mincut

## Ví dụ

Giả sử ta có dữ liệu facebook của đám bạn cấp 3 và đang tò mò xem trong chục năm qua, những đứa bạn đó có lập thành nhóm chơi thân nào không. Dữ liệu đầu vào là danh sách các bạn trong lớp cấp 3 và mối quan hệ từng người với nhau (quan hệ bạn cấp 3, bạn đại học, đồng nghiệp, quan hệ nam nữ, vợ chồng).

Giả sử ta tạo một đồ thị với đỉnh là một người trong lớp, `a` có thể nối với `b` thông qua các cạnh nối:

- Bạn cấp 3 (cái này chắc chắn)
- Bạn đại học
- Đồng nghiệp

Việc tìm ra nhóm bạn *thân* - tức gắn bó với nhau sau thời gian cấp 3 chính là việc tìm cách tách đồ thị lớn này thành những đồ thị con.

Những bài toán *chia cắt* đồ thị gọi là *graph cut*, nếu trong bài toán yêu cầu tìm ra đoạn cắt nào có chi phí thấp nhất: cắt ít số cạnh nhất - thì đó chính là bài toán tìm *mincut*.

Trong ví dụ này ta xét đồ thị là một [multigraph](http://mathworld.wolfram.com/Multigraph.html) - tức đồ thị có thể có nhiều cạnh cùng nối chung hai điểm. Một số định nghĩa cho phép *multigraph* là đồ thị có các cạnh lặp (self-loop). Để thuận tiện cho việc chứng minh và minh hoạ, các đồ thị được đề cập trong bài là các đồ thị vô hướng.

## [Karger Mincut](https://en.wikipedia.org/wiki/Karger%27s_algorithm)

![Minh hoạ thuật toán Karger](https://upload.wikimedia.org/wikipedia/commons/e/e7/Single_run_of_Karger%E2%80%99s_Mincut_algorithm.svg)

Một quá trình quan trọng trong thuật toán Karger là *Edge Contraction* - gộp cạnh. Cho một cạnh $ e = \{u, v\}$, sau phép gộp cạnh ta sẽ có được một *đỉnh* mới là $uv$ trong đó tất cả các cạnh nối từ $u$ đến $v$ hay ngược lại đều bị loại bỏ, đồng thời các cạnh lặp (self-loop) cũng bị xoá bỏ.

Với các cạnh khác $ e' = \{u, w\}$ hay $e'=\{v, w\}$ đều trở thành $e'=\{uv,w\}$.

Một cách đơn giản: phép gộp cạnh sẽ nhập 2 đỉnh lại với nhau - xoá toàn bộ các cạnh nối 2 cạnh cũ và giữ lại những cạnh nối 2 đỉnh đó với các đỉnh khác trong đồ thị.

Thuật toán được mô tả như sau:

1. Chọn ngẫu nhiên (theo phân phối đều) một cạnh trong đồ thị.
2. Thực hiện phép gộp cạnh vừa chọn.
3. Lặp lại bước (1) cho đến khi số đỉnh trong đồ thị còn lại 2.
4. Output: min-cut là các cạnh còn lại trong đồ thị

## Tính đúng đắn của giải thuật

Để có thể tính được độ phức tạp trong thời gian trung bình, ta cần quay lại một chút về các tính chất của đồ thị. Cho đa đồ thị (multigraph) $G=(V, E)$ gồm các đỉnh $V$ và các cạnh $E$. Gọi $d(v)$ là bậc của đỉnh $v$ là tổng số các cạnh liên thuộc với $v$. Ta có tính chất sau:

$$
\sum_{v \in V} d(v) = 2 | E |
$$

Gọi $C$ là lát cắt có kích thước nhỏ nhất $k$ - tức số lượng các cạnh trong lát cắt đó là $k$. Do đó, bậc tối thiểu của mỗi cạnh trong đồ thị này là $k$. Bởi nếu tồn tại một đỉnh có bậc nhỏ hơn $k$ thì lát cắt $k$ không phải là lát cắt nhỏ nhất.

Như vậy ta có:

$$
nk \leq \sum_{v \in V} d(v) = 2 | E |
$$

$$
|E| \geq \frac{nk}{2}
$$

Ta thấy xác suất để thuật toán gộp cạnh chọn đúng ngay 1 cạnh trong C chính là

$$
\frac{k}{|E|}
$$

kết hợp với bất đẳng thức phía trên, ta được:

$$
\frac{k}{|E|} \leq \frac{2k}{nk} = \frac{2}{n}
$$

Như vậy, xác suất để thuật toán gộp cạnh không chọn phải các cạnh của $C$ là $p_n $.

Ta có $p_n \leq (1-\frac{2}{n})p_{n-1} $ .

Đồng thời ta cũng có $ p_2 = 1 $ lí do là bởi Karger chỉ chọn cạnh để gộp khi $ \vert V \vert > 2 $

Nên khi $ n=2 $ thì biến cố chọn phải cạnh để gộp nằm trong $ C $ chắc chắn không xảy ra.

Xác suất $p_n$ có cận như sau:

$$
p_n \geq \prod_{i=0}^{n-3} \left (1 - \frac{2}{n-i} \right ) = \frac{2}{n(n-1)}
$$

Để dễ tưởng tượng hơn, ta có thể phân tích một chút về trường hợp Karger không tìm ra được mincut, rõ ràng xác suất đó chính là $ 1 - \frac{2}{n(n-1)}$, để tăng độ chính xác, ta có thể cho Karger chạy $k$ lần. Lúc này, xác suất Karger không tìm ra được mincut là: $ \left (1 - \frac{2}{n(n-1)} \right )^k$. Có một bất đẳng thức thú vị ở đây:

$$
\frac{1}{4} \leq \left (1 - \frac{1}{x} \right )^ x \leq \frac{1}{e}
$$

Giả sử $k = \frac{n(n-1)}{2}\ln n$ ta có được kết quả khá đẹp như sau:

$$
\left (1 - \frac{2}{n(n-1)} \right )^{\frac{n(n-1)}{2}\ln n} \leq \left (\frac{1}{e} \right )^{\frac{n(n-1)}{2}\ln n} = \left (\frac{1}{e} \right ) ^{\ln n} = \frac{1}{n}
$$

# Binary Planar Partitions

## Giới thiệu

![Một ví dụ về cây BSP](http://i.imgur.com/cGwRyxq.png)

Binary Planar Partitions (trong trường hợp tổng quát là *Binary Space Partitions*) là một phương pháp phổ biến được sử dụng nhằm chia cắt không gian thành các tập lồi (convex set) chứa các siêu phẳng - hyperplane. Sự chia cắt này tạo nên một cấu trúc dữ liệu được gọi là cây BSP.

BSP có nhiều ứng dụng, đặc biệt là trong các bài toán về đồ hoạ. Điển hình như trong bài toán dựng hình (xác định đối tượng nào được dựng trong khung hình từ góc một góc nhìn nào đó), trong hệ thống CAD, phát hiện va chạm trong robotics, cũng như trong các bài toán chứa các cấu trúc không gian phức tạp.

Trong trường hợp tổng quát, cây BSP, từ mỗi node của mình sẽ chia không gian thành hai nửa siêu phẳng, từ mỗi nửa siêu phẳng đó sẽ tiếp tục được chia cắt thành các nửa siêu phẳng nhỏ hơn sao cho những node lá cuối cùng sẽ chứa 1 đối tượng mà thuộc không gian. Có thể thấy cây BSP là trường hợp tổng quát của cây [k-d](https://en.wikipedia.org/wiki/K-d_tree), và [Quadtree](https://en.wikipedia.org/wiki/Quadtree).

## Ví dụ

Để đơn giản bài toán ta xét trường hợp mặt phẳng với dữ liệu đầu vào là tập các đoạn thẳng sao cho từng cặp trong tập không giao nhau $S=\{s_1, s_2, \dots, s_n\}$, output của bài toán là một cây BSP mà mỗi vùng trong mỗi node lá chỉ chứa 1 một đoạn thẳng.

1. Chọn ngẫu nhiên (theo phân phối đều) một hoán vị $\pi$ trong tập hoán vị của $\{1, 2, \dots, n \}$ (gồm $n!$ phần tử).
2. Tồn tại một vùng chứa nhiều hơn 1 đoạn thẳng:
   2.a Cắt vùng này bởi *đường thẳng* $l(s_i)$ trong đó $i$ là phần tử đầu tiên trong hoán vị (ở đây đường thẳng $l$ sẽ chứa $s_i$) $\pi$ sao cho $s_i$ cắt vùng đang xét.

## Phân tích

Gọi biến $X_{ij}$ là biến ngẫu nhiên và $X_{ij}=1$ khi đường thẳng chứa $s_i$ cắt $s_j$ trong một vòng gọi đệ quy nào đó, $X_{ij}=0$ trong trường hợp ngược lại.

Ở đây ta muốn xét xem kì vọng số lần thuật toán này cắt phải một đoạn thẳng trong tập đầu vào $S$.

$$
\mathbf{E} (X) = \mathbf{E} \left [ \sum_{i=1}^{n} \sum_{i=1}^{n} X _ {ij} \right ]
$$

$$
=  \sum_{i=1}^{n} \sum_{i=1}^{n} \mathbf{E} [X _ {ij} ]
$$

$$
=  \sum_{i=1}^{n} \sum_{i=1}^{n} Pr [X _ {ij} = 1 ]
$$

Bài toán được quy về việc tính xác suất $Pr[X_{ij}=1]$. Gọi $t$ là giao điểm của $s_i$ và $s_j$, $index(i,j)=t$ nếu $s_i$ cắt $t-1$ đoạn thẳng trước khi giao với $s_j$, như ví dụ bên dưới $s_{ij}=4$. Trường hợp hai đoạn thẳng không cắt nhau thì $S_{ij}=\infty$.

![Ví dụ về giá trị index(i, j)](http://i.imgur.com/kyaZ5CL.png)

Bởi đường thẳng chứa $s_i$ bất kì có thể tiến vô cùng về hai phía nên tồn tại hai đoạn sao cho $index(s_i, s_j) = index(s_i, s_k)$. Nếu $index(s_i, s_j)=t$ ta gọi $s_{i1}, s_{i2}, \dots, s_{it}$ là những đoạn thẳng mà $s_i$ sẽ cắt trước khi giao với $s_j$, xác suất để sự kiện này xảy ra là $\frac{1}{t+1}$

Cho một đoạn $s_k$ cố định và $m \in \{0, 1, 2, dots, n-2 \}$ tồn tại tối đa hai đoạn thẳng $s_l$ sao cho $index(s_l, s_k)=m$

Cận trên được tính như sau:

$$
\mathbf{E}[X] = \sum_{i=1}^{n} \sum_{j=1}^{n} Pr [X _ {ij} = 1 ]
$$

$$
\leq \sum_{i=1}^{n} \sum_{j=1}^{n} \frac{1}{index(i, j) + 1}
$$

$$
\sum_{i=1}^{n} \sum_{k=2}^{n} \frac{2}{k}
$$

$$
= 2n \ln n
$$

# Tài liệu tham khảo

1. [Introduction to Randomized Algorithms](http://www.csee.wvu.edu/~ksmani/courses/fa01/random/lecnotes/lecture2.pdf)
2. [Randomised Algorithms](http://cs.au.dk/~gudmund/Documents/randompearlnotes.pdf)

>[!note]
> migrate từ một bài viết cũ năm 2016, nhờ Deepseek chuyển sang markdown nên khả năng cao sẽ có hallucations.
