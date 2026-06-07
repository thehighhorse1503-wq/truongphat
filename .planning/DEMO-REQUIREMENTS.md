# Demo Requirements - TPCo

Nguồn hiện trạng: `CUSTOMER-DISCOVERY.md`.

Mục tiêu: xác định demo ít effort nhất nhưng vẫn chứng minh đúng pain point khách.

## 1. Functional requirements

### F1. Google Sheets audit/mapping

- Nhận file Google Sheets mẫu.
- Xác định sheet nào là source of truth.
- Xác định sheet nào là báo cáo, sheet nào là nhập liệu, sheet nào là trung gian.
- Map trường dữ liệu đơn hàng sang model demo.
- Ghi lại công thức quan trọng đang chứa logic nghiệp vụ.
- Chưa cam kết đồng bộ trước khi mapping xong.

### F2. Đơn hàng

- Tạo đơn hàng.
- Thêm nhiều dòng sản phẩm.
- Có thông tin khách hàng, ngày giao, khối lượng và giá trị.
- Có trạng thái đơn hàng.
- Có người tạo và người phụ trách.
- Xem được đơn trên mobile.

### F3. Duyệt đơn

- Gửi đơn đi duyệt.
- Người có quyền duyệt hoặc từ chối.
- Lưu người duyệt, thời điểm duyệt và lý do từ chối nếu có.
- Đơn đã duyệt không được sửa trực tiếp theo cách ghi đè dữ liệu cũ.

### F4. Version đơn hàng

- Khi cần sửa đơn đã phát hành, tạo version mới.
- Version mới liên kết với version gốc.
- Xem được danh sách version của cùng một đơn.
- Version cũ không bị mất.
- Lưu lý do sửa.
- Chặn sửa trực tiếp version đã chốt nếu không có quyền đặc biệt.

### F5. Hạch toán theo version

- Chỉ một version của một đơn được đánh dấu là bản hạch toán.
- Nếu chọn version mới để hạch toán, version cũ phải bị bỏ trạng thái hạch toán.
- Xem rõ bản nào không hạch toán.
- Logic này phải được kiểm soát bằng hệ thống, không phụ thuộc ghi nhớ của người dùng.

### F6. Audit trail

- Lưu người thao tác.
- Lưu thời điểm thao tác.
- Lưu thay đổi trạng thái.
- Lưu lịch sử duyệt.
- Lưu lịch sử version.
- Không xóa cứng dữ liệu nghiệp vụ trong demo.

### F7. Chuẩn bị cho sản xuất

- Đơn đã duyệt có thể chuyển sang hàng chờ sản xuất.
- Có thông tin khối lượng, ngày giao và sản phẩm để phục vụ lập lịch.
- Demo không cần lập lịch sản xuất hoàn chỉnh.
- Cần preview được hướng phase 2: đơn -> sản xuất -> báo cáo tiến độ -> khoán.

### F8. Mobile

- Tạo đơn cơ bản trên mobile.
- Duyệt đơn trên mobile.
- Xem trạng thái đơn trên mobile.
- Xem dashboard đơn hàng tối thiểu trên mobile.

## 2. Non-functional requirements

### N1. Hiệu năng

- Thao tác tạo và duyệt đơn phải nhanh hơn Google Sheets nặng hiện tại.
- Không để người dùng phải mở nhiều màn hình sâu để làm một tác vụ đơn giản.

### N2. Phân quyền

- Phân quyền theo vai trò.
- Phân quyền theo hành động: xem, tạo, sửa, duyệt, chọn bản hạch toán.
- Nếu có thể, phân quyền theo phạm vi dữ liệu: người phụ trách, phòng ban hoặc nhóm.

### N3. Audit và dữ liệu

- Không xóa cứng bản ghi nghiệp vụ.
- Nếu hệ thống nền có chức năng xóa, demo phải khóa hoặc ẩn quyền xóa với người dùng nghiệp vụ.
- Dữ liệu đã chốt phải không bị ghi đè im lặng.

### N4. Khả năng mở rộng phase

- Phase 1 không được thiết kế cụt.
- Dữ liệu đơn hàng phải dùng tiếp được cho phase 2 sản xuất.
- Sau này thêm giao việc văn phòng không được làm đứt liên kết với đơn hàng và sản xuất.

### N5. Tích hợp Google Sheets

- Ban đầu ưu tiên import/export hoặc mapping rõ ràng.
- Chỉ thiết kế sync sau khi biết sheet nào là source of truth.
- Không hứa sync hai chiều nếu chưa audit file.

## 3. Odoo fit check

### Có sẵn hoặc gần có sẵn

- Sales: quotation và sales order.
- Order lines, product variants, delivery và invoicing flow.
- Lock confirmed sales order nếu bật cấu hình.
- Manufacturing Order và Work Order.
- Shop Floor cho thao tác sản xuất.
- Manufacturing lead time và MPS cho hướng lập lịch.
- Mobile app truy cập được cả module tùy chỉnh.
- Studio/custom module cho field, view, model, automation, approval rule và webhook.
- Access rights và record rules.
- API để tích hợp hệ thống ngoài.

### Cần custom chắc chắn

- Version đơn hàng theo nghiệp vụ TPCo.
- Chọn duy nhất một version hạch toán.
- Không xóa cứng hoặc archive thay delete theo quy tắc riêng.
- Mapping Google Sheets.
- Dashboard/demo đúng ngôn ngữ nghiệp vụ khách.

### Cần kiểm chứng

- Odoo mobile UX có đủ gọn cho tạo đơn nhiều dòng không.
- Chatter/audit mặc định đủ cho yêu cầu truy vết không, hay cần log custom.
- Lock confirmed sales order có phù hợp với mô hình sửa bằng version mới không.
- Manufacturing flow chuẩn có quá nặng cho phase 2 không.
- Odoo Studio đủ cho demo hay phải viết module Python.

## 4. Option demo effort

### Option A: Odoo custom nhẹ

Làm nếu dữ liệu mẫu đơn giản.

Demo gồm:

- Sale Order custom field.
- Duplicate thành version mới.
- Button chọn bản hạch toán.
- Lock bản đã phát hành.
- Log bằng chatter hoặc model history.
- Mobile app Odoo.
- Link sang Manufacturing Order hoặc hàng chờ sản xuất.

Effort dự kiến: thấp đến trung bình.

Rủi ro: mobile form nhiều dòng có thể không mượt; version logic cần code.

### Option B: Odoo custom module nghiêm túc

Làm nếu muốn demo sát nghiệp vụ hơn.

Demo gồm:

- Model `tp.order.version`.
- Workflow duyệt riêng.
- Ràng buộc unique bản hạch toán.
- Log custom.
- Mapping import từ Google Sheets.
- Action tạo Sale Order/MO khi version được chốt.

Effort dự kiến: trung bình.

Rủi ro: không còn là "chỉnh xíu"; nhưng vẫn tận dụng Odoo backend.

### Option C: PHP/Node.js prototype

Làm nếu Odoo form/mobile không đủ gọn.

Demo gồm:

- UI mobile riêng.
- API riêng cho order/version/audit.
- Import/export Google Sheets.
- Có thể sau đó tích hợp Odoo backend.

Effort dự kiến: trung bình.

Rủi ro: phải tự xây nhiều thứ Odoo đã có nếu đi xa hơn phase 1.

## 5. Khuyến nghị demo hiện tại

Thử đánh giá Option A trước bằng dữ liệu mẫu.

Nếu Option A làm được trong ít ngày, đây là đường demo tốt nhất:

- Có nền ERP thật.
- Có mobile app sẵn.
- Có đường sang sản xuất.
- Chứng minh được đội mình customize, không bán phần mềm đóng gói.

Nếu Option A vướng version/hạch toán/mobile, chuyển sang Option B.

Chỉ dùng Option C nếu Odoo khiến demo chậm, khó dùng hoặc khó giải thích.

## 6. Hướng dẫn chọn model demo trong Odoo

Quyết định cần chốt:

- Dùng trực tiếp `sale.order`.
- Hay tạo model riêng `tp.order`, sau đó đẩy sang `sale.order` khi bản hạch toán được chốt.

### Option 1: Dùng trực tiếp `sale.order`

Mô hình:

- Mỗi version đơn là một `sale.order` hoặc quotation riêng.
- Thêm field:
  - `tp_order_group_id`: nhóm các version cùng một đơn.
  - `tp_version_no`: số version.
  - `tp_accounting_version`: bản hạch toán.
  - `tp_previous_version_id`: version trước.
  - `tp_revision_reason`: lý do sửa.
- Khi sửa đơn đã phát hành, duplicate `sale.order` thành version mới.
- Chỉ một order trong cùng nhóm được đánh dấu hạch toán.

Ưu điểm:

- Demo nhanh nhất.
- Tận dụng sẵn Sales, order lines, product, customer, amount, delivery, invoice.
- Dễ show đường sang Manufacturing/Inventory.
- Dùng được mobile app Odoo ngay.

Nhược điểm:

- `sale.order` là model chuẩn của Odoo, chỉnh sâu dễ ảnh hưởng flow bán hàng, giao hàng, invoice.
- Các version không hạch toán vẫn là sale order, có thể gây nhiễu báo cáo nếu không filter kỹ.
- Cần rất cẩn thận để version không hạch toán không tạo delivery/invoice/MO.
- Logic "chỉ một bản hạch toán" phải custom bằng constraint/action.

Chọn khi:

- Dữ liệu đơn hàng của khách gần với cấu trúc sale order.
- Demo cần nhanh.
- Chưa cần kế toán/giao hàng thật trong demo.
- Có thể filter rõ version nháp, version không hạch toán và version hạch toán.

Không chọn khi:

- Đơn hàng hiện tại có nhiều trường, công thức và trạng thái khác xa sale order.
- Version không hạch toán vẫn phải lưu nhưng tuyệt đối không được xuất hiện trong báo cáo bán hàng chuẩn.
- Cần quản lý nhiều vòng sửa/phê duyệt trước khi hình thành sale order thật.

### Option 2: Tạo model riêng `tp.order`

Mô hình:

- `tp.order`: nhóm đơn gốc.
- `tp.order.version`: từng phiên bản của đơn.
- `tp.order.version.line`: dòng sản phẩm/vật tư.
- Chỉ khi một version được chọn hạch toán, hệ thống mới tạo hoặc cập nhật `sale.order`.
- `sale.order` chỉ chứa bản đã chốt để phục vụ sales/invoice/delivery/MO.

Ưu điểm:

- Đúng nghiệp vụ version hơn.
- Dữ liệu chưa hạch toán không làm bẩn sale order chuẩn.
- Dễ kiểm soát audit, trạng thái, quyền sửa, quyền duyệt.
- Dễ map từ Google Sheets vì không bị ép theo cấu trúc Odoo ngay.
- Dễ mở rộng phase 2 nếu sản xuất cần dữ liệu riêng trước khi tạo MO.

Nhược điểm:

- Effort cao hơn.
- Phải tự làm form, list, action, constraint và dashboard cơ bản.
- Phải viết logic chuyển từ `tp.order.version` sang `sale.order`.
- Demo có thể lâu hơn nếu dữ liệu mẫu phức tạp.

Chọn khi:

- Google Sheets phức tạp và chứa nhiều nghiệp vụ riêng.
- Version, hạch toán, audit là điểm thắng chính.
- Không muốn đụng vào `sale.order` quá sớm.
- Muốn demo cho khách thấy hệ thống được thiết kế riêng theo quy trình của họ.

Không chọn khi:

- Cần demo cực nhanh trong vài ngày.
- Đơn hàng rất đơn giản và gần như sale order chuẩn.
- Team chưa muốn viết module Odoo riêng.

### Option 3: Hybrid nhẹ

Mô hình:

- Demo tạo đơn bằng `sale.order` để tận dụng sẵn UI/mobile.
- Tạo thêm model `tp.order.revision` để lưu metadata version và audit riêng.
- Version không hạch toán vẫn là quotation, chưa confirm.
- Chỉ bản hạch toán mới được confirm thành sales order.

Ưu điểm:

- Nhanh hơn model riêng hoàn toàn.
- Ít làm bẩn flow Odoo hơn dùng `sale.order` trần.
- Vẫn có câu chuyện custom rõ.

Nhược điểm:

- Vẫn phải kiểm soát chặt để quotation version không bị confirm nhầm.
- Dữ liệu version nằm rải giữa sale order và model custom.

Chọn khi:

- Muốn demo nhanh nhưng vẫn cần version/audit rõ.
- Dữ liệu mẫu chưa đủ để thiết kế model riêng hoàn chỉnh.
- Cần chứng minh Odoo custom được trước.

### Khuyến nghị hiện tại

Chưa chốt ngay. Sau khi có Google Sheets mẫu, ra quyết định theo bảng sau:

| Điều kiện từ dữ liệu mẫu | Chọn |
| --- | --- |
| Đơn hàng giống sale order chuẩn, ít field đặc thù | `sale.order` trực tiếp |
| Đơn hàng có nhiều field/công thức/trạng thái riêng | `tp.order` riêng |
| Cần demo nhanh nhưng vẫn show version/audit | Hybrid nhẹ |
| Muốn tránh rủi ro làm bẩn dữ liệu sales/invoice/MO | `tp.order` riêng |
| Muốn tận dụng mobile Odoo nhanh nhất | `sale.order` hoặc Hybrid nhẹ |

Default khuyến nghị trước khi có dữ liệu mẫu:

> Hybrid nhẹ: dùng `sale.order`/quotation cho UI và mobile, thêm custom model để quản lý nhóm version, trạng thái hạch toán và audit. Nếu Google Sheets quá phức tạp, nâng lên `tp.order` riêng.

## 7. Câu hỏi cần dữ liệu mẫu trả lời

- Một đơn hàng gồm những trường nào?
- Số dòng sản phẩm trung bình và tối đa mỗi đơn?
- Khi sửa đơn, trường nào hay thay đổi?
- Version hạch toán được chọn lúc nào và bởi ai?
- Có trường hợp nhiều lần sửa sau duyệt không?
- Ai được xem đơn, sửa đơn, duyệt đơn, chọn bản hạch toán?
- Google Sheets hiện đang tính tổng, khối lượng, m2, mét dài bằng công thức nào?
- Dữ liệu nào từ đơn hàng sẽ chuyển sang sản xuất?
- Đơn nào trong Google Sheets tương ứng với đơn nháp, đơn phát hành, đơn hạch toán?
- Có bao nhiêu version trung bình cho một đơn bị sửa?
- Các version không hạch toán có cần xuất hiện trong báo cáo bán hàng không?
- Khi chọn bản hạch toán, có cần khóa toàn bộ version còn lại không?

## 8. Nguồn Odoo chính thức

- Sales quotations: https://www.odoo.com/documentation/19.0/applications/sales/sales/sales_quotations.html
- Create quotations: https://www.odoo.com/documentation/19.0/applications/sales/sales/sales_quotations/create_quotations.html
- Product variants on sales orders: https://www.odoo.com/documentation/19.0/applications/sales/sales/sales_quotations/orders_and_variants.html
- Manufacturing: https://www.odoo.com/documentation/19.0/applications/inventory_and_mrp/manufacturing.html
- Manufacturing orders and work orders: https://www.odoo.com/documentation/saas-19.1/applications/inventory_and_mrp/manufacturing/basic_setup/manufacturing_work_orders.html
- Multilevel BoMs and production planning: https://www.odoo.com/documentation/saas-19.1/applications/inventory_and_mrp/manufacturing/advanced_configuration/sub_assemblies.html
- Lead times: https://www.odoo.com/documentation/saas-19.1/applications/inventory_and_mrp/inventory/warehouses_storage/replenishment/lead_times.html
- Mobile app for customized modules: https://www.odoo.com/documentation/saas-19.1/developer/reference/frontend/mobile.html
- Security: https://www.odoo.com/documentation/19.0/developer/reference/backend/security.html
- Webhooks: https://www.odoo.com/documentation/19.0/applications/studio/automated_actions/webhooks.html
