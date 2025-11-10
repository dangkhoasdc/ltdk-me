---
layout: "post.njk"
title: "Sách: Selected Papers on Computer Science"
date: 2018-01-15
tags:
    - vi
    - books
---

Một chút thông tin về cuốn sách trước khi mình đánh giá:

| Thông tin | Mô tả                                    |
| --------- | ---------------------------------------- |
| Tiêu đề   | Selected Papers on Computer Science [[Amazon](https://www.amazon.com/Selected-Papers-Computer-Science-Lecture/dp/1881526917)] |
| Tác giả   | Donald Knuth                             |
| Số trang  | 276                                      |

Đây là một trong những cuốn sách dễ tiếp cận nhất của Don Knuth. Tuy được xuất
bản cách đây khá lâu (gần 20 năm về trước), nhưng đây là một trong những cuốn
sách kinh điển dẫn nhập về KHMT. Trên trang Amazon có [bình luận khá
hay](https://www.amazon.com/gp/customer-reviews/R2BNAZLQDF5NI8/ref=cm_cr_arp_d_rvw_ttl?ie=UTF8&ASIN=1881526917)
của Peter Norvig (giám đốc nghiên cứu của Google). Một trong những vấn đề được
thảo luận nhiều trong sách chính là sự ra đời bộ môn KHMT ở giai đoạn khi ngành
nghiên cứu còn khá mới mẻ. Thông qua các chương sách, ta có thể thấy thời đó
các bậc tiền bối đã đấu tranh rất nhiều để KHMT có thể được công nhận là một
môn "khoa học" chính thống và tách biệt với toán học.

Điều này khiến mình liên hệ với Deep Learning hiện giờ, dễ có khi vài năm sau,
với sự bùng nổ và phát triển của hướng nghiên cứu này, Deep Learning sẽ trở
thành một ngành riêng biệt và không còn nhập nhằng với KHMT. Nếu như khi xưa
KHMT "tách ra" khỏi Toán học, thì biết đâu 5, 6 năm nữa, Deep Learning sẽ
"tách" ra khỏi KHMT.

Một số chương đặc biệt thú vị, có thể kể đến như:

- Chapter 0: cái nhìn toàn cảnh nhất về KHMT.
- Chapter 1: Computer Science and its Relation to Mathematics: sự khác nhau giữa
toán học hiện đại và KHMT. Đồng thời tác giả cũng đề cập đến phân tích bài toán
kinh điển: hashing.
- Chapter 2 và Chapter 3: cái nhìn toàn cảnh về các thuật toán, cũng như cách
tác giả tiếp cận để giải các vấn đề. Dù được xuất bản lần đầu 1976, 1977 có thể
trong giai đoạn đó khá là mới, nhưng theo mình những bài toán này (đường đi
ngắn nhất, tìm kiếm, tối ưu rời rạc) trở thành chủ đề kinh điển trong KHMT hiện
nay.
- Chapter 6-9: Theory and Practice: tinh hoa của cả cuốn sách, vừa mang yếu tố
lịch sử, xoay quanh những thảo luận sôi nổi về 2 khía cạnh quan trọng nhất
của KHMT.
- Chapter 11-13: Lịch sử KHMT: từ KHMT cổ điển (những thuật toán được sử dụng
vào thời kì rất xa xưa), đến KHMT hiện đại khi John von Neumann phân tích
về thuật toán merge sort.

Mình dành phần chi tiết nội dung cho bạn nào tìm đọc sách. Mình nghĩ ở Việt Nam
thì cuốn này tương đối khó kiếm, nhưng những chương rời rạc có thể tìm được
ở trang Publications của Don Knuth. Dưới đây mình thảo luận về chủ đề xoay quanh
cuốn sách.

# Toán học và KHMT

Khi đọc cuốn sách này, người đọc sẽ cảm nhận được giai đoạn 1950-1975 có lẽ
là thời kì bùng nổ của KHMT (có lẽ rất giống Deep Learning hiện giờ). Vào thời
điểm đó giống như giai đoạn "mông muội" của KHMT vậy, các trường ĐH danh tiếng
không dám mở 1 khoa riêng mang tên KHMT, thiên hạ vẫn tranh nhau gọi ngành mới
này nên là KHMT, CNTT hay "Xử lý thông tin"... Thời điểm mà những thuật toán
dân tình nghĩ là giải $\mathcal{O}(N^2)$ lại hóa ra giải được trong $\mathcal{O}(N\lg N)$,
thời kì mà KHMT vẫn chưa có một công cụ chính xác nào về mặt toán học để phân
tích các kỹ thuật được sử dụng. Và KHMT và những người có tâm đã đấu tranh
rất nhiều để có thể phát triển hướng nghiên cứu này, từ việc xin phép mở khoa
trong trường, đến việc phổ biến chương trình cho sinh viên, đến việc xây dựng
nền móng lý thuyết (từ những nghiên cứu của Turing, John von Neunman) và
nền móng phân tích (Don Knuth, Sedgewick, Ullman, ...).

Có điểm gì với Deep Learning hiện nay? rất giống là đằng khác, Deep Learning
được so sánh như [giả kim học](https://www.amazon.com/Selected-Papers-Computer-Science-Lecture/dp/1881526917)
vì thiếu sự chính xác và một "công cụ phân tích toán học". Tuy nhiên nếu theo
đúng những gì đang diễn ra, và ta loại đi những gì quá hype của media, thì ta
cũng rất nên hi vọng Deep Learning sẽ trở thành 1 ngành nghiên cứu và thoát
khỏi cái gọi là "giả kim học" như hiện nay. Mình tưởng tượng, hẳn là trong thời
kì 50-60 năm trước, hẳn cũng có ai đó đăng đàn và nói rằng KHMT không có cơ
sở chính xác toán học. Chỉ là trong giai đoạn ấy, truyền thông và mạng xã hội
không phổ biến như hiện nay và rốt cuộc bị xem như là cuộc cãi nhau giữa những
giáo sư trong trường ĐH.

Toán học gắn liền mật thiết với KHMT, nhưng vào thời điểm này, Toán học "hiện
đại" đã đi khá xa so với những gì kiến thức phổ thông cung cấp. Tuy nhiên, tác
giả đã trình bày sự khác nhau trong tiếp cận vấn đề, dẫn đến KHMT xứng đáng
có 1 chỗ đứng riêng ra khỏi toán học. Đồng thời, qua chapter 2, ta cũng thấy
được KHMT đã góp phần nào phát triển rất nhiều hướng trong Toán học.

# Lịch sử KHMT

Mình đặc biệt hứng thú với những phân tích chi tiết về các thuật toán cổ đại
của tác giả, cũng như cái nhìn cụ thể về những bản thảo merge sort mà John
von Neunman để lại. Đây mới thực sự là cách ta tìm hiểu về lịch sử KHMT. Không
phải là nhớ ngày tháng nào ai đó phát minh ra cái gì mà động lực nào, trong
hoàn cảnh nào mà tác giả có thể tạo ra thuật toán đó, đồng thời đánh giá với
những hạn chế kỹ thuật, ràng buộc công nghệ thời bấy giờ.

Thông qua những phân tích đó, ta mới có thể trân trọng sự đóng góp của tác giả,
cũng như có góp nhặt được cách tiếp cận, phương pháp khi giải quyết vấn đề,
theo mình đó là điều mà KHMT nên được nhớ theo lịch sử, và những điều đó
sẽ trường tồn, cho dù sau này máy tính lượng tử có thay thế hoàn toàn các mô hình
tính toán tuần tự.

Don Knuth rất quan tâm đến điều này, thể hiện ra qua một số bài viết và talk:

- [Let's Not Dumb Down the History of Computer Science](https://www.youtube.com/watch?v=gAXdDEQveKw):
rất đáng để bỏ ra 55 phút để nghe. GS phát biểu mở đầu chính là [bố già của thung lũng Sillicon](https://en.wikipedia.org/wiki/John_L._Hennessy). Mình rất thích 1 comment trong clip này: "Discover how discoveries are discovered".
- Lịch sử các thuật toán về sinh các mẫu [[fasc4b](http://www.cs.utsa.edu/~wagner/knuth/fasc4b.pdf)]:
tác giả tìm hiểu các thuật toán có từ thời cổ đại, trung đại và hiện đại với những
thông tin cực kì thú vị.
- Lịch sử về chu trình Hamilton [[fasc8a](http://www-cs-faculty.stanford.edu/~knuth/fasc8a.ps.gz)].
