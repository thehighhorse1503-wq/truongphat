# Business Requirements Document (BRD)

## 1. Document Overview

### 1.1 Purpose

Tài liệu này được lập để mô tả và xác nhận bài toán kinh doanh, phạm vi nghiệp vụ, các vấn đề vận hành và các yêu cầu business cốt lõi của TPCo. BRD đóng vai trò làm cơ sở thống nhất trước khi chuyển sang các tài liệu solution, architecture và implementation planning.

### 1.2 Document Status

- Trạng thái tài liệu: Draft for Business Validation.
- Trạng thái phần giải pháp: Pending.
- Mức độ hoàn thiện hiện tại: Đủ để xác nhận bối cảnh, vấn đề, mục tiêu và phạm vi nghiệp vụ; chưa đủ để chốt kiến trúc và báo giá.


## 2. Executive Summary

Theo cách hiểu hiện tại, TPCo đang có nhu cầu xây dựng một hệ thống quản trị nội bộ theo hướng ERP phục vụ chuỗi vận hành từ khách hàng, đơn hàng, kiểm soát điều kiện tài chính, sản xuất, kho, giao vận đến báo cáo quản trị.

Phạm vi nghiệp vụ đang được xác nhận gồm 6 nhóm năng lực cốt lõi:

1. CRM
2. HRM
3. Hệ thống đặt hàng sản xuất
4. Quản lý sản phẩm
5. Báo cáo tổng hợp
6. Quản lý đội xe

BRD này không nhằm đề xuất công nghệ hay mô hình triển khai. Tài liệu tập trung trả lời ba câu hỏi chính:

- TPCo đang vận hành trong bối cảnh nào.
- Những vấn đề nghiệp vụ nào cần được giải quyết.
- Hệ thống tương lai phải đáp ứng các yêu cầu business nào.

## 3. Business Context

### 3.1 Company Operating Context

Theo sơ đồ hiện có, TPCo đang vận hành trong bối cảnh của một doanh nghiệp sản xuất với chuỗi hoạt động gắn chặt giữa bán hàng, xử lý đơn, sản xuất, kho, giao vận và theo dõi hiệu quả kinh doanh.

Các đặc điểm vận hành nổi bật được suy ra từ tài liệu nguồn:

- Có hoạt động bán hàng thông qua đại lý hoặc nhà phân phối.
- Có luồng tiếp nhận đơn hàng gắn với kiểm soát công nợ, ký quỹ hoặc đặt cọc.
- Có hoạt động sản xuất theo đơn hàng hoặc chủ yếu theo đơn hàng.
- Có nhu cầu quản lý vật liệu sản xuất theo từng sản phẩm và có thể theo từng đơn.
- Có nhu cầu theo dõi hiệu suất tổ sản xuất và sử dụng dữ liệu đó cho lương thưởng.
- Có nhu cầu kiểm soát hoạt động vận chuyển và đội xe phục vụ giao hàng.

### 3.2 Organizational Context

Từ sơ đồ cơ cấu hiện có, có thể suy ra TPCo có ít nhất các nhóm vai trò hoặc bộ phận sau:

- Ban giám đốc
- Phòng kinh doanh
- Sale Admin
- Marketing
- Kế toán
- Xưởng sản xuất
- Tổ sản xuất
- Kho
- Hệ thống đại lý hoặc nhà phân phối nhiều cấp

Cơ cấu tổ chức chính thức, số lượng đơn vị vận hành và phạm vi trách nhiệm của từng vai trò vẫn cần được xác nhận lại.

### 3.3 Current-State Business Flow

Luồng vận hành đang được hiểu ở mức high-level như sau:

Khách hàng hoặc đối tác phân phối phát sinh nhu cầu mua hàng, đơn hàng được tiếp nhận và kiểm tra điều kiện tài chính, sau đó chuyển vào sản xuất, hoàn thành nhập kho, xuất kho, giao hàng và cuối cùng được phản ánh lên báo cáo quản trị.

Trục vận hành chính hiện đang được hiểu là:

Khách hàng hoặc đại lý -> Đơn hàng -> Điều kiện tài chính -> Sản xuất -> Kho -> Giao vận -> Báo cáo

## 4. Problem Statement

### 4.1 Fragmented Operational Data

Thông tin khách hàng, đơn hàng, công nợ, sản phẩm, sản xuất, kho và giao vận chưa thể hiện là đang được quản lý trên một luồng dữ liệu thống nhất. Điều này tạo ra rủi ro đứt mạch thông tin và khó truy vết vòng đời đầy đủ của một đơn hàng.

### 4.2 Manual Sales and Credit Control Activities

Quy trình nhận đơn, xác nhận thanh toán, đối chiếu công nợ, kiểm tra blacklist hoặc nợ xấu có dấu hiệu phụ thuộc vào trao đổi thủ công, gọi điện hoặc xử lý rời rạc. Đây là điểm nghẽn trực tiếp đối với tốc độ xử lý đơn và khả năng kiểm soát rủi ro tài chính.

### 4.3 Incomplete Production Status Visibility

Luồng từ tiếp nhận đơn đến sản xuất, hoàn thành, nhập kho và giao hàng có nhiều điểm bàn giao giữa các bộ phận. Nếu không có trạng thái nghiệp vụ thống nhất, doanh nghiệp sẽ khó kiểm soát tiến độ, trách nhiệm và nguyên nhân chậm trễ.

### 4.4 Product and Material Master Data Risk

Dữ liệu sản phẩm và vật liệu như sắt, thép, tôn, sơn là nền tảng để tính định mức, kiểm soát tồn vật liệu, xác định chi phí và tính lãi. Nếu dữ liệu master không được chuẩn hóa, báo cáo quản trị sẽ thiếu độ tin cậy.

### 4.5 Limited Management Reporting Reliability

Nhu cầu báo cáo trải rộng từ lãi, chi phí theo đơn, vật liệu kho, hiệu suất tổ sản xuất đến báo cáo theo sản phẩm. Nếu nguồn dữ liệu nằm phân tán ở nhiều file hoặc nhiều bộ phận, ban điều hành khó có được một góc nhìn kịp thời và nhất quán.

### 4.6 Weak HR-to-Operation Linkage

Dữ liệu chấm công, phép, lỗi sản xuất, hiệu suất tổ sản xuất và lương thưởng có dấu hiệu chưa liên kết thành một chuỗi quản trị rõ ràng. Điều này làm tăng rủi ro thiếu minh bạch khi đánh giá hiệu suất và chi trả.

### 4.7 Limited Centralized Fleet Cost Control

Vận hành xe nội bộ và xe thuê ngoài có nhiều thành phần chi phí như xăng dầu, ăn nghỉ, di chuyển, bảo trì. Nếu không có cơ chế quản lý tập trung, chi phí logistics và hiệu quả sử dụng xe khó được theo dõi chính xác.

## 5. Business Objectives

Dựa trên tài liệu nguồn, dự án đang hướng đến các mục tiêu business sau:

- Chuẩn hóa dữ liệu và quy trình vận hành cốt lõi của doanh nghiệp.
- Theo dõi đơn hàng xuyên suốt từ tiếp nhận đến giao hàng.
- Kiểm soát điều kiện tài chính trước sản xuất, bao gồm công nợ, đặt cọc hoặc ký quỹ.
- Quản lý sản phẩm và vật liệu để hỗ trợ sản xuất và đánh giá hiệu quả.
- Liên kết dữ liệu vận hành sản xuất với dữ liệu nhân sự để phục vụ chấm công, hiệu suất và lương thưởng.
- Quản trị giao vận và đội xe để kiểm soát chi phí giao hàng.
- Cung cấp báo cáo quản trị đáng tin cậy cho ban lãnh đạo và các bộ phận liên quan.

## 6. Scope and Boundaries

### 6.1 In-Scope Business Capabilities

| Module | Business Purpose |
| --- | --- |
| CRM | Quản lý khách hàng, lịch sử chăm sóc, công nợ hoặc ký quỹ và liên kết với đơn hàng |
| HRM | Quản lý dữ liệu nhân sự, chấm công, phép, lỗi, hiệu suất và đầu vào cho lương thưởng |
| Hệ thống đặt hàng sản xuất | Quản lý vòng đời đơn hàng từ tiếp nhận đến giao hàng |
| Quản lý sản phẩm | Quản lý sản phẩm, mã hàng, trạng thái sản phẩm và dữ liệu vật liệu hoặc định mức |
| Báo cáo tổng hợp | Cung cấp báo cáo điều hành về lãi, chi phí, vật liệu, sản phẩm và hiệu suất |
| Quản lý đội xe | Quản lý phương tiện, lái xe, chuyến xe, bảo trì và chi phí vận chuyển |

### 6.2 Out of Scope for This BRD

Các nội dung dưới đây nằm ngoài phạm vi của BRD hiện tại:

- Thiết kế giải pháp kỹ thuật chi tiết
- Kiến trúc hệ thống
- Lựa chọn công nghệ
- Thiết kế triển khai theo phase chi tiết
- Báo giá dự án
- Module quản lý công việc hoặc project nội bộ theo kiểu Trello

### 6.3 Phase Note

Việc một năng lực nằm trong phạm vi business không đồng nghĩa với việc năng lực đó phải được triển khai trong cùng một phase. Việc chia phase sẽ được xác định sau khi hoàn thành business validation.

## 7. Stakeholders and User Groups

| Stakeholder Group | Vai trò trong dự án hoặc vận hành |
| --- | --- |
| Ban giám đốc hoặc chủ doanh nghiệp | Xác nhận mục tiêu kinh doanh, ưu tiên đầu tư và phạm vi quyết định |
| Phòng kinh doanh | Sử dụng dữ liệu khách hàng, đơn hàng và kênh phân phối |
| Sale Admin | Tiếp nhận, chuẩn hóa và xử lý đơn hàng theo quy trình công ty |
| Kế toán | Kiểm soát công nợ, đặt cọc, ký quỹ, thanh toán và điều kiện tài chính |
| Kho | Quản lý nhập kho, xuất kho và liên kết với giao hàng |
| Xưởng và tổ sản xuất | Thực hiện sản xuất, cập nhật trạng thái, hiệu suất và lỗi |
| Bộ phận nhân sự | Quản lý nhân sự, chấm công, phép, lương thưởng |
| Bộ phận vận hành đội xe | Quản lý lái xe, xe, chuyến xe, bảo trì và chi phí logistics |
| Đại lý hoặc nhà phân phối | Có thể là bên tham gia trực tiếp vào luồng đặt hàng hoặc tra cứu, tùy mức độ self-service được xác nhận |

## 8. Enterprise-Level Business Requirements

Các yêu cầu nghiệp vụ áp dụng ở cấp toàn hệ thống gồm:

- Người dùng phải đăng nhập được theo vai trò.
- Dữ liệu phải được phân quyền theo phòng ban, vai trò và phạm vi phụ trách.
- Các giao dịch quan trọng phải có lịch sử thao tác và khả năng truy vết.
- Các đối tượng chính như khách hàng, đơn hàng, sản phẩm, xe, chuyến xe và bảo trì phải có trạng thái nghiệp vụ rõ ràng.
- Hệ thống phải hỗ trợ tìm kiếm, lọc và tra cứu dữ liệu nhanh.
- Hệ thống phải tạo ra dữ liệu đủ sạch và nhất quán để phục vụ báo cáo quản trị.
- Các bộ phận tham gia cùng một vòng đời đơn hàng phải có cùng một nguồn dữ liệu tham chiếu.

## 9. Detailed Business Requirements by Domain

### 9.1 CRM

#### 9.1.1 Business Purpose

Quản lý khách hàng và kênh phân phối, theo dõi lịch sử chăm sóc, quản lý công nợ hoặc ký quỹ và liên kết hoạt động khách hàng với đơn hàng.

#### 9.1.2 Business Requirements

- Quản lý hồ sơ khách hàng hoặc đối tác phân phối.
- Quản lý thông tin liên hệ và thông tin pháp lý cơ bản.
- Quản lý lịch sử chăm sóc khách hàng.
- Ghi nhận hình thức chăm sóc như gọi điện hoặc gặp trực tiếp.
- Lưu nội dung trao đổi, kết quả trao đổi và bước tiếp theo.
- Theo dõi đơn hàng theo từng khách hàng hoặc từng đối tác phân phối.
- Quản lý công nợ và ký quỹ ở mức phục vụ quyết định kinh doanh.
- Cho phép gán khoản thanh toán vào đúng đơn hàng cần cấn trừ, không bắt buộc theo FIFO.
- Phân quyền để Sale Admin chỉ xem hoặc quản lý tệp khách hàng phụ trách.

#### 9.1.3 Items Requiring Confirmation

- Khách hoặc đại lý có cần tự tra cứu đơn hàng và công nợ hay không.
- Cấu trúc kênh phân phối hiện tại đang theo bao nhiêu cấp.
- Có cần AI hỗ trợ tóm tắt nội dung cuộc gọi hay không.

### 9.2 HRM

#### 9.2.1 Business Purpose

Quản lý dữ liệu nhân sự và chấm công để phục vụ vận hành, tính lương thưởng và đo hiệu suất sản xuất.

#### 9.2.2 Business Requirements

- Quản lý hồ sơ nhân sự cơ bản.
- Quản lý chấm công.
- Nhận dữ liệu từ máy chấm công FaceID hoặc từ một phương thức nhập liệu trung gian.
- Cho phép bổ sung hoặc điều chỉnh dữ liệu chấm công có kiểm soát.
- Quản lý ngày phép.
- Quản lý lỗi và nhóm lỗi nếu đây là tiêu chí tính thưởng hoặc đánh giá.
- Tính lương thưởng dựa trên dữ liệu chấm công, phép, hiệu suất và lỗi.
- Ghi nhận hiệu suất tổ sản xuất làm đầu vào cho tính thưởng hoặc đánh giá.

#### 9.2.3 Items Requiring Confirmation

- Công thức lương thưởng hiện đang tính theo cách nào.
- Có cần self-service cho nhân viên hay không.
- Máy chấm công hiện dùng giải pháp nào và có tích hợp được không.

### 9.3 Production Order Management System

#### 9.3.1 Business Purpose

Số hóa luồng từ tiếp nhận đơn, kiểm tra điều kiện tài chính, phê duyệt ngoại lệ, tổ chức sản xuất, nhập kho, thanh toán và giao hàng.

#### 9.3.2 Business Requirements

- Hỗ trợ tiếp nhận đơn hàng.
- Hỗ trợ ít nhất hai cách tạo đơn: khách tự đặt hoặc Sale Admin đặt hộ.
- Sale Admin có thể chỉnh sửa đơn theo chuẩn công ty.
- Hệ thống phải quản lý trạng thái đơn hàng theo từng giai đoạn nghiệp vụ.
- Hệ thống phải kiểm tra điều kiện công nợ, ký quỹ hoặc đặt cọc trước khi đơn đi vào sản xuất.
- Trường hợp khách có nợ xấu hoặc blacklist thì phải có luồng duyệt ngoại lệ.
- Đơn được duyệt phải chuyển vào sản xuất.
- Tổ sản xuất cần thấy đơn đang chờ ở công đoạn của mình.
- Khi đơn hoàn thành phải ghi nhận nhập kho.
- Sau khi hoàn thành cần có luồng yêu cầu thanh toán và tạo lệnh xuất kho.
- Giao hàng phải gắn được với bước vận chuyển.
- Đơn hàng cần lưu rõ nguồn tạo đơn, lý do từ chối, lịch sử chuyển trạng thái và các mốc thời gian.
- Hệ thống cần hỗ trợ trường hợp điều chỉnh chi phí vật liệu theo từng đơn.

#### 9.3.3 Items Requiring Confirmation

- Khách có thực sự tự đặt trên hệ thống hay chưa.
- Điều kiện nào bắt buộc phải đặt cọc.
- Ai phê duyệt các trường hợp công nợ rủi ro.
- Có bao nhiêu công đoạn sản xuất chuẩn.

### 9.4 Product Management

#### 9.4.1 Business Purpose

Quản lý danh mục sản phẩm và dữ liệu định mức vật liệu làm nền cho đơn hàng, sản xuất và báo cáo.

#### 9.4.2 Business Requirements

- Quản lý danh mục sản phẩm.
- Thêm mới và chỉnh sửa sản phẩm.
- Quản lý trạng thái sản phẩm như đang sản xuất hoặc dừng sản xuất.
- Quản lý mã hàng và mô tả sản phẩm.
- Quản lý dữ liệu vật liệu như sắt, thép, tôn và sơn.
- Phân biệt dữ liệu định mức chuẩn của sản phẩm với dữ liệu điều chỉnh theo từng đơn nếu có.

#### 9.4.3 Items Requiring Confirmation

- Có cần BOM nhiều cấp hay chỉ cần định mức tổng.
- Có quản lý biến thể sản phẩm hay không.
- Ai là owner nghiệp vụ của dữ liệu sản phẩm.

### 9.5 Management Reporting

#### 9.5.1 Business Purpose

Cung cấp bức tranh điều hành tổng hợp để ban lãnh đạo và các bộ phận theo dõi hiệu quả bán hàng, sản xuất, chi phí và vận hành.

#### 9.5.2 Business Requirements

- Có báo cáo lãi.
- Có báo cáo chi phí theo đơn.
- Có báo cáo vật liệu kho.
- Có báo cáo theo sản phẩm.
- Có báo cáo về tổ sản xuất.
- Có báo cáo hiệu suất.
- Báo cáo phải lọc được theo thời gian, khách hàng, kênh phân phối, sản phẩm và tổ sản xuất.
- Báo cáo phải truy được nguồn dữ liệu chính để kiểm tra ngược.
- Dữ liệu lợi nhuận phải làm rõ được các cấu phần chi phí chính.

#### 9.5.3 Items Requiring Confirmation

- TPCo cần các báo cáo nào là bắt buộc cho phase đầu.
- Lợi nhuận cần tính theo logic nào.
- Có cần dashboard realtime hay không.

### 9.6 Fleet Management

#### 9.6.1 Business Purpose

Quản trị giao vận nội bộ để kiểm soát xe, lái xe, chuyến xe, bảo trì và chi phí vận chuyển.

#### 9.6.2 Business Requirements

- Quản lý xe ngoài và xe nhà máy.
- Quản lý lái xe.
- Quản lý chuyến xe.
- Quản lý bảo trì xe.
- Ghi nhận dữ liệu chuyến xe như km đi, km về, chi phí xăng dầu, chi phí ăn nghỉ và chi phí di chuyển khác.
- Ghi nhận thông tin bảo trì như người bảo trì và loại bảo trì.
- Liên kết chuyến xe với lệnh giao hàng hoặc đơn xuất kho nếu cần.

#### 9.6.3 Items Requiring Confirmation

- Có cần điều xe hoặc phân tuyến hay không.
- Có cần quản lý đăng kiểm, bảo hiểm và bảo dưỡng định kỳ hay không.
- Có cần mobile app cho lái xe hay không.

## 10. Cross-Functional Process Dependencies

Các phụ thuộc liên phòng ban và liên module đang được hiểu như sau:

- CRM cung cấp dữ liệu khách hàng, lịch sử giao dịch và công nợ cho luồng đặt hàng.
- Hệ thống đặt hàng là trục chính liên kết khách hàng, sản phẩm, sản xuất, kho, thanh toán và giao vận.
- Quản lý sản phẩm cung cấp dữ liệu định mức hoặc vật liệu cho sản xuất và báo cáo.
- HRM nhận dữ liệu hiệu suất sản xuất để phục vụ lương thưởng hoặc đánh giá.
- Báo cáo tổng hợp lấy dữ liệu từ toàn bộ hệ thống.
- Quản lý đội xe tiếp nhận nhu cầu giao hàng từ kho hoặc từ đơn hàng đã đủ điều kiện xuất.

## 11. Business Rules and Operational Constraints

### 11.1 Key Business Rules

- Đơn hàng chỉ được chuyển sang sản xuất khi đáp ứng điều kiện tài chính phù hợp với chính sách của doanh nghiệp.
- Các trường hợp khách hàng có nợ xấu, blacklist hoặc vượt ngưỡng rủi ro phải có cơ chế duyệt ngoại lệ.
- Khoản thanh toán có thể cần được gán vào một đơn hàng cụ thể, không mặc định phân bổ theo FIFO.
- Dữ liệu sản phẩm và dữ liệu vật liệu phải được kiểm soát bởi owner nghiệp vụ rõ ràng.
- Dữ liệu hiệu suất sản xuất có thể là đầu vào cho lương thưởng hoặc đánh giá nhân sự.

### 11.2 Operational Constraints

- Doanh nghiệp đang vận hành trong bối cảnh nhiều bộ phận cùng tham gia vào một vòng đời đơn hàng.
- Chất lượng dữ liệu hiện trạng và mức độ chuẩn hóa dữ liệu chưa được xác nhận đầy đủ.
- Mức độ sẵn sàng của người dùng, hệ thống hiện hữu và hạ tầng kỹ thuật chưa được xác nhận.
- Khả năng dự án phải triển khai theo phase là cao, nhưng chưa được chốt chính thức.

## 12. Assumptions, Dependencies, and Risks

### 12.1 Assumptions

- TPCo là doanh nghiệp sản xuất theo đơn hàng hoặc chủ yếu theo đơn hàng.
- Công nợ, đặt cọc hoặc ký quỹ là một cơ chế kiểm soát tài chính quan trọng trước sản xuất.
- Dữ liệu vật liệu là yếu tố trọng yếu trong việc tính lãi và kiểm soát kho.
- Các luồng hiện tại đang có mức độ thủ công đủ lớn để cần một hệ thống quản lý tập trung.

### 12.2 Dependencies

- Xác nhận cơ cấu tổ chức, số lượng người dùng và phạm vi vận hành thực tế từ TPCo.
- Xác nhận chính sách công nợ, đặt cọc, blacklist và cơ chế phê duyệt ngoại lệ.
- Xác nhận mô hình sản xuất, số công đoạn và cách các tổ sản xuất đang nhận việc.
- Xác nhận nguồn dữ liệu hiện tại, bao gồm Excel, phần mềm kế toán, máy chấm công và dữ liệu kho.

### 12.3 Key Risks

- Nếu dữ liệu nguồn hiện tại không sạch hoặc không nhất quán, effort chuẩn hóa dữ liệu có thể cao hơn dự kiến.
- Nếu phạm vi module phase đầu không được chốt sớm, phần kiến trúc và báo giá có thể bị sai lệch.
- Nếu quy trình thực tế khác đáng kể so với sơ đồ hiện có, BRD sẽ cần cập nhật đáng kể trước khi sang phase solution design.
- Nếu nhiều stakeholder có kỳ vọng khác nhau về mức độ số hóa, dự án có nguy cơ mở rộng scope không kiểm soát.

## 13. Success Criteria

BRD này được xem là hoàn thành mục tiêu nếu các điều kiện sau được đáp ứng:

- Các stakeholder business chính xác nhận rằng bối cảnh vận hành và luồng nghiệp vụ chính được mô tả đúng ở mức đủ dùng cho bước phân tích tiếp theo.
- TPCo xác nhận 6 nhóm năng lực nêu trong phạm vi là đúng hoặc nêu rõ phần cần bổ sung hoặc loại bỏ.
- Các điểm còn mơ hồ về công nợ, sản xuất, dữ liệu sản phẩm, HRM, báo cáo và đội xe được phân loại thành confirmed, pending hoặc out of scope.
- Tài liệu có đủ cơ sở để làm đầu vào cho giai đoạn solution design và lập kế hoạch triển khai.

## 14. Open Items Requiring Business Confirmation

### 14.1 Organization and Governance

- Quy mô người dùng thực tế là bao nhiêu.
- Có bao nhiêu bộ phận, xưởng, kho và địa điểm vận hành.
- Ai là người ra quyết định cuối cùng về phạm vi nghiệp vụ.

### 14.2 Sales, Customer, and Financial Control

- Kênh phân phối hiện tại đang theo mô hình mấy cấp.
- Đại lý hoặc nhà phân phối có cần tài khoản riêng để tự thao tác hay không.
- Cách kiểm soát công nợ và blacklist hiện nay là gì.
- Điều kiện nào bắt buộc phải đặt cọc hoặc ký quỹ.

### 14.3 Production Operations

- Có bao nhiêu công đoạn sản xuất tiêu chuẩn.
- Tổ sản xuất đang nhận việc và xác nhận hoàn thành bằng cách nào.
- Có cần quản lý tiến độ theo từng công đoạn chi tiết hay không.

### 14.4 HR and Performance Management

- Công thức lương thưởng hiện tại ra sao.
- Hiệu suất tổ sản xuất đang được chấm và xác nhận theo cách nào.
- Có cần nhân viên tự tra cứu dữ liệu nhân sự hay không.

### 14.5 Data and Reporting

- Dữ liệu hiện đang nằm ở Excel, sổ sách, phần mềm kế toán hay hệ thống khác.
- Những báo cáo nào là bắt buộc phải có ngay ở phase đầu.
- Ban giám đốc mong muốn xem báo cáo theo chu kỳ hay realtime.

### 14.6 Fleet and Delivery Operations

- Đội xe nội bộ chiếm tỷ trọng bao nhiêu so với thuê ngoài.
- Có cần quản lý điều phối xe, tài xế và tuyến đường hay không.
- Có cần tích hợp quy trình giao hàng với xác nhận bàn giao hay không.

## 15. Solution Status and Next Steps

### 15.1 Solution Status

Phần giải pháp hiện được giữ ở trạng thái Pending vì chưa đủ thông tin để chốt:

- Quy mô người dùng và tổ chức vận hành.
- Mức độ phức tạp của dữ liệu hiện trạng.
- Ưu tiên phase đầu hoặc MVP.
- Ranh giới giữa core scope và future scope.

### 15.2 Next Steps

Sau khi BRD này được xác nhận, các bước tiếp theo nên là:

1. Chốt các điểm confirmed, pending và out of scope với các stakeholder business liên quan.
2. Xác định module ưu tiên cho phase đầu hoặc MVP.
3. Chuyển sang tài liệu kiến trúc để đề xuất solution options và approach triển khai.
4. Từ kiến trúc đã thống nhất, lập báo giá và timeline chi tiết.

## 16. Conclusion

Theo cách hiểu hiện tại, bài toán của TPCo không phải là một nhu cầu phần mềm rời rạc cho một bộ phận riêng lẻ, mà là bài toán chuẩn hóa và kết nối một chuỗi vận hành nội bộ theo hướng ERP, trong đó đơn hàng đóng vai trò trục chính liên kết các nhóm nghiệp vụ còn lại.

BRD này được cấu trúc theo chuẩn business requirements document quốc tế, với mục đích làm tài liệu xác nhận nghiệp vụ và làm đầu vào cho các bước phân tích giải pháp tiếp theo. Nếu các nội dung trong tài liệu này được xác nhận, phạm vi business của dự án sẽ rõ hơn và đủ cơ sở để sang bước thiết kế giải pháp.
