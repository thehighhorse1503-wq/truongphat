# Customer Discovery - TPCo

Nguồn: trao đổi trực tiếp với chủ doanh nghiệp.

Đây là nguồn thông tin hiện trạng ưu tiên. Các giả định cũ trong `BRD.md`, `CONTEXT.md` và `L-CHECKLIST.md` phải được đối chiếu lại với tài liệu này.

## 1. Hiện trạng

- Công ty đã vận hành tốt trên Google Sheets.
- Nhu cầu làm phần mềm không xuất phát từ việc quy trình hiện tại thất bại.
- Google Sheets đang chạm giới hạn:
  - Khó phân quyền chi tiết.
  - File nặng, thao tác chậm.
  - Trải nghiệm trên điện thoại không phù hợp.
  - Khó thực hiện nhanh các việc như lên đơn, duyệt đơn và xem báo cáo.
- Khách đã tham khảo:
  - ECOUNT: ERP.
  - Base.vn: giao việc và vận hành văn phòng. Khách đã thử và không duyệt vì chỉ mạnh ở chia việc, chưa đáp ứng các điểm lõi khác.
  - MISA AMIS: kế toán và giao việc.
- Mỗi sản phẩm giải quyết tốt một phần, nhưng chưa đáp ứng mức tùy chỉnh khách mong muốn.

## 2. Yêu cầu cốt lõi

- Nhanh, gọn, dễ thao tác.
- Chạy tốt trên điện thoại cho các nghiệp vụ cơ bản.
- Phân quyền theo vai trò và phạm vi dữ liệu.
- Không xóa cứng dữ liệu.
- Mọi thay đổi quan trọng phải có lịch sử và người thao tác.
- Triển khai từng phần nhưng phải kết nối được với quy trình Google Sheets hiện tại.
- Không buộc công ty thay toàn bộ cách vận hành ngay từ đầu.

## 3. Nghiệp vụ đơn hàng

- Có thể sửa đơn sau khi đã phát hành.
- Mỗi lần sửa phải tạo và lưu một phiên bản mới.
- Phải xem lại được các phiên bản cũ.
- Phải xác định rõ phiên bản nào được dùng để hạch toán.
- Các phiên bản không được chọn hạch toán vẫn phải được lưu để truy vết.

Quy trình sơ bộ:

> Nhận đơn -> Duyệt đơn -> Giao sản xuất -> Lập lịch sản xuất -> Các tổ báo cáo tiến độ theo đơn.

Lịch sản xuất cần dựa trên:

- Khối lượng đơn hàng.
- Ngày giao hàng.
- Năng lực hoặc tiến độ của các tổ.

## 4. Nghiệp vụ sản xuất và khoán

- Công nhân được khoán theo đơn vị sản lượng, ví dụ:
  - Tiền trên mỗi m2.
  - Tiền trên mỗi mét dài.
- Tổ trưởng ghi nhận kết quả thực hiện.
- Cần lọc theo khoảng thời gian để lấy các đơn đã thực hiện.
- Từ dữ liệu đơn hàng, bóc tách theo chỉ tiêu năng suất.
- Tính hiệu suất từng người hoặc từng tổ.
- Dùng kết quả để chia tiền khoán.

Các điểm cần làm rõ từ dữ liệu mẫu:

- Công thức khoán theo từng loại sản phẩm hoặc công đoạn.
- Cách phân bổ sản lượng khi nhiều người cùng làm một đơn.
- Cách xử lý hàng lỗi, làm lại và điều chỉnh.
- Người nhập, người xác nhận và người duyệt kết quả.

## 5. Phạm vi nghiệp vụ dài hạn

Hệ thống cần phục vụ ba khối:

- Bán hàng.
- Sản xuất.
- Văn phòng: giao việc và ký duyệt online.

Giả định chia phase do khách đưa ra:

1. Phase 1: Đơn hàng.
2. Phase 2: Sản xuất.
3. Phase 3: Quản lý công việc.

Đây là giả định ban đầu, chưa phải kế hoạch triển khai đã chốt.

## 6. Yêu cầu đối với demo

- Khách gửi dữ liệu mẫu.
- Demo phải dùng dữ liệu và tình huống gần với thực tế của khách.
- Có thể làm MVP hoặc vay mượn từ case study khác.
- Demo phải chứng minh được:
  - Thao tác nhanh trên điện thoại.
  - Phân quyền rõ hơn Google Sheets.
  - Sửa đơn nhưng giữ toàn bộ phiên bản.
  - Chọn đúng phiên bản để hạch toán.
  - Duyệt đơn và lưu lịch sử duyệt.
  - Kết nối hoặc trao đổi dữ liệu với Google Sheets.
  - Có đường phát triển tiếp sang lập lịch, báo cáo tiến độ và tính khoán sản xuất.

## 7. Điều kiện làm việc

- Khách muốn có các buổi làm việc trực tiếp tại Hà Nội.
- Việc di chuyển hiện có hai khả năng:
  - Đi nhờ xe người quen: chi phí thấp nhưng lịch bị động.
  - Chủ động phương tiện: cần tính rõ chi phí.
- Chỉ cần chốt mô hình làm việc, tần suất gặp và chi phí sau khi demo đạt yêu cầu và hai bên xác định hợp tác dài hạn.

## 8. Hành động tiếp theo

1. Nhận dữ liệu mẫu và mô tả quy trình hiện tại.
2. Đối chiếu cấu trúc dữ liệu, công thức và phân quyền trong Google Sheets.
3. Chọn một luồng đơn hàng tiêu biểu để làm demo.
4. Chốt tiêu chí khách dùng để đánh giá demo.
5. Sau demo mới xác định phạm vi, lịch triển khai và mô hình làm việc trực tiếp.
