# L-CHECKLIST.md

## 1. Mục đích tài liệu

Checklist này được tách ra từ BRD để dùng trực tiếp khi làm việc với anh L.

Mục tiêu:

- Xác nhận lại rằng đội phát triển đang hiểu đúng bài toán của TPCo.
- Chốt các giả định nghiệp vụ đang còn mơ hồ.
- Thu thập đủ thông tin để chuyển sang phase đề xuất giải pháp và kiến trúc.

## 2. Cách sử dụng

- Dùng checklist này trong buổi trao đổi với L.
- Với mỗi câu hỏi, cố gắng ghi luôn câu trả lời ngắn gọn ngay bên dưới hoặc ngay trong cột `Ghi nhận`.
- Nếu L chưa có câu trả lời ngay, đánh dấu `Cần hỏi lại khách`.
- Ưu tiên đi hết nhóm `P1` trước vì đây là phần ảnh hưởng trực tiếp đến scope, kiến trúc và báo giá.

## 3. Xác nhận nhanh về bức tranh tổng thể

### 3.1 Điều chúng ta đang hiểu

Đề nghị xác nhận với L các ý sau:

- TPCo là doanh nghiệp sản xuất và bài toán chính là quản lý xuyên suốt từ khách hàng đến giao hàng.
- Hệ thống cần bao quát 6 module chính: CRM, HRM, đặt hàng sản xuất, quản lý sản phẩm, báo cáo tổng hợp, quản lý đội xe.
- Quy trình đặt hàng có liên quan trực tiếp đến công nợ, đặt cọc hoặc ký quỹ trước khi vào sản xuất.
- Sản xuất đang vận hành theo đơn hàng hoặc phần lớn theo đơn hàng.
- Dữ liệu vật liệu sản phẩm là đầu vào quan trọng để tính giá thành, vật liệu và lợi nhuận.

### 3.2 Kết quả cần ghi nhận

- Ý nào đúng hoàn toàn.
- Ý nào đúng một phần.
- Ý nào đang hiểu sai và cần sửa lại BRD.

## 4. Checklist câu hỏi làm việc với L

## 4.1 Nhóm P1: Ảnh hưởng trực tiếp đến scope và giải pháp

| ID | Chủ đề | Câu hỏi | Lý do cần hỏi | Ghi nhận |
|---|---|---|---|---|
| P1-01 | Quy mô | TPCo hiện có khoảng bao nhiêu người dùng sẽ tham gia hệ thống? | Ảnh hưởng phạm vi người dùng, phân quyền, hạ tầng | |
| P1-02 | Tổ chức | Có bao nhiêu phòng ban, xưởng, kho, chi nhánh hoặc điểm vận hành? | Ảnh hưởng cấu trúc dữ liệu và mô hình triển khai | |
| P1-03 | Phạm vi phase đầu | Khách đang muốn làm toàn bộ 6 module hay ưu tiên một số module trước? | Ảnh hưởng MVP, roadmap và báo giá | |
| P1-04 | Mức độ ưu tiên | Nếu phải chọn phase 1, 3 module quan trọng nhất là gì? | Giúp chốt phạm vi triển khai ban đầu | |
| P1-05 | Kênh phân phối | Mô hình hiện tại là nhà phân phối -> đại lý, hay có nhiều cấp hơn? | Ảnh hưởng thiết kế CRM, khách hàng, đơn hàng | |
| P1-06 | Đặt hàng | Khách hoặc đại lý có thật sự tự đặt hàng trên hệ thống không, hay hiện chủ yếu gọi Sale Admin? | Ảnh hưởng thiết kế user portal và nghiệp vụ order | |
| P1-07 | Công nợ | Quy tắc kiểm soát công nợ, ký quỹ hoặc đặt cọc hiện tại là gì? | Ảnh hưởng luồng duyệt đơn và điều kiện vào sản xuất | |
| P1-08 | Nợ xấu | Blacklist hoặc nợ xấu hiện được kiểm soát như thế nào và ai là người duyệt ngoại lệ? | Ảnh hưởng workflow nghiệp vụ | |
| P1-09 | Sản xuất | Một đơn hàng đi qua bao nhiêu công đoạn sản xuất chính? | Ảnh hưởng mô hình workflow sản xuất | |
| P1-10 | Kho | Quy trình từ hoàn thành sản xuất đến nhập kho và xuất kho hiện đang vận hành như thế nào? | Ảnh hưởng tích hợp order, kho, vận chuyển | |
| P1-11 | Dữ liệu hiện trạng | Dữ liệu hiện đang nằm ở Excel, phần mềm kế toán, phần mềm chấm công, hay công cụ nào khác? | Ảnh hưởng kế hoạch migration và tích hợp | |
| P1-12 | Hạ tầng | Khách có yêu cầu on-premise, cloud, hay chưa có định hướng? | Ảnh hưởng kiến trúc tổng thể | |
| P1-13 | Timeline | Khách có deadline kinh doanh hoặc mốc thời gian mong muốn không? | Ảnh hưởng cách chia phase và báo giá | |
| P1-14 | Ngân sách | Có khung ngân sách sơ bộ hoặc mức đầu tư kỳ vọng không? | Ảnh hưởng cách đề xuất solution | |

## 4.2 Nhóm P2: Ảnh hưởng đến chi tiết nghiệp vụ từng module

| ID | Chủ đề | Câu hỏi | Lý do cần hỏi | Ghi nhận |
|---|---|---|---|---|
| P2-01 | CRM | Sale Admin có chỉ được xem khách của mình hay có trường hợp xem chéo? | Ảnh hưởng phân quyền dữ liệu | |
| P2-02 | CRM | Có cần nhắc lịch chăm sóc, pipeline khách hàng, hoặc chỉ cần lưu lịch sử chăm sóc? | Xác định độ sâu module CRM | |
| P2-03 | CRM | Có cần đại lý tự xem công nợ và đơn hàng không? | Ảnh hưởng cổng self-service | |
| P2-04 | CRM | Có quan tâm AI tóm tắt cuộc gọi hay đây chỉ là ý tưởng tham khảo? | Tách core scope và future scope | |
| P2-05 | HRM | Máy chấm công FaceID đang dùng của hãng nào và có thể tích hợp trực tiếp không? | Ảnh hưởng tích hợp HRM | |
| P2-06 | HRM | Công thức tính lương thưởng có cố định hay thay đổi theo tổ, vai trò, hoặc thời điểm? | Ảnh hưởng độ phức tạp payroll | |
| P2-07 | HRM | Nhân viên có cần tự xem công, phép, bảng lương không? | Xác định self-service HRM | |
| P2-08 | HRM | Quy trình xác nhận hiệu suất và chia thưởng hiện tại diễn ra thế nào? | Ảnh hưởng workflow HRM | |
| P2-09 | Sản phẩm | Dữ liệu sản phẩm hiện đang quản lý ở đâu và ai chịu trách nhiệm cập nhật? | Xác định owner dữ liệu master | |
| P2-10 | Sản phẩm | Có cần quản lý BOM nhiều cấp hay chỉ cần định mức vật liệu tổng? | Ảnh hưởng dữ liệu sản phẩm và giá thành | |
| P2-11 | Sản phẩm | Có nhiều biến thể sản phẩm theo kích thước, màu, quy cách không? | Ảnh hưởng cấu trúc catalog | |
| P2-12 | Báo cáo | Những báo cáo nào bắt buộc phải có ngay ở phase đầu? | Chốt MVP reporting | |
| P2-13 | Báo cáo | Lợi nhuận cần tính theo biên gộp hay tính đủ nhiều lớp chi phí? | Ảnh hưởng dữ liệu cost model | |
| P2-14 | Báo cáo | Ban giám đốc muốn dashboard realtime hay báo cáo định kỳ là đủ? | Ảnh hưởng kiến trúc dữ liệu và hạ tầng | |
| P2-15 | Đội xe | Tỷ trọng xe nhà máy và xe thuê ngoài hiện nay là bao nhiêu? | Ảnh hưởng độ sâu module fleet | |
| P2-16 | Đội xe | Có cần điều xe, phân tuyến, lịch xe, hoặc mobile app cho tài xế không? | Xác định scope vận hành đội xe | |
| P2-17 | Đội xe | Có cần quản lý đăng kiểm, bảo hiểm, hạn bảo dưỡng định kỳ không? | Xác định mức độ asset management | |

## 4.3 Nhóm P3: Định hướng tương lai và cơ hội mở rộng

| ID | Chủ đề | Câu hỏi | Lý do cần hỏi | Ghi nhận |
|---|---|---|---|---|
| P3-01 | Mở rộng | Module quản lý công việc hoặc project nội bộ có phải nhu cầu thật không, hay chỉ là ý tưởng thêm? | Xác định backlog phase sau | |
| P3-02 | Mở rộng | Khách có nhu cầu app mobile cho sale, tài xế, hoặc quản lý không? | Xác định hướng phát triển dài hạn | |
| P3-03 | Mở rộng | Có nhu cầu tích hợp phần mềm kế toán, máy chấm công, Zalo, hoặc tổng đài không? | Xác định nhu cầu tích hợp tương lai | |

## 5. Danh sách xác nhận theo từng module

## 5.1 CRM

Đề nghị xác nhận:

- Có đúng là CRM hiện cần tập trung vào khách hàng, lịch sử chăm sóc, công nợ, ký quỹ và đơn hàng liên quan.
- Có đúng là công nợ cần gắn về đúng đơn hàng, không xử lý cứng theo FIFO.
- Có đúng là Sale Admin cần bị giới hạn phạm vi dữ liệu theo tệp khách phụ trách.

## 5.2 HRM

Đề nghị xác nhận:

- Có đúng là phase đầu HRM chủ yếu xoay quanh chấm công, phép, hiệu suất và lương thưởng.
- Có đúng là hiệu suất tổ sản xuất là dữ liệu quan trọng để tính thưởng hoặc đánh giá.
- Có đúng là hiện còn có bước nhập liệu từ Excel hoặc thao tác tay.

## 5.3 Hệ thống đặt hàng sản xuất

Đề nghị xác nhận:

- Có đúng là đây là trục nghiệp vụ quan trọng nhất của toàn hệ thống.
- Có đúng là luồng chuẩn là nhận đơn -> kiểm tra công nợ hoặc cọc -> duyệt -> sản xuất -> nhập kho -> thanh toán -> giao hàng.
- Có đúng là hệ thống cần kiểm soát rõ các trạng thái và trách nhiệm từng bước.

## 5.4 Quản lý sản phẩm

Đề nghị xác nhận:

- Có đúng là dữ liệu vật liệu theo sản phẩm là một yêu cầu cốt lõi.
- Có đúng là một số trường hợp cần điều chỉnh chi phí vật liệu theo từng đơn hàng.
- Có đúng là trạng thái sản phẩm cần hỗ trợ mở hoặc dừng sản xuất.

## 5.5 Báo cáo tổng hợp

Đề nghị xác nhận:

- Có đúng là báo cáo lãi, chi phí theo đơn, vật liệu kho, sản phẩm và hiệu suất là nhóm báo cáo cốt lõi.
- Có đúng là lãnh đạo cần nhìn dữ liệu theo khách, sản phẩm, tổ sản xuất hoặc đại lý.

## 5.6 Quản lý đội xe

Đề nghị xác nhận:

- Có đúng là đội xe chủ yếu phục vụ vận chuyển hàng từ kho đến đại lý hoặc nhà phân phối.
- Có đúng là cần quản lý ít nhất xe, lái xe, chuyến xe, bảo trì và chi phí chuyến.

## 6. Kết quả đầu ra mong muốn sau buổi làm việc với L

Sau buổi làm việc, tối thiểu cần chốt được:

- Core scope thực sự của phase đầu.
- Mức độ ưu tiên giữa 6 module.
- Các điểm hiểu đúng và hiểu sai trong BRD.
- Những dữ liệu hoặc tài liệu cần L xin thêm từ khách.
- Những phần nào có thể đưa sang phase solution ngay.

## 7. Hành động sau khi có phản hồi từ L

- Cập nhật lại `BRD.md` theo nội dung đã được xác nhận.
- Chia rõ phần `Confirmed`, `Need further clarification`, `Out of scope for phase 1`.
- Từ đó mới chuyển sang tài liệu kiến trúc và báo giá.
