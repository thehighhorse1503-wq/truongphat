# Bài học từ Base.vn

Nguồn: khách đã thử Base và không duyệt.

## 1. Kết luận

Base không phải hướng giải pháp cho TPCo.

Base mạnh ở:

- Chia việc.
- Theo dõi công việc.
- Quy trình phê duyệt.
- Vận hành văn phòng.
- Mobile cho tác vụ ngắn.

Base không đáp ứng đủ ở các điểm khách cần cho hệ thống lõi:

- Quản lý đơn hàng theo nghiệp vụ riêng.
- Sửa đơn sau phát hành nhưng giữ version.
- Chọn một version để hạch toán.
- Kết nối chặt với Google Sheets hiện tại.
- Luồng đơn hàng nối sang sản xuất.
- Tự lập lịch sản xuất theo khối lượng và ngày giao.
- Theo dõi tiến độ sản xuất theo đơn.
- Tính khoán theo m2, mét dài, tổ và người.
- Audit và không xóa cứng dữ liệu theo yêu cầu vận hành lõi.

## 2. Điểm mạnh nên học từ Base

- Giao diện giao việc đơn giản.
- Người dùng dễ thấy việc của mình.
- Có trạng thái, người phụ trách và deadline rõ.
- Mobile phù hợp thao tác nhanh.
- Quy trình duyệt dễ hiểu với người dùng văn phòng.
- Thông báo và nhắc việc là một phần tự nhiên của luồng làm việc.

## 3. Bài học cho giải pháp của mình

Không cạnh tranh bằng cách làm một công cụ giao việc giống Base.

Giải pháp cần nổi bật ở phần Base không giải quyết được:

- Đơn hàng là dữ liệu lõi, không chỉ là một task.
- Version đơn hàng là thiết kế lõi.
- Hạch toán phải chỉ rõ dùng version nào.
- Google Sheets được kế thừa theo phase, không thay thế đột ngột.
- Sản xuất phải nối trực tiếp từ đơn đã duyệt.
- Khoán sản xuất phải tính theo công thức thực tế của TPCo.
- Lưu vết phải phục vụ nghiệp vụ, không chỉ ghi log thao tác.

## 4. Cách dùng Base trong phân tích

Base chỉ dùng làm benchmark cho:

- UX giao việc.
- Mobile task flow.
- Phê duyệt online.
- Thông báo và nhắc việc.
- Cách tổ chức việc theo người phụ trách.

Không dùng Base làm:

- Nền tảng triển khai.
- Kiến trúc đề xuất.
- Phương án pilot.
- Hệ thống lõi đơn hàng hoặc sản xuất.

## 5. Hàm ý cho phase 3

Phase 3 quản lý công việc nên học cách Base làm tốt:

- Việc phải có owner.
- Việc phải có deadline.
- Việc phải có trạng thái rõ.
- Người dùng mobile phải xử lý được việc nhanh.
- Việc phát sinh từ đơn hàng hoặc sản xuất phải giữ liên kết về dữ liệu gốc.

Nhưng phase 3 không nên tách thành một module giao việc độc lập nếu làm đứt mạch dữ liệu đơn hàng và sản xuất.
