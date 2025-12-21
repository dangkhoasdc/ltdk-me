---
layout: "post.njk"
title: "Review Algorithms (Princeton) - Coursera"
date: 2016-08-08
tags:
    - review
    - courses
    - algorithms
    - vi
---

![Algorithms, Princeton](http://algs4.cs.princeton.edu/cover.png)

Đây là một trong những khoá rất đỉnh về lập trình, vì sao ư?

1. Kiến thức được dạy vững chắc và có nhiều thông tin rất thú vị và bổ ích.
2. Bài tập lập trình rất hay.
3. Bài tập trắc nghiệm giúp người học hiểu rõ hơn về các thuật toán và cấu trúc dữ liệu trong bài giảng.
4. Các câu hỏi phỏng vấn rất hay và sáng tạo.

Part 1 của khoá học cover các phần sau:

## Union-Find

Cấu trúc dữ liệu này rất hay. Một phần nó hay là vì hồi đại học mình chưa được học cấu trúc này, cộng thêm nó cũng có kha khá ứng dụng trong thực tế (phần Interview Questions có vài câu hỏi khá thực tế). Vì phần này ngoài cấu trúc dữ liệu nên bài tập và phần lập trình không quá xoắn não.

## Stacks and Queues

Phần bài tập lập trình làm về cấu trúc Deque và RandomizedQueue, khá là thú vị. Phần thuật toán có giới thiệu giải thuật [Graham scan](https://en.wikipedia.org/wiki/Graham_scan) - tìm tập bao lồi trong một tập các điểm. Phần này thì cũng không quá khó, thiên về lập trình và API là nhiều. Để được 100/100 điểm lập trình thì cần tricky một chút cho phần RandomizedQueue.

## Merge sort và Quicksort

Hai thuật toán sort rất nổi tiếng, đồng thời tác giả có đề cập cả stable sort và các vấn đề liên quan. Ví dụ như tìm k phần tử nhỏ nhất (có thuật toán nào có thể run tốt hơn O(nlogn) không). Vì sao quick sort lại tốt hơn merge sort dù 2 ẻm này đều là O(nlogn), vì sao ta phải shuffle dữ liệu trước khi thực hiện quick sort, merge sort được sử dụng trong các thuật toán cần stable sort. Đồng thời bài giảng cũng đề cập đến các thuật toán sort được cài đặt sẵn trong các ngôn ngữ lập trình.

Phần bài tập lập trình cũng hơi tricky, tui nhiên rất hay: đó là tìm những điểm collinear trong một mặt phẳng.

## Priority Queue và Symbol Table

Học về heap sort và các vấn đề liên quan. Bài tập lập trình [8-puzzle](https://en.wikipedia.org/wiki/15_puzzle), một bài rất hay.

## Balanced Search Trees

Cây và các vấn đề liên quan đây cây cân bằng, điểm mình thấy hay nhất đó là được học về 2-3 tree, cây đỏ đen, B-tree. Đặc biệt là B-tree sử dụng trong cơ sở dữ liệu và hệ điều hành. Một phần khá hay khác là thuật toán sử dụng trong không gian, điển hình là [kdtree](https://en.wikipedia.org/wiki/K-d_tree). Bài tập lập trình là kdtree, quá là phê luôn.

Bài tập trắc nghiệm trong phần này bao khó, vì phải chạy bằng tay cây đỏ đen.

## Hash Tables

Học về hashing function, các cấu trúc dữ liệu trong hashing, birthday problem … blah blah. Một trong những ứng dụng của nó chính là cấu trúc dành cho véc tơ, ma trận thưa ([sparce vector](https://en.wikipedia.org/wiki/Sparse_array)), nhờ khoá này mà khi dự một buổi meeting có liên quan đến Hashing thì mình không bị bỡ ngỡ bởi các khái niệm.

Khoá học còn một phần nữa là Part 2, đề cập đến các chủ đề như:

1. Đồ thị.
2. Cây.
3. Maximum Flow và Minimum Cut.
4. Regular Expression và Data Compression.
5. Reductions và Linear Programming.

## Tổng kết

Một khoá _bắt buộc_ phải học với những ai theo nghiệp lập trình. Một trong những điểm cộng sáng giá đó là khoá học này không giảm độ khó so với khoá gốc ở Princeton (Như khoá Machine Learning của Andrew Ng. trên Course thì quá dễ so với khoá của ông ở Stanford). Không những được học về những cấu trúc dữ liệu và giải thuật kinh điển mà còn được học, sử dụng vào các ứng dụng thực tiễn, các bài toán còn nóng hổi cũng nhưng các giải thuật nâng cao. Bài tập lập trình rất hay và sáng tạo, điểm cộng đó là cho người học tự do với sự sáng tạo cũng như cách ra đề giúp người học động não.

## Một số lưu ý

Thầy dạy rất dễ buồn ngủ, để tránh hiện tượng này ta có thể:

1. Tăng tốc độ video lên 1.25 hoặc 1.5, việc này giúp não tránh bị nhàm chán.
2. Viết note đầy đủ.
3. Pause video, viết một đoạn code minh hoạ thuật toán hoặc search wiki về các thông tin thầy đề cập.
4. Uống nước cho tinh thần thoải mái, tránh Red Bull và nước có ga.

Để theo hết được khoá học, thì đây là một số kinh nghiệm của bản thân:

1. Follow theo đúng deadline và lịch của khoá học. Tốt nhất là dành 2 ngày để nghe video, vì thường 1 tuần sẽ có 2 nội dung học. Một bài thường có thời lượng 60-70 phút, tốt nhất nên dành 2 tiếng trong ngày để nghe video, ghi chép và tìm hiểu. Dành khoảng 10 phút giải lao trong mỗi 45 phút học bài.
2. Dành một tuần cho bài tập lập trình và bài tập trắc nghiệm.
3. Dành một ngày trong tuần sau đó để ôn lại bài, làm lại bài tập hoặc nộp lại bài lập trình.
4. Thông thường khi bài lập trình rất khó để đạt 100/100 ngay từ lần submit đầu tiên, tuy nhiên để đạt trên 80 thì không khó. Cố gắng nắm bắt thật kĩ đề bài, thiết kế API và mã giả trước, được kĩ checklist cũng như hint được tiết lộ. Chịu khó Google về bài tập, thường chủ đề của bài tập là những bài toán/vấn đề nổi tiếng trong Khoa Học Máy Tính.
5. Tham gia diễn đàn, ta sẽ được an ủi phần nào khi có kha khá đứa cũng đang nổi điên với bài tập như mình.
6. Bài tập trắc nghiệm: đọc lại slides, với các bài tập thuật toán thì cần chạy chính xác từng lệnh trong thuật toán đó bằng tay. Các bài tập về mệnh đề rất mẹo, cần đọc kĩ câu hỏi và xem kĩ lại video.
