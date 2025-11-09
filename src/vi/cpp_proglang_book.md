---
layout: "post.njk"
title: "Review: The C++ Programming Languages"
date: 2016-10-10
tags:
    - vi
    - cpp
    - books
---

![C++ Programming Language](http://www.stroustrup.com/4thEnglish.JPG)

Hồi năm 1 đại học, mình rất thích cuốn C Programming Language của K&C, dù cuốn sách khá là ít trang nhưng đầy tinh tuý và rất hấp dẫn. Đến tận bây giờ, khi đã tốt nghiệp ra trường, tức đã 4 năm được biết cuốn sách, đôi lúc mình vẫn muốn đọc lại. Một thời gian sau mình có đọc thêm một số sách có tựa: The XXX Programming Language nhưng chỉ thấy C++ là hay.

Bản C++ Programming Language mới nhất cập nhật cách tính năng của C++11, vì vậy, đây là một cuốn rất cần thiết cho bất kì ai muốn tìm hiểu về phiên bản C++11 cũng như các phiên bản tiếp sau như C++14, C++17\. Chính vì những tính năng hoàn toàn mới và những thay đổi kể từ C++03, bản cập nhật này thêm vào kha khá chương so với phiên bản 3 của cuốn sách.

# Nhìn chung

Điều mình không thích nhất là bản 4 _đã bỏ phần câu hỏi và bài tập_ ra khỏi cuốn sách - điểm mà ngày xưa mình rất thích. Một điều nữa là cuốn sách khá là dày, một số phần khá hay, một số phần giống sách reference về ngôn ngữ lập trình. Mà điều đó lại không cần thiết lắm vì nếu cần tra cứu thì [cppreference](http://en.cppreference.com/w/) hay [cplusplus](http://www.cplusplus.com/) lại gần gũi và chi tiết hơn.

# Part I: Introductory Material

Đây là phần rất hay của cuốn sách. Tác giả giúp người đọc hình dung được như thế nào là lập trình sử dụng ngôn ngữ C++. Vì sao điều này quan trọng? Theo như kinh nghiệm bản thân, rất nhiều người học lập trình bị lẫn lộn giữa C++ và C, và hơn thế nữa là sử dụng tư tưởng của Java hay C# khi lập trình C++. Thêm vào đó, phần I giới thiệu sơ lược về thư viện chuẩn - một thành phần rất quan trọng trong ngôn ngữ C++.

Từ các ví dụ tính toán thông thường đến các sử dụng các cấu trúc dữ liệu, thiết kế hàm hay module cũng như thiết kế hướng đối tượng, chương cuối của phần I còn đề cập phần mới đó là tính toán song song.

# Part II: Basic Facilities

Phần này đề cập đến các thành phần cơ bản trong ngôn ngữ C++. Cơ bản ở đây gồm có:

1. Các lệnh (lặp, điều kiện, …)
2. Hàm.
3. Cấu trúc mảng, con trỏ và reference.
4. Structure và các cấu trúc liên quan như Enumeration, Union.
5. Exception và namespace.

Các tính năng (1) và (2) có lẽ rất quen thuộc với những ai đã lập trình với các ngôn ngữ họ nhà C. Tuy nhiên, các tính năng (3), (4) và (5) lại khá quan trọng. Nằm vững phần này giúp việc tránh các lỗi rất ngỡ ngẩn vì nhầm lẫn khái niệm trong C++.

# Part III: Abstraction Mechnisms

Phần này cực kì quan trọng và có lẽ là phần mình thấy hay nhất trong cuốn sách bởi lẽ:

1. Tác giả đề cập đến lập trình hướng đối tượng và các kĩ thuật liên quan.
2. Tác giả nêu lên những vấn đề trong lập trình hướng đối tượng cũng như phát triển phần mềm. Tập trung vào phương pháp trong kiến trúc ngôn ngữ nhằm giúp lập trình viên giải quyết các vấn đề dễ dàng hơn.
3. Các kĩ thuật trong phát triển phần mềm khá hay và thực tế.

Tuy nhiên, điều làm mình không thích lắm có lẽ ngay ở các C++ giải quyết các vấn đề. Đặc biệt là ở template, và mình cảm thấy càng về sau càng rắm rối. Và điểm này C++ rõ ràng không “tốt” trong thiết kế hơn Java. Về mặt “hướng đối tượng” có lẽ Java đảm nhiệm tốt hơn hẳn.

# Part IV: the Standard Library

Phần “chán” nhất trong cuốn sách. Vì sao ư? Hầu như tác giả liệt kê toàn bộ các lớp, hàm, cũng như thiết kế trong thư viện chuẩn. Nếu đề cập một số thành phần quan trọng (container, algorithm hay string) thì không có gì đáng nói. Nhưng là toàn bộ thư viện chuẩn rất đồ sộ và việc đọc hết part này rất mệt, nó giống như đọc một cuốn từ điển vậy. Ưu điểm duy nhất mình thấy khi đọc phần này đó là phát hiện ra một số hàm mà mình không nghĩ là nó tồn tại (điển hình là convert từ string sang số và ngược lại). Chương mình nghĩ là quan trọng gồm:

1. Container.
2. Algorithms.
3. Threads and Tasks,
4. (Optional) Memory: mặc dù khá quan trọng, nhưng mình nghĩ dùng unique_ptr hay weak_ptr vẫn có gì đó không ổn.

# Tổng kết

Đây là cuốn sách rất đáng đọc cho bạn này đang học/làm việc hay quan tâm về ngôn ngữ C++. Như chính Bjarne Stroustrup từng nói: “Lập trình C đau thương như thể bắn vào bàn chân mình; nhưng C++ còn khó hơn; đó là lúc bạn bắn bay cả đôi chân của mình” [Nguồn](https://en.wikiquote.org/wiki/Bjarne_Stroustrup), để tránh bản thân “đau thương” đến vậy thì C++ Programming Language chính là cuốn sách hướng dẫn sử dụng súng. Ngoài ra, một số chương còn đề cập đến phương pháp cũng như quá trình hình thành ngôn ngữ và các tính năng trong ngôn ngữ, đó cũng là những kiến thức rất hay trong viết phần mềm. Nhưng đây không phải là cuốn sách để đọc ngấu nghiến từ trang đầu tới trang cuối cùng. Theo kinh nghiệm của bản thân, có thể đọc một số phần tuỳ thuộc vào việc người đọc đang làm việc với C++ ở mức độ nào:

1. Đang học lập trình: Part 1 và Part 2 rất quan trọng, đọc xong 2 part là ở mức khá khi hiểu về C++ rồi.
2. Đang học về lập trình hướng đối tượng: Part 3 buộc phải đọc, bỏ qua phần Template. Part 1 là optional nhưng khuyến khích đọc nếu trước đây bị lậm Java hay C# nhiều, Part 2 có thể không đọc.
3. Người làm về C++: Part 3 và Part 4\. Cho dù cppreference hay cplusplus có tiện đi chăng nữa thì trong sách này là văn bản chính thức và qui chuẩn về các hàm cũng như về thư viện STD.
4. Expert về C++: đổi sách khác đọc. Xét về khía cạnh expert thì mình nghĩ cuốn sách này hơi chung chung và chưa đi sâu vào các vấn đề trong lập trình C++.
