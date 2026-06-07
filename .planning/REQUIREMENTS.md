# REQUIREMENTS.md

## 1. Mục tiêu tài liệu

Tài liệu này tổng hợp yêu cầu nghiệp vụ bước đầu cho dự án phần mềm quản lý nội bộ của TPCo, dựa trên các sheet trong `truongphat.drawio`, ngoại trừ các sheet có chữ `nháp`.

Mục tiêu của tài liệu:

- Làm rõ phạm vi 6 module cốt lõi đang xuất hiện trong sơ đồ tổng quan.
- Tách phần yêu cầu đã thể hiện rõ trên sơ đồ với phần giả định cần xác nhận thêm.
- Tạo đầu vào cho 2 tài liệu tiếp theo: `ARCHITECTURE.md` và `PRICING.md`.

## 2. Nguồn phân tích

Nguồn chính dùng để phân tích:

- `HÌnh Dung tổng quan`
- `Sơ đồ cơ cấu`
- `CRM-Usecase`
- `HRM-usecase`
- `flow đặt hàng sản xuất`

Sheet `Quản lý công việc/project - yêu cầu` được xem là nhu cầu mở rộng tiềm năng, chưa đưa vào 6 module cốt lõi của scope hiện tại.

Sheet `Nháp-Ko xem` bị loại khỏi phân tích.

## 3. Bối cảnh nghiệp vụ hiện tại

TPCo là doanh nghiệp sản xuất tại Việt Nam. Tại thời điểm phân tích, các thông tin sau đã rõ:

- Công ty có hoạt động theo chuỗi: đại lý hoặc nhà phân phối, sale admin, kế toán, tổ sản xuất, kho, đội xe.
- Quy trình đặt hàng có liên quan trực tiếp đến công nợ, ký quỹ hoặc đặt cọc, sản xuất, nhập kho, xuất kho và vận chuyển.
- Tồn tại nhu cầu quản lý vật liệu theo sản phẩm và theo đơn hàng.
- Hoạt động quản trị hiện nay có dấu hiệu còn thủ công ở một số khâu như nhập Excel, theo dõi hiệu suất, xác nhận thưởng, gọi điện nhận đơn.

Các thông tin chưa rõ nhưng ảnh hưởng lớn đến giải pháp:

- Quy mô người dùng theo phòng ban và theo chi nhánh.
- Cơ cấu tổ chức chính thức của TPCo.
- Hạ tầng CNTT hiện tại, mức độ sẵn sàng cho cloud hoặc on-premise.
- Mức độ tự động hóa mong muốn cho từng module.
- Mức ưu tiên giữa MVP và các phase mở rộng.

## 4. Phạm vi 6 module cốt lõi

6 module nằm trong scope chính của dự án pre-sale:

1. CRM
2. HRM
3. Hệ thống đặt hàng sản xuất
4. Quản lý sản phẩm
5. Báo cáo tổng hợp
6. Quản lý đội xe

## 5. Vai trò người dùng sơ bộ

Các vai trò có thể suy ra từ sơ đồ hiện tại:

- Ban giám đốc
- Giám đốc kinh doanh
- Phòng kinh doanh
- Sale Admin
- Kế toán
- Marketing
- Nhân viên
- Tổ trưởng hoặc đại diện tổ sản xuất
- Thành viên tổ sản xuất
- Kho
- Lái xe
- Đại lý vùng
- Đại lý tỉnh
- Đại lý cấp 2
- Nhà phân phối

Nhận định quan trọng:

- Mô hình kênh phân phối có khả năng cần hỗ trợ nhiều cấp linh hoạt, không nên hard-code đúng 2 cấp hoặc 3 cấp.
- Quyền truy cập dữ liệu nhiều khả năng phải chia theo vai trò, phòng ban, và phạm vi dữ liệu phụ trách.

## 6. Yêu cầu tổng thể toàn hệ thống

### 6.1 Yêu cầu bắt buộc ở mức nền tảng

- Đăng nhập cho nhiều loại người dùng nội bộ và đối tác ngoài doanh nghiệp nếu có self-service.
- Phân quyền theo vai trò và phạm vi dữ liệu.
- Ghi nhận lịch sử thao tác trên dữ liệu quan trọng.
- Theo dõi trạng thái của đơn hàng, khách hàng, sản phẩm, xe, bảo trì.
- Tra cứu và lọc dữ liệu theo nhiều tiêu chí.
- Xuất dữ liệu để phục vụ vận hành và báo cáo.

### 6.2 Yêu cầu tích hợp nội bộ

- CRM phải liên thông với đơn hàng, công nợ, và báo cáo.
- Đơn hàng phải liên thông với sản phẩm, sản xuất, kho, công nợ, và đội xe.
- HRM phải có đầu vào từ chấm công và có thể nhận dữ liệu hiệu suất từ hệ thống đặt hàng hoặc sản xuất.
- Báo cáo tổng hợp phải lấy dữ liệu từ toàn bộ các module cốt lõi.

### 6.3 Yêu cầu quản trị dữ liệu

- Dữ liệu khách hàng, đại lý, nhà phân phối cần có cấu trúc chuẩn, tránh trùng lặp.
- Dữ liệu sản phẩm phải đủ chi tiết để làm cơ sở tính vật liệu, giá thành, và báo cáo.
- Dữ liệu đơn hàng phải cho phép truy vết từ lúc tiếp nhận đến lúc giao hàng.

## 7. Phân tích chi tiết theo module

## 7.1 Module CRM

### 7.1.1 Mục tiêu nghiệp vụ

Quản lý thông tin khách hàng, lịch sử chăm sóc, công nợ hoặc ký quỹ, và theo dõi đơn hàng liên quan đến từng khách hoặc từng đại lý.

### 7.1.2 Vai trò liên quan

- Sale Admin
- Kế toán
- Giám đốc
- Phòng kinh doanh

### 7.1.3 Yêu cầu chức năng chính

- Quản lý hồ sơ khách hàng.
- Quản lý thông tin cá nhân hoặc thông tin pháp lý của khách hàng hoặc đối tác.
- Ghi nhận lịch sử chăm sóc khách hàng.
- Phân biệt hình thức tương tác: gọi điện hoặc gặp trực tiếp.
- Lưu nội dung trao đổi sau mỗi lần chăm sóc.
- Theo dõi đơn hàng của khách hàng.
- Theo dõi công nợ và ký quỹ của khách hàng.
- Thêm, sửa, xem hồ sơ khách hàng.
- Thêm, sửa, xem dữ liệu công nợ và ký quỹ.
- Phân quyền để Sale Admin chỉ xem và quản lý khách hàng thuộc phạm vi của mình.

### 7.1.4 Yêu cầu nghiệp vụ chi tiết

- Một khách hàng hoặc đối tác cần gắn với người phụ trách chính.
- Lịch sử trao đổi cần có thời gian, người thực hiện, hình thức trao đổi, nội dung, kết quả, và bước tiếp theo.
- Công nợ thanh toán không theo logic FIFO cố định; kế toán hoặc Sale Admin phải biết khách đang thanh toán cho đơn nào.
- Hệ thống nên cho phép gán khoản thanh toán vào đúng đơn hàng cần cấn trừ.
- Dữ liệu khách hàng nên liên kết với cấu trúc kênh phân phối như nhà phân phối, đại lý vùng, đại lý tỉnh, đại lý cấp 2 nếu TPCo áp dụng.

### 7.1.5 Dữ liệu chính cần quản lý

- Khách hàng
- Đơn vị phân phối hoặc đại lý
- Liên hệ
- Lịch sử chăm sóc
- Đơn hàng liên quan
- Công nợ
- Ký quỹ hoặc đặt cọc

### 7.1.6 Tích hợp với module khác

- Đồng bộ với hệ thống đặt hàng để xem danh sách đơn hàng theo khách.
- Đồng bộ với báo cáo để tính doanh thu, lợi nhuận, công nợ theo khách hoặc theo kênh phân phối.
- Đồng bộ với kế toán hoặc nghiệp vụ thu tiền để hạch toán thanh toán theo đơn.

### 7.1.7 Điểm cần xác nhận thêm

- TPCo có cần cổng cho đại lý tự tra cứu công nợ và đơn hàng hay không.
- Có cần tự động nhắc lịch chăm sóc hay không.
- Có cần AI tóm tắt cuộc gọi, trích xuất ý chính, hoặc gợi ý follow-up hay không.
- Khách hàng được tổ chức theo cấp nào: nhà phân phối, đại lý, cửa hàng, người mua cuối, hay kết hợp.

## 7.2 Module HRM

### 7.2.1 Mục tiêu nghiệp vụ

Quản lý chấm công, ngày phép, dữ liệu nhân sự phục vụ tính lương thưởng, và theo dõi hiệu suất của tổ sản xuất.

### 7.2.2 Vai trò liên quan

- Giám đốc
- Kế toán
- Nhân viên

### 7.2.3 Yêu cầu chức năng chính

- Quản lý hồ sơ nhân sự cơ bản.
- Chấm công.
- Nhận dữ liệu từ máy chấm công FaceID.
- Bổ sung hoặc sửa thông tin chấm công.
- Quản lý ngày phép.
- Theo dõi phép năm và phép tháng nếu chính sách có tách biệt.
- Theo dõi lỗi và nhóm lỗi trong quá trình làm việc.
- Tính lương thưởng.
- Theo dõi hiệu suất làm việc của tổ sản xuất.

### 7.2.4 Yêu cầu nghiệp vụ chi tiết

- Hệ thống cần nhận hoặc nhập dữ liệu chấm công từ máy FaceID.
- Khi dữ liệu chấm công sai hoặc thiếu, phải có quy trình bổ sung hoặc điều chỉnh có kiểm soát.
- Dữ liệu hiệu suất tổ sản xuất có thể là đầu vào cho lương thưởng.
- Quy trình hiện tại cho thấy kế toán gửi hiệu suất, tổ trưởng chia tiền cho nhân viên, nhân viên ký xác nhận; điều này cho thấy có nhu cầu workflow xác nhận thưởng hoặc ít nhất là ghi nhận phân bổ thưởng.
- Hệ thống phải hỗ trợ tính lương thưởng dựa trên nhiều nguồn dữ liệu: chấm công, phép, hiệu suất, lỗi.
- Có thể cần hỗ trợ nhập liệu chuyển tiếp từ Excel trong giai đoạn đầu.

### 7.2.5 Dữ liệu chính cần quản lý

- Nhân viên
- Phòng ban hoặc tổ sản xuất
- Ca làm hoặc lịch làm việc
- Bản ghi chấm công
- Đơn xin nghỉ hoặc số dư phép
- Chỉ số hiệu suất
- Lỗi và nhóm lỗi
- Bảng lương thưởng

### 7.2.6 Tích hợp với module khác

- Nhận dữ liệu hiệu suất từ hệ thống đặt hàng sản xuất hoặc module báo cáo sản xuất.
- Cung cấp dữ liệu lương thưởng và hiệu suất cho module báo cáo tổng hợp.

### 7.2.7 Điểm cần xác nhận thêm

- TPCo đang dùng máy FaceID của hãng nào và có API không.
- Công thức lương thưởng có cố định hay thay đổi theo tổ, vai trò, hoặc thời kỳ.
- Có yêu cầu nhân viên tự xem công, phép, bảng lương hay không.
- Có cần chữ ký số hoặc xác nhận điện tử cho bảng chia thưởng không.

## 7.3 Module Hệ thống đặt hàng sản xuất

### 7.3.1 Mục tiêu nghiệp vụ

Số hóa quy trình từ tiếp nhận đơn hàng, kiểm tra điều kiện công nợ hoặc đặt cọc, phê duyệt sản xuất, thực hiện sản xuất, nhập kho, đến giao hàng và thanh toán hoàn tất.

### 7.3.2 Vai trò liên quan

- Đại lý hoặc nhà phân phối
- Sale Admin
- Hệ thống nội bộ
- Kế toán
- Giám đốc kinh doanh
- Tổ sản xuất
- Kho

### 7.3.3 Yêu cầu chức năng chính

- Tiếp nhận đơn hàng.
- Hỗ trợ ít nhất 2 cách tạo đơn: khách gọi cho admin đặt hộ, hoặc khách tự đặt.
- Sale Admin chỉnh sửa đơn theo chuẩn công ty.
- Quản lý đơn hàng theo vòng đời nghiệp vụ.
- Kiểm tra điều kiện công nợ, ký quỹ, hoặc đặt cọc trước khi vào sản xuất.
- Trình duyệt trường hợp khách có nợ xấu hoặc nằm trong danh sách xấu.
- Bắt đầu sản xuất sau khi đủ điều kiện.
- Theo dõi các tổ sản xuất nhận việc và hoàn thành.
- Nhập kho thành phẩm.
- Thông báo hoàn thành đơn hàng.
- Yêu cầu khách thanh toán.
- Tạo lệnh xuất kho.
- Điều phối sang bước vận chuyển.

### 7.3.4 Quy trình nghiệp vụ rút ra từ sơ đồ

- Khách hoặc đại lý đăng nhập và tạo đơn, hoặc gọi điện để Sale Admin nhập đơn.
- Sale Admin chuẩn hóa hoặc chỉnh sửa nội dung đơn theo mẫu công ty.
- Hệ thống ghi nhận đơn hàng và đánh giá điều kiện công nợ hoặc ký quỹ.
- Nếu khách thuộc diện nợ xấu hoặc blacklist thì chuyển kế toán hoặc giám đốc kinh doanh duyệt.
- Nếu đủ điều kiện hoặc đã được duyệt thì đơn chuyển sang trạng thái được phép sản xuất.
- Các tổ sản xuất nhận đơn theo trình tự công đoạn.
- Khi đơn hoàn thành, hệ thống ghi nhận nhập kho.
- Hệ thống hoặc Sale Admin thông báo cho khách về tình trạng hoàn tất và yêu cầu thanh toán.
- Sau thanh toán, hệ thống tạo lệnh xuất kho và thực hiện vận chuyển.

### 7.3.5 Yêu cầu nghiệp vụ chi tiết

- Đơn hàng cần có trạng thái rõ ràng theo từng bước: mới tạo, chờ kiểm tra điều kiện, chờ đặt cọc, chờ duyệt ngoại lệ, được duyệt sản xuất, đang sản xuất, hoàn thành, nhập kho, chờ thanh toán, sẵn sàng giao, đã giao.
- Đặt cọc có thể tính theo phần trăm đơn hàng.
- Trường hợp khách hàng tự đặt và trường hợp admin đặt hộ đều phải lưu rõ nguồn tạo đơn.
- Hệ thống cần lưu lý do từ chối hoặc không duyệt đơn.
- Sơ đồ cho thấy có thể chỉnh sửa chi phí vật liệu của sản phẩm theo từng đơn; điều này nghĩa là đơn hàng cần hỗ trợ tùy chỉnh định mức hoặc chi phí vật liệu ở cấp đơn.
- Các tổ sản xuất cần nhìn thấy đơn nào đang chờ công đoạn của mình.
- Khi chuyển giai đoạn, hệ thống cần đảm bảo truy vết ai thực hiện và thời điểm nào.

### 7.3.6 Dữ liệu chính cần quản lý

- Đơn hàng
- Khách hàng hoặc đại lý đặt hàng
- Dòng sản phẩm trong đơn
- Giá, chiết khấu, đặt cọc, công nợ
- Trạng thái phê duyệt
- Trạng thái sản xuất
- Trạng thái thanh toán
- Trạng thái kho và giao vận

### 7.3.7 Tích hợp với module khác

- CRM để lấy thông tin khách hàng, công nợ, lịch sử mua hàng.
- Quản lý sản phẩm để lấy danh mục sản phẩm và định mức vật liệu.
- HRM và báo cáo để tính hiệu suất tổ sản xuất.
- Kho và quản lý đội xe để xuất kho và vận chuyển.
- Báo cáo tổng hợp để tính doanh thu, lợi nhuận, chi phí theo đơn.

### 7.3.8 Điểm cần xác nhận thêm

- Khách có thật sự tự đặt trên hệ thống hay hiện chỉ gọi điện cho Sale Admin.
- Điều kiện nào kích hoạt yêu cầu đặt cọc.
- Danh sách xấu hoặc nợ xấu hiện được quản lý ở đâu.
- Có bao nhiêu công đoạn sản xuất chuẩn và có thay đổi theo loại sản phẩm không.
- Có cần tích hợp chữ ký xác nhận giao hàng hay biên bản giao nhận hay không.

## 7.4 Module Quản lý sản phẩm

### 7.4.1 Mục tiêu nghiệp vụ

Quản lý danh mục sản phẩm làm nền cho bán hàng, sản xuất, tính vật liệu, và báo cáo.

### 7.4.2 Vai trò liên quan

- Sale Admin hoặc bộ phận phụ trách sản phẩm
- Kế toán hoặc quản trị dữ liệu
- Bộ phận sản xuất

### 7.4.3 Yêu cầu chức năng chính

- Thêm mới sản phẩm.
- Chỉnh sửa sản phẩm.
- Quản lý trạng thái sản phẩm: mở sản xuất hoặc dừng sản xuất.
- Lưu thông tin chi tiết sản phẩm.

### 7.4.4 Thông tin chi tiết sản phẩm cần có theo sơ đồ

- Mã hàng
- Loại hàng sản xuất hoặc mô tả
- Khối lượng hoặc định mức vật liệu sắt, thép, tôn
- Khối lượng hoặc định mức vật liệu sơn

### 7.4.5 Yêu cầu nghiệp vụ chi tiết

- Sản phẩm phải có bộ mã duy nhất để liên kết xuyên suốt từ đơn hàng tới báo cáo.
- Trạng thái sản phẩm phải ngăn việc chọn sản phẩm đã dừng sản xuất vào đơn mới.
- Dữ liệu vật liệu của sản phẩm là đầu vào cho báo cáo vật liệu kho và phân tích lợi nhuận.
- Hệ thống cần hỗ trợ sửa thông tin khi có thay đổi định mức hoặc mô tả.
- Do sơ đồ đặt hàng cho thấy có thể thay đổi chi phí vật liệu theo từng đơn, cần phân biệt rõ dữ liệu chuẩn ở cấp sản phẩm và dữ liệu override ở cấp đơn hàng.

### 7.4.6 Dữ liệu chính cần quản lý

- Danh mục sản phẩm
- Nhóm hoặc loại sản phẩm
- Định mức vật liệu
- Trạng thái sản phẩm
- Phiên bản hoặc lịch sử thay đổi nếu cần truy vết

### 7.4.7 Tích hợp với module khác

- Cung cấp dữ liệu cho đơn hàng, sản xuất, và báo cáo.
- Là đầu vào để tính chi phí vật liệu và lợi nhuận.

### 7.4.8 Điểm cần xác nhận thêm

- Có quản lý BOM nhiều cấp hay chỉ cần định mức vật liệu tổng.
- Có cần quản lý đơn vị tính, quy cách, kích thước, màu sắc, hoặc biến thể sản phẩm không.
- Ai là owner dữ liệu sản phẩm.

## 7.5 Module Báo cáo tổng hợp

### 7.5.1 Mục tiêu nghiệp vụ

Tổng hợp dữ liệu toàn doanh nghiệp để lãnh đạo và các bộ phận theo dõi hiệu quả bán hàng, chi phí, vật liệu, hiệu suất sản xuất, và tình hình vận hành.

### 7.5.2 Các nhóm báo cáo thể hiện trên sơ đồ

- Báo cáo lãi
- Báo cáo chi phí theo đơn
- Báo cáo vật liệu kho
- Báo cáo theo sản phẩm
- Báo cáo về các tổ sản xuất
- Báo cáo hiệu suất

### 7.5.3 Yêu cầu phân tích chi tiết

- Báo cáo lãi cần xem ít nhất theo đơn hàng.
- Báo cáo lãi có thể cần xem theo đại lý hoặc nhà phân phối.
- Báo cáo lãi có thể cần xem theo khách hàng.
- Báo cáo theo sản phẩm cần gắn với lượng đặt hàng và lợi nhuận.
- Báo cáo vật liệu kho cần dựa trên định mức vật liệu sản xuất của sản phẩm.
- Báo cáo chi phí theo đơn cần tổng hợp các khoản chi phí trực tiếp liên quan đến đơn.
- Báo cáo tổ sản xuất cần phản ánh hiệu suất hoặc kết quả thực hiện của từng tổ.

### 7.5.4 Yêu cầu nghiệp vụ chi tiết

- Hệ thống phải cho phép lọc báo cáo theo thời gian, khách hàng, kênh phân phối, sản phẩm, tổ sản xuất.
- Báo cáo phải truy xuất được nguồn dữ liệu, tránh chỉ hiển thị số tổng hợp không giải thích được.
- Dữ liệu lợi nhuận cần làm rõ bao gồm những cấu phần chi phí nào: vật liệu, sản xuất, vận chuyển, chi phí bán hàng, chi phí khác.
- Các chỉ số hiệu suất nên lấy từ kết quả đơn hàng hoàn thành, năng suất tổ, và dữ liệu chấm công nếu có.

### 7.5.5 Dữ liệu đầu vào chính

- Đơn hàng
- Sản phẩm
- Định mức vật liệu
- Công nợ, thu tiền
- Tiến độ và kết quả sản xuất
- Dữ liệu nhân sự hoặc chấm công nếu dùng cho hiệu suất
- Dữ liệu kho và giao vận nếu tính chi phí đầy đủ

### 7.5.6 Điểm cần xác nhận thêm

- Lợi nhuận cần tính theo biên lợi nhuận gộp hay lợi nhuận ròng.
- TPCo có chuẩn KPI chính thức cho từng phòng ban chưa.
- Dashboard cần realtime hay chấp nhận cập nhật theo batch.

## 7.6 Module Quản lý đội xe

### 7.6.1 Mục tiêu nghiệp vụ

Quản lý phương tiện vận chuyển, lái xe, chuyến đi, và bảo trì để kiểm soát chi phí vận hành và hỗ trợ giao hàng.

### 7.6.2 Vai trò liên quan

- Bộ phận vận hành vận tải
- Kho
- Lái xe
- Kế toán hoặc quản lý chi phí

### 7.6.3 Yêu cầu chức năng chính

- Quản lý đội xe.
- Phân loại xe ngoài và xe nhà máy.
- Quản lý lái xe.
- Quản lý chuyến xe.
- Quản lý quá trình bảo trì.
- Thêm mới bản ghi bảo trì.

### 7.6.4 Thông tin cần quản lý theo sơ đồ

- Với chuyến xe:
  - Km đi
  - Km về
  - Tiền mua xăng dầu
  - Chi phí ăn nghỉ trên đường
  - Chi phí di chuyển khác

- Với bảo trì:
  - Ai bảo trì
  - Loại bảo trì gì

### 7.6.5 Yêu cầu nghiệp vụ chi tiết

- Cần phân biệt chi phí vận hành theo từng chuyến xe.
- Cần theo dõi lịch sử bảo trì theo từng xe.
- Cần quản lý thông tin liên kết giữa xe, lái xe, và chuyến đi.
- Do sơ đồ tổng quan cho thấy đội xe chở hàng từ kho đến đại lý hoặc nhà phân phối, hệ thống nên cho phép liên kết chuyến xe với lệnh giao hàng hoặc đơn xuất kho.
- Nếu có dùng xe ngoài, hệ thống cần làm rõ cơ chế quản lý chi phí thuê ngoài và chứng từ liên quan.

### 7.6.6 Dữ liệu chính cần quản lý

- Xe
- Loại xe
- Chủ sở hữu hoặc hình thức sử dụng
- Lái xe
- Chuyến xe
- Chi phí chuyến xe
- Bảo trì

### 7.6.7 Tích hợp với module khác

- Nhận lệnh giao hàng từ hệ thống đặt hàng hoặc kho.
- Cung cấp dữ liệu chi phí vận chuyển cho báo cáo tổng hợp.

### 7.6.8 Điểm cần xác nhận thêm

- Có cần điều xe, phân tuyến, lịch xe theo ngày hay không.
- Có cần theo dõi đăng kiểm, bảo hiểm, hạn bảo dưỡng định kỳ hay không.
- Có cần ứng dụng mobile cho lái xe hay không.

## 8. Liên kết liên phòng ban và phụ thuộc nghiệp vụ

Các phụ thuộc quan trọng giữa module:

- CRM tạo nền dữ liệu khách hàng và công nợ cho hệ thống đặt hàng.
- Hệ thống đặt hàng kích hoạt sản xuất, kho, và giao vận.
- Quản lý sản phẩm cung cấp định mức để tính vật liệu và lợi nhuận.
- HRM nhận dữ liệu hiệu suất từ sản xuất để tính lương thưởng.
- Báo cáo tổng hợp phụ thuộc dữ liệu sạch, thống nhất từ tất cả module.
- Quản lý đội xe là mắt xích cuối của quy trình fulfillment.

Nếu thiếu thiết kế tích hợp tốt, rủi ro lớn nhất là:

- Công nợ không khớp với đơn hàng.
- Vật liệu và lợi nhuận tính sai do định mức không chuẩn.
- Hiệu suất tổ sản xuất không truy vết được theo đơn.
- Chi phí giao vận không được cộng đúng vào báo cáo.

## 9. Phạm vi đề xuất cho MVP

Đề xuất MVP nên tập trung vào năng lực vận hành cốt lõi trước:

- Quản lý khách hàng, công nợ, và lịch sử chăm sóc ở mức đủ dùng.
- Quản lý danh mục sản phẩm và định mức vật liệu cơ bản.
- Số hóa quy trình đặt hàng sản xuất từ tiếp nhận đến xuất kho.
- Báo cáo cốt lõi: doanh thu, công nợ, lợi nhuận theo đơn, vật liệu, hiệu suất tổ.
- Quản lý đội xe ở mức cơ bản: xe, lái xe, chuyến xe, bảo trì.
- HRM ưu tiên chấm công, ngày phép, và đầu vào cho lương thưởng trước khi mở rộng self-service.

Các hạng mục có thể để phase sau nếu ngân sách hoặc timeline hạn chế:

- AI tóm tắt cuộc gọi CRM.
- Portal tự đặt hàng đầy đủ cho đại lý.
- Workflow xác nhận thưởng điện tử phức tạp.
- Dashboard realtime toàn hệ thống.
- Mobile app chuyên biệt cho lái xe.

## 10. Hạng mục ngoài phạm vi chính nhưng nên ghi nhận backlog

Sheet `Quản lý công việc/project - yêu cầu` cho thấy khách có thể còn nhu cầu về module giao việc hoặc quản lý project nội bộ, với các khả năng:

- Tạo mới việc hoặc project.
- Giao việc cho từng người.
- Theo dõi tiến độ.
- Cập nhật, phản hồi, comment hoặc chat.
- Chuyển tiếp công việc.
- Đóng hoặc hoàn thành.

Nhận định hiện tại:

- Đây chưa phải một trong 6 module cốt lõi của scope chính.
- Nên giữ lại như backlog hoặc phase 2 sau khi xác nhận với L.

## 11. Rủi ro và giả định nghiệp vụ

### 11.1 Giả định đang dùng để phân tích

- TPCo có mô hình sản xuất theo đơn hàng.
- Quy trình công nợ hoặc đặt cọc là một chốt kiểm soát trước sản xuất.
- Dữ liệu vật liệu là yếu tố quan trọng để tính lợi nhuận.
- Hệ thống cần phục vụ cả nội bộ lẫn một phần đối tác bên ngoài trong tương lai.

### 11.2 Rủi ro nếu không xác nhận sớm

- Scope nở nhanh do kênh phân phối nhiều cấp quá linh hoạt.
- Kiến trúc sai nếu thực tế cần tích hợp với nhiều hệ thống hiện hữu.
- Báo giá sai nếu công thức lương thưởng hoặc quy trình duyệt quá phức tạp.
- Chọn sai ưu tiên nếu khách chỉ cần số hóa một phần thay vì ERP đầy đủ.

## 12. Danh sách câu hỏi cần xác nhận với L

### 12.1 Về tổ chức và vận hành

- Quy mô công ty hiện tại là bao nhiêu người, bao nhiêu phòng ban, bao nhiêu xưởng.
- Có bao nhiêu vai trò thực tế sẽ dùng hệ thống hằng ngày.
- Có bao nhiêu chi nhánh, kho, hoặc địa điểm sản xuất.

### 12.2 Về kênh bán hàng và CRM

- Cấu trúc nhà phân phối và đại lý hiện tại đang theo mấy cấp.
- Khách có tự đặt hàng trên hệ thống hay chỉ thông qua Sale Admin.
- Quy tắc quản lý công nợ, ký quỹ, blacklist hiện tại là gì.

### 12.3 Về sản xuất và sản phẩm

- Một đơn hàng đi qua bao nhiêu công đoạn sản xuất.
- Định mức vật liệu hiện đang quản lý ở đâu.
- Có bao nhiêu loại sản phẩm và mức độ biến thể của sản phẩm.

### 12.4 Về HRM

- Công thức tính lương thưởng hiện tại như thế nào.
- Máy chấm công có thể tích hợp trực tiếp hay phải import file.
- Có cần nhân viên tự xem dữ liệu cá nhân hay không.

### 12.5 Về báo cáo và dữ liệu

- Báo cáo nào là bắt buộc phải có ngay từ phase 1.
- Dữ liệu gốc hiện nằm ở Excel, phần mềm kế toán, hay hệ thống nào khác.
- Ban giám đốc muốn xem dashboard realtime hay báo cáo định kỳ.

### 12.6 Về triển khai

- Khách ưu tiên triển khai toàn bộ hay theo từng phase.
- Có ràng buộc về thời gian, ngân sách, hay hạ tầng không.
- Có yêu cầu on-premise, cloud, hoặc hybrid không.

## 13. Kết luận sơ bộ

Phạm vi hiện tại cho thấy đây không chỉ là một hệ thống quản lý bán hàng đơn lẻ mà là bài toán ERP nội bộ tập trung vào trục `khách hàng -> đơn hàng -> sản xuất -> kho -> giao vận -> báo cáo`, kèm theo HRM phục vụ vận hành nhà máy.

Trọng tâm của giai đoạn tiếp theo nên là:

- Chốt scope MVP với L.
- Xác định các luồng dữ liệu và điểm tích hợp quan trọng.
- Đề xuất kiến trúc đủ linh hoạt cho mô hình phân phối nhiều cấp và sản xuất theo đơn.
