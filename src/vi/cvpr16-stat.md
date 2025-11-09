---
layout: "post.njk"
title: "Một chút thống kê về các bài báo CVPR16"
date: 2016-10-23
tags:
    - vi
    - research
---

Hôm nay tình cờ thấy cái link liệt kê [các bài được accept ở CVPR16](http://www.cv-foundation.org/openaccess/CVPR2016.py), thế là mình ngồi thống kê vài cái cho vui

Đầu tiên là parse đống html này, sau đó dùng python load một dữ liệu lên, ta có được:

1. Số bài báo được accept: 643 bài.
2. Người có nhiều bài được đăng nhất: Ming-Hsuan Yang với tổng cộng 11 bài.
3. Bài có chữ _deep_ trong tiêu đề: 87 bài, chiếm 13.53% tổng số bài được accept.
4. Bài có số tác giả nhiều nhất: _Multimodal Spontaneous Emotion Corpus for Human Behavior Analysis_ với 13 tác giả đứng tên.
5. Bài chỉ có 1 tác giả (một mình chống mafia):

    * [Structured Feature Similarity With Explicit Feature Map](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Kobayashi_Structured_Feature_Similarity_CVPR_2016_paper.pdf)
    * [Hierarchically Gated Deep Networks for Semantic Segmentation](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Qi_Hierarchically_Gated_Deep_CVPR_2016_paper.pdf)
    * [Robust, Real-Time 3D Tracking of Multiple Objects With Similar Appearances](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Sekii_Robust_Real-Time_3D_CVPR_2016_paper.pdf)
    * [Semantic Filtering](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Yang_Semantic_Filtering_CVPR_2016_paper.pdf)
    * [Learnt Quasi-Transitive Similarity for Retrieval From Large Collections of Faces](http://arxiv.org/abs/1603.00560)

cv-foundation còn hào phóng đính kèm trong source link download các paper, đồng thời có cả bibtex của các bài, nếu kết hợp với arxiv api thì có thể thống kê được nhiều thứ hay ho hơn nữa =))

# Một số thống kê về tác giả

Thử xem phân phối số lượng tác giả trên đầu bài của CVPR16 thế nào. Theo như kết quả, số bài ở CVPR16 trung bình có từ 2, 3 hoặc 4 tác giả đứng tên. Nhiều nhất là các bài có 3 tác giả (186 bài). Ngoại trừ gã outlier 13 tác giả thì biểu đồ đã gần giống với _phân phối chuẩn_ rồi.

![Biểu đồ phân bố số lượng tác giả trong một bài báo](http://i.imgur.com/gpHfOTW.png)

Có _1843_ tác giả có bài trong CVPR16\. Ngoài _Ming-Hsuan Yang_ bá đạo ở trên, trong danh sách tác giả nhiều bài còn có những cái tên nổi bật như: Pascal Fua, Li Fei-Fei. Dưới đây là danh sách các tác giả có nhiều bài nhất trong CVPR16:

1. Lei Zhang [[scholar](https://scholar.google.com/citations?user=tAK5l1IAAAAJ)] [[homepage](http://www4.comp.polyu.edu.hk/~cslzhang/)]: 7 bài.
2. In So Kweon [[scholar](https://scholar.google.com.sg/citations?user=XA8EOlEAAAAJ&hl=en)] [[homepage](http://rcv.kaist.ac.kr/v2/bbs/member_detail.php?mb_id=%20iskweon)]: 7 bài.
3. Antonio Torralba [[scholar](https://scholar.google.com/citations?user=8cxDHS4AAAAJ)] [[homepage](http://web.mit.edu/torralba/www/)]: 7 bài.
4. Jiashi Feng [[scholar](https://scholar.google.com.sg/citations?hl=en&user=Q8iay0gAAAAJ&view_op=list_works&sortby=pubdate)] [[homepage](https://sites.google.com/site/jshfeng/)]: 7 bài.
5. Wangmeng Zuo [[scholar](https://scholar.google.com/citations?user=rUOpCEYAAAAJ)] [[homepage](http://homepage.hit.edu.cn/pages/wangmengzuo)]: 7 bài.
6. Anton van den Hengel [[scholar](https://scholar.google.com.sg/citations?user=nMGZ2ZQAAAAJ&hl=en)] [[homepage](https://cs.adelaide.edu.au/~hengel/)]: 8 bài.
7. Bernt Schiele [[scholar](https://scholar.google.com/citations?user=z76PBfYAAAAJ)] [[homepage](https://www.mpi-inf.mpg.de/departments/computer-vision-and-multimodal-computing/people/bernt-schiele/)]: 8 bài.
8. Luc Van Gool [[scholar](https://scholar.google.com.hk/citations?user=TwMib_QAAAAJ&hl=zh-CN)] [[homepage](http://www.vision.ee.ethz.ch/~vangool/)]: 8 bài.
9. Xiaogang Wang [[scholar](https://scholar.google.com.sg/citations?user=-B5JgjsAAAAJ&hl=en)] [[homepage](http://www.ee.cuhk.edu.hk/~xgwang/)]: 9 bài.
10. Ming-Hsuan Yang [[scholar](https://scholar.google.com/citations?user=p9-ohHsAAAAJ)] [[homepage](http://faculty.ucmerced.edu/mhyang/)]: 11 bài.

Một điểm mình quan tâm nữa là mối quan hệ giữa các tác giả với nhau <del>đó là lí do mình viết: một mình chống mafia ở đoạn trên</del>. Ở đây mình dùng `graph-tool` để minh hoạ data đã thu thập được. Cách xây dựng đồ thị khá đơn giản: những tác giả đứng chung bài với nhau sẽ có cạnh nối với nhau.

Xưa kia nhà toán học Michael Gurevich đã từng thử điều này với các nhà toán học, và hiện nay bài toán [Six degree of Seperation](https://research.facebook.com/blog/three-and-a-half-degrees-of-separation/) đã nổi tiếng và quan tâm nhiều.

![Vision Gang](http://i.imgur.com/QIiCNur.png)

Nhìn hình ta có thể hình dung có 1 hội mafia cực lớn dây mơ rễ má với nhau. Và các team lẻ lẻ hơn thì bị nằm ngoài rìa, có 1 số team hoạt động khá độc lập (nằm giữa vùng trung tâm và vành đai). Đồng thời những chấm đỏ mỏng manh nằm ngoài vùng vành đai chính là các thánh một mình chống mafia, xin hoan nghênh các anh.

# Chủ đề của `CVPR16`

![Main topics](http://i.imgur.com/9AxhgVP.png)

Ban đầu mình dự định sử dụng `arvix-api` để lấy keywords từ Bibtex tuy nhiên vì có cơ số bài hiện chưa có trên Arvix (mình sample 5 bài và cả 5 bài đều không được tìm thấy trên đó) nên không có cách để lấy chính xác keywords.

Có 2 cách tiếp cận:

1. Dựa vào tiêu đề. Cách này sẽ nhanh hơn vì dữ liệu này đã có sẵn.
2. Dựa vào nội dung. Cách làm tương đối đơn giản nhưng hơi mất thời gian: (1) download đống paper từ `cv-foundation`, (2) dùng `pdf2text` lưu text, (3) dùng 1 số thuật toán clustering để phân loại.

Cách thứ (2) tương đối dài hơi nên mình ưu tiên dùng cách thứ (1) trước. Một thuật toán để rút trích keywords khá nổi tiếng là [RAKE](https://github.com/aneesha/RAKE/blob/master/rake.py). Dưới đây là kết quả.

```
    deep convolutional neural networks
    convolutional neural networks
    recurrent neural networks
    deep neural networks
    salient object detection
    convolutional networks
    sparse coding
    object detection
    image segmentation
    action recognition
    semantic segmentation
    optical flow
    shot learning
    unsupervised learning
    activity recognition
    set registration
    person re
    image
    pose
    detection
    video
    learning

```

# Future Works

Hiện giờ minh đang tìm cách download toàn bộ pdf của bài năm nay để làm clustering và phân tích nội dung, đồng thời làm 1 tool search nho nhỏ. Ngoài ra hiện giờ mình đang tìm kiếm danh sách các bài các năm trước để có thêm 1 số phân tích hay ho hơn nữa (về trending, các bài được cite nhiều,).
