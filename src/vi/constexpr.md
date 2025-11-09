---
layout: "post.njk"
title: "constexpr: Hằng biểu thức trong C++11"
date: 2016-10-23
tags:
    - vi
    - cpp
---
## constexpr

Đầu tiên ta xem xét động lực của việc tạo ra từ khoá mới này. Điều mà C++11 muốn tạo ra chính là **tăng tốc hiệu suất của chương trình viết bằng ngôn ngữ này**. Ta quay một chút về cú pháp `define` bất hủ của C, ưu điểm của phương pháp tạo macro chính là hiệu suất nhanh, các hàm được tạo ra trong lúc biên dịch và không tốn bộ nhớ cũng như các lệnh nhảy trong hàm. C++ cũng có tham vọng vậy, và mục tiêu của C++ chính là nếu một biến/hàm có thể tính toán được trong thời gian biên dịch thì tính luôn tại thời điểm đó. Và như vậy trong quá trình chạy chương trình sẽ không mất thêm thời gian tính toán hàm/biến này. Done! Thời gian thực thi chương trình được nhanh hơn.

Nhìn đi nhìn lại mới thấy ngôn ngữ C được thiết kế rất hay, tinh giản nhưng mạnh mẽ. Để giải quyết vấn đề loại bỏ define trong C mà C++ đã chế ra const, inline và tá lả tùng xèn các thứ khác. Tuy nhiên cái gì cũng có hai mặt của vấn đề, với các từ khoá const, inline, ... thì việc người lập trình đỡ nhọc hơn về phần code (hạn chế được các lệnh define) nhưng để sử dụng tốt các tính năng của C++ khiến người lập trình phải hiểu rõ tính năng mà ngôn ngữ đó cung cấp.

## Tầm hoạt động

Từ khoá `constexpr` được sử dụng cho 3 đối tượng như sau:

1. Hàm.
2. Biến.
3. Hàm khởi tạo.

Trong đó, nếu từ khoá này được dùng cho khai báo đối tượng hoặc biến thì đối tượng hoặc biến đó được ngầm hiểu là `const`. Trong trường hợp là hàm, thì hàm đó được ngầm hiểu là 1 hàm `inline`.

Quay lại câu chuyện vì sao có 3 ẻm này.

Từ khoá `constexpr` có hàm nghĩa hoàn toàn khác với `const`:

* `const`: không được thay đổi giá trị.
* `constexpr`: thực thi tại thời điểm biên dịch.

`constexpr` là từ khoá yêu cầu trình biên dịch tính toán phép tính hay biểu thức tại thời điểm biên dịch, trong khi đó `const` là công cụ giúp trình biên dịch nhắc nhở người dùng những biến nào không được thay đổi giá trị (nó chỉ nhắc nhở, có nghĩa là nếu ta muốn đổi cũng ok). `constexpr` liên quan mật thiết tới khái niệm _biểu thức hằng_ (constant expression). Vậy constant expression là gì?

_Biểu thức hằng là biểu thức mà trình biên dịch có thể tính toán được_. Điều đó có nghĩa biểu thức hằng không thể thực thi nếu các biến/ toán tử trong biểu thức chưa được biết trong thời gian biên dịch, và biểu thức này không gây ra tác dụng phụ ([side effect](http://programmers.stackexchange.com/a/40314)). Thêm vào đó, biểu thức hằng phải được cấu thành từ các giá trị nguyên, các số thực và kiểu liệt kê (enumerator), hay các tổ hợp của 3 kiểu dữ liệu này (một trong những cách tổ hợp là tạo ra 1 đối tượng giữ các giá trị này: `constexpr constructor` ra đời là vì lí do này).

Trong quá trình viết mã, người lập trình sẽ có yêu cầu đặt tên biến cho giá trị của biểu thức hằng (`constexpr function` ra đời) hoặc các dữ liệu có trong biểu thức, và đây chính là lí do mà `constexpr variable` ra đời. Ngoài việc đặt tên, biểu thức hằng còn có kha khá công dụng khác nhau như:

1. Sử dụng trong khai báo kích thước mảng, nhãn trong lệnh switch, tham số trong `template`.
2. Trong các hệ thống nhúng, các giá trị _chỉ đọc_ các chi phí thấp hơn so với giá trị dữ liệu động. Ngoài ra dữ liệu chỉ đọc tránh được các lỗi trong hệ thống.
3. Trong các hệ thống đa luồng, biểu thức hằng tránh được hiện tượng [data race](http://docs.oracle.com/cd/E19205-01/820-0619/geojs/index.html).
4. Tăng hiệu suất chương trình.

## constexpr variable

Khi khai báo constexpr thì biến đó được hiểu là const - tức không thể thay đổi nội dung trong quá trình thực thi chương trình. Nhưng khác với const ở chỗ: constexpr là hằng ở quá trình biên dịch, và còn const thì được qui định trong quá trình thực thi.

Để trở khai báo một biến là _constexpr_, biến đó phải thoả mãn một số điều kiện sau:

1. Kiểu của biến phải thuộc [kiểu Literal](http://en.cppreference.com/w/cpp/concept/LiteralType).
2. Khi khai báo là biến _constexpr_, biến đó phải được định nghĩa ngay trong thời điểm đó.
3. Tham số của hàm khởi tạo trong kiểu của biến này phải chứa: (1) kiểu literal, (2) biến _constexpr_, (3) hàm.
4. Hàm khởi tạo của biến được khai báo phải thoả các điều kiện của **constexpr constructor** và trong Kiểu/Lớp đó phải có hàm khởi tạo là **constexpr constructor**.

## constexpr function

Để khai báo là một **constexpr function**, hàm này phải thoả những điều kiện sau:

1. Không phải là hàm ảo ([virtual funciton](http://stackoverflow.com/questions/2391679/why-do-we-need-virtual-methods-in-c)).
2. Kiểu trả về phải là LiteralType.
3. Mỗi tham số đầu vào của hàm phải thuộc kiểu LiteralType.

Hàm chỉ được chứa các lệnh sau:

1. state_assert.
2. Chỉ có duy nhất 1 lệnh `return`.
3. Lệnh Null, lệnh không thực hiện gì.
4. Lệnh khai báo `typedef`.
5. Khai báo sử dụng `using`.

## constexpr constructor

Hàm khởi tạo _constexpr_ được xây dựng nhằm phục vụ cho các biến _constexpr_, vì hàm khởi tạo cũng là hàm nên nó có những yêu cầu buộc thoả mãn giống như _constexpr function_, ngoài ra _constexpr constructor_ còn phải thoả mãn một số điều kiện:

1. Lớp chứa hàm khởi tạo _constexpr_ có hàm cha không phải là Lớp ảo.
2. Không phải hàm khởi tạo function-try-block.

## Ghi chú

Các thông tin trên được lấy từ chuẩn C++11, tuy nhiên trong C++14 có những thay đổi lớn sẽ được cập nhật sau.

## Tham khảo

1. [C++ Programm Language](http://en.cppreference.com/w/cpp/language/constexpr).
2. [Book: C++ Programming Language](http://www.amazon.com/C-Programming-Language-4th/dp/0321563840/ref=sr_1_3?ie=UTF8&qid=1441600777&sr=8-3&keywords=c+programming+language).
