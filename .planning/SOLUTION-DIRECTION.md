# Hướng giải pháp sơ bộ

Nguồn hiện trạng: `CUSTOMER-DISCOVERY.md`.

Mục tiêu: định hướng giải pháp thuộc năng lực đội cung cấp, chưa phải kiến trúc chốt.

## 1. Nguyên tắc

- Không thay Google Sheets ngay.
- Không triển khai một công cụ giao việc như Base.
- Không bán ERP tổng quát nếu chưa chứng minh được xử lý đúng quy trình riêng.
- Demo phải giải quyết đúng pain point khách nêu, không chỉ trình bày module.

## 2. Yêu cầu giải pháp phải chứng minh

- Mobile nhanh cho lên đơn, duyệt đơn và xem báo cáo.
- Phân quyền tốt hơn Google Sheets.
- Không xóa cứng dữ liệu nghiệp vụ.
- Lưu vết đầy đủ thay đổi quan trọng.
- Sửa đơn sau phát hành bằng version mới.
- Chọn rõ version dùng để hạch toán.
- Kết nối được với Google Sheets hiện tại.
- Mở rộng được sang sản xuất và khoán.
- Sau này thêm giao việc và ký duyệt online nhưng không tách khỏi dữ liệu vận hành.

## 3. Hướng A: Odoo

Phù hợp nếu:

- Muốn tận dụng sẵn các năng lực ERP.
- Cần kho, sản xuất, kế toán, khách hàng, mua bán và báo cáo chuẩn.
- Khách chấp nhận quy trình có phần bám theo khung ERP.

Điểm mạnh:

- Có nền tảng ERP thật.
- Có module sản xuất, kho, kế toán và API.
- Có thể tùy chỉnh bằng Python.

Rủi ro:

- Mobile UX và thao tác nhanh có thể không hợp nếu dùng giao diện Odoo mặc định.
- Version đơn hàng và chọn bản hạch toán theo cách TPCo cần có thể phải tùy chỉnh sâu.
- Tùy chỉnh nhiều có thể làm tăng chi phí và độ phức tạp.
- Nếu khách ghét cảm giác "phải theo phần mềm", Odoo nguyên bản sẽ khó thuyết phục.

Vai trò hợp lý:

- Là backend ERP hoặc nguồn dữ liệu nghiệp vụ chuẩn.
- Không nhất thiết là giao diện người dùng chính.

## 4. Hướng B: PHP/Node.js custom

Phù hợp nếu:

- Quy trình riêng của TPCo là yếu tố quyết định.
- Mobile UX cần cực gọn.
- Version đơn hàng, audit và khoán sản xuất là phần lõi.
- Cần tích hợp Google Sheets theo cách linh hoạt.

Điểm mạnh:

- Thiết kế đúng theo luồng khách đang chạy.
- Dễ tối ưu giao diện mobile.
- Kiểm soát tốt version, audit và quyền dữ liệu.
- Dễ làm demo sát pain point.

Rủi ro:

- Phải tự xây nhiều năng lực ERP nếu phạm vi mở rộng nhanh.
- Cần thiết kế dữ liệu kỹ để không thành Google Sheets phiên bản web.
- Báo cáo, phân quyền và audit phải làm chắc từ đầu.

Vai trò hợp lý:

- Là hệ thống chính cho phase 1 đơn hàng.
- Mở rộng dần sang sản xuất, khoán và giao việc.

## 5. Hướng C: Hybrid Odoo + PHP/Node.js

Phù hợp nếu:

- Muốn có nền ERP chuẩn phía sau nhưng vẫn cần UX và logic riêng.
- Phase 1 cần demo nhanh theo quy trình khách.
- Phase sau có thể cần kho, kế toán hoặc sản xuất chuẩn ERP.

Mô hình:

- PHP/Node.js làm lớp mobile, workflow, version đơn hàng, audit và Google Sheets integration.
- Odoo làm backend cho phần ERP chuẩn nếu cần: sản phẩm, kho, sản xuất, kế toán.

Điểm mạnh:

- Giữ được trải nghiệm tùy chỉnh.
- Không phải tự xây toàn bộ ERP.
- Có đường nâng cấp nếu khách đi sâu vào sản xuất và kho.

Rủi ro:

- Tích hợp hai hệ thống làm tăng độ phức tạp.
- Cần xác định rõ hệ thống nào là nguồn dữ liệu chính cho từng đối tượng.
- Demo phải tránh hứa quá sớm các phần chưa kiểm chứng.

## 6. Khuyến nghị hiện tại

Ưu tiên đánh giá demo theo hướng Odoo custom trước, nhưng chỉ chốt nếu chi phí demo thấp hơn custom PHP/Node.js.

Lý do:

- Odoo có sẵn Sales, Manufacturing, Inventory, audit/chatter, phân quyền, API và mobile app.
- Nếu chỉ cần chỉnh nhẹ Sale Order để thể hiện version, hạch toán, duyệt và chuyển sản xuất, đây có thể là đường demo ít effort nhất.
- Khác MISA/Base/ECOUNT ở chỗ mình không bắt khách tự xử lý trong phần mềm đóng gói; mình customize trên nền có sẵn.

Không demo Odoo nguyên bản. Demo phải là Odoo đã được chỉnh theo luồng TPCo, ẩn bớt phần không liên quan.

Nếu Odoo custom cho phase 1 đụng quá nhiều vào version đơn hàng, Google Sheets mapping hoặc mobile UX, chuyển sang custom PHP/Node.js hoặc hybrid.

## 7. Demo nên tập trung

1. Tạo đơn trên mobile.
2. Duyệt đơn.
3. Sửa đơn đã phát hành thành version mới.
4. Xem lịch sử version.
5. Chọn version hạch toán.
6. Đồng bộ hoặc xuất trạng thái về Google Sheets.
7. Dashboard đơn hàng gọn.
8. Màn hình preview phase 2: báo cáo sản lượng theo m2/mét dài và tính khoán.

## 8. Cách chọn option demo

Chọn option theo effort, không theo sở thích kiến trúc.

| Option | Khi chọn | Khi loại |
| --- | --- | --- |
| Odoo custom | Chỉnh được Sale Order/Quotation, version, audit, quyền và mobile với effort thấp | Phải viết quá nhiều custom để né quy trình Odoo |
| PHP/Node.js custom | Cần UX mobile rất riêng, version/audit là lõi, Google Sheets phức tạp | Phạm vi ERP mở rộng nhanh sang kho/sản xuất/kế toán |
| Hybrid | Odoo mạnh ở backend ERP, custom app mạnh ở mobile/workflow | Tích hợp hai hệ thống làm demo chậm hoặc khó giải thích |

Điều kiện để ưu tiên Odoo custom demo:

- Dữ liệu đơn hàng map được vào `sale.order` và `sale.order.line` hoặc model custom liên kết với `sale.order`.
- Version đơn hàng làm được bằng model custom hoặc duplicate order có quan hệ cha/con.
- Có thể khóa sửa trực tiếp bản đã phát hành.
- Có thể chỉ định một version hạch toán.
- Có thể chứng minh lịch sử thay đổi bằng chatter/audit hoặc log custom.
- Mobile app Odoo đủ dùng cho tạo, duyệt và xem trạng thái.
- Từ đơn hàng có đường rõ sang Manufacturing Order hoặc model chuẩn bị sản xuất.
