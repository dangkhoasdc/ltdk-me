---
layout: "post.njk"
title: "Bioshock: Elizabeth hay học tăng cường"
date: 2018-05-01
tags:
    - vi
    - video games
---

Trong một ngày rảnh rỗi giữa hai đợt deadlines và trong cái không khí ảm đạm do mùa mưa sắp tới của Singapore, tôi đã quyết định ngồi chơi cái game mà hồi nhỏ mà không hiểu gì: Bioshock. Tuy nhiên lần này tôi lại chơi bản Bioshock Infinite. Để nói về game này, tôi không gọi đó là chơi game, đó là một trải nghiệm.

Với cốt truyện lôi cuốn cùng với những chủ đề lồng vào nhau nhuần nhuyễn, Bioshock Infinite mang đến người chơi một thành phố Columbia steampunk với bề ngoài hào nhoáng, sung túc, và hạnh phúc. Nhưng đằng sau đó là sự phân biệt chủ tộc, chủ nghĩa da trắng cực đoan, chủ nghĩa cộng sản và một xã hội bị thao tóm bởi sự cai trị tập trung lẫn về chính trị lẫn tôn giáo. Chưa dừng lại ở đó, Bioshock Infinite còn kết hợp với yếu tố khoa học viễn tưởng như vật lý lượng tử, du hành đa vũ trụ và du hành thời gian. Điều tạo nên Bioshock đặc biệt, mặc dù mang trong miình rất nhiều chủ đề khác nhau, là cùng với rất nhiều cao trào, thắt nút, lẫn những vấn đề xã hội phức tạp, các nhà làm game vẫn cho ra được một cốt truyện mạch lạc và đầy hấp dẫn. Nếu bạn yêu thích những bộ phim xoắn não như Memento, Inception, Donnie Darko, Mr.Nobody và đặc biệt là Predestination, thì Bioshock là một trải nghiệm hoàn toàn xứng đáng.

![Imgur](https://i.imgur.com/b9vucB7.png)

Tôi từng nhận định rằng, game không chỉ là phương tiện giải trí, mà đó còn là phương tiện nghệ thuật. Nếu ta theo dõi các nhà đạo diễn game như Hideo Kojima, Ken Levine, ta sẽ cảm nhận rõ ràng cảm hứng nghệ thuật, chủ đề lẫn cách tiếp cận người chơi để mang đến một câu chuyện lôi cuốn. Với cách nhìn nhận này, video game trở thành bước tiến của điện ảnh truyền thống. Đó chính xác là điều mà Hideo Kojima đã tạo ra với bộ Metal Gear. Và đồng thời, ta cũng thấy một xu hướng gần đây rằng rất nhiều game có sự tham gia của các đạo diễn, biên kịch nổi tiếng từ Hollywood.

Nhưng trái tim của cả Bioshock Infinite là Elizabeth, là cách xây dựng trí tuệ nhân tạo (AI) lồng vào trong một cốt truyện, là cách mà developer tạo ra sự tương tác giữa AI và người chơi và cách AI tương tác với môi trường. AI, đó cũng chính là một trong những yếu tố phân biệt video game với các loại hình nghệ thuật khác. Chỉ cần Irrational Games tạo ra 1 Elizabeth với 1 tương tác AI ngượng ngùng, và cứng ngắt, họ đơn giản là phá hỏng toàn bộ công sức với game của mình.

![Imgur](https://i.imgur.com/CoCQUwJ.png)

Tôi đánh giá rất cao AI của nhân vật trong Bioshock Infinite hơn hẳn những game có cốt truyện hấp dẫn tương đương. Ví dụ là Witcher, mặc dù Witcher có cốt truyện lôi cuốn, nhưng tương tác giữa người chơi và các nhân vật chính khá đơn điệu, tất cả bị đơn giản hóa thành các đoạn đối thoại. Trong khi đó nhân vật Elizabeth không chỉ đồng hành cùng người chơi, mà còn tạo ra các chiến lược hoàn toàn khác nhau, đồng thời hỗ trợ người chơi trong quá trình combat. Nhưng thực ra, ta không thể trách các game thế giới mở có tương tác AI nghèo nàn, vì có quá nhiều tác nhân [agent] mà AI cần phải tương tác, và developer không thể if else cho từng trường hợp.
Đó là lúc ta cần reinforcement learning =]] LOL. Nghiêm túc nào,

Học tăng cường là gì?, Theo wiki tiếng Việt, ta có:

> "là một lĩnh vực con của học máy, nghiên cứu cách thức một agent trong một môi trường nên chọn thực hiện các hành động nào để cực đại hóa một khoản reward nào đó về lâu dài. Các thuật toán học tăng cường cố gắng tìm một chiến lược ánh xạ các trạng thái của thế giới tới các hành động mà agent nên chọn trong các trạng thái đó."

Vâng chính xác đó là điều ta cần làm để có thể có AI tốt trong game thế giới mở. Mỗi AI cho học 1 thuật toán reinforcement learning để có thể tương tác tốt hơn với môi trường.

Thực ra mấy đoạn xàm kia để cho khớp với cái tiêu đề đầy tính clickbait.
Hết câu chuyện về reinforcement learning.

Ta quay trở lại với vấn đề làm thế nào để tạo sự liên kết giữa AI và người chơi lẫn môi trường. Một cách để giải quyết đó là định nghĩa các primitive elements trong game, và cho NPC tương tác thông qua yếu tố đó thay vì trực tiếp với từng agent trong game. Thay vì cho NPC tương tác trực tiếp với đơn vị X trong game, ta cho NPC tương tác khi NPC thấy có nổ súng, thấy có cháy, hoặc các yếu tố liên quan.
[Dĩ nhiên, ta có thể làm chiều ngược lại, apply các kĩ thuật phát triển AI trong gaming sang machine learing, ví dụ như kỹ thuật Goal Oriented Action Planning hay Behaviour Trees chẳng hạn. Dù sau, những giới hạn AI trong game về data, tính toán xử lý nghiêm ngặt hơn nhiều trong machine learning]

Video của Mark Brown giải thích rõ về các tương tác AI trong game, và nếu xem kỹ, thì đó cũng chính là các vấn đề trong reinforcement learning

www.youtube.com/watch?v=9bbhJi0NBkk

Nhưng còn một yếu tố còn quan trọng hơn, đó là tạo ra một AI với cốt truyện, có tính cách và có sự độc nhất. Nếu không có một cốt truyện, hay backstory liên kết với người chơi, cho dù AI có rất thông minh, thì người chơi cũng không đặt cảm xúc vào AI đó. Đó là lí do Elizabeth là một điển hình của AI xuất sắc. Cốt truyện được xây dựng để bạn càng ngày càng quan tâm đến hành trình của Elizabeth, đồng thời tìm hiểu mối quan hệ của cô với phần còn lại của câu chuyện.
Tính độc đáo tạo nên kí ức về AI cho người chơi. Elizabeth có một sức mạnh phi thường: du hành giữa các vũ trụ, điều khiển thời gian [giống Ciri phết =]] ] nhưng cô cũng vô cùng ngây thơ và đầy cảm xúc [vì bị nhốt trong tòa tháp gần 20 năm và không biết gì ngoài đọc sách và học cách mở khóa, và một ước mơ được đến Paris]. Thông qua đó ta thấy các yếu tố có mối quan hệ hữu cơ với nhau: một nhân vật độc đáo tạo nên kí ức với người chơi, một cốt truyện đi kèm tạo nên mối quan tâm về AI, và tương tác AI tốt tạo sự gắng bó với người chơi.  Thông qua các yếu tố trên người chơi lại càng ấn tượng với AI trong tựa game mình trải nghiệm.

Đó là điều tạo nên AI.
Game: 9/10. Điểm trừ ở mặt combat, mình phải config lại keyboard giống với Doom. Và đồng thời không có sự balance giữa các vũ khí.
Cốt truyện, nhân vật, graphics optimization: 10/10.
