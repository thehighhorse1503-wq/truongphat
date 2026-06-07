# Phân tích các giải pháp khách đã tham khảo

Tên "Bay" trong trao đổi được xác định là Base.vn. Khách đã thử Base và không duyệt vì Base mạnh ở chia việc nhưng không đáp ứng đủ các nhu cầu lõi ngoài giao việc.

## 1. So sánh nhanh

| Tiêu chí | ECOUNT | Base.vn | MISA AMIS | Cơ hội cho giải pháp đề xuất |
| --- | --- | --- | --- | --- |
| Đơn hàng, kho, sản xuất | Mạnh | Work+ không phải trọng tâm | Mạnh, có bộ Sản xuất - Cung ứng riêng | Bám đúng các ngoại lệ riêng của TPCo |
| Giao việc, quy trình, phê duyệt | Có groupware và approval | Mạnh | Mạnh | Gắn phê duyệt trực tiếp vào dữ liệu đơn hàng |
| Mobile | Có | Có | Có | Tối ưu đúng 3 việc khách cần: lên đơn, duyệt, xem báo cáo |
| Phân quyền | Có theo menu và dữ liệu | Có theo ứng dụng, nhóm và quy trình | Có theo vai trò và ứng dụng | Phân quyền tới phạm vi khách hàng, đơn và phiên bản |
| Lưu vết | Có lịch sử và chức năng khôi phục | Có lịch sử xử lý quy trình | Có lịch sử phê duyệt và dữ liệu nghiệp vụ | Version đơn hàng bất biến, không xóa cứng |
| Tùy chỉnh | Trường, biểu mẫu, menu, báo cáo | Quy trình, biểu mẫu, trường dữ liệu | Quy trình, trường và ứng dụng | Tùy chỉnh sâu công thức và quy tắc riêng của TPCo |
| Google Sheets | Có Excel import/export và API | Có API ở lớp quy trình | Có API và hệ sinh thái tích hợp | Đồng tồn tại trực tiếp với Sheets, không ép thay ngay |
| Khoán sản xuất đặc thù | Cần kiểm chứng | Không phải trọng tâm | Cần kiểm chứng | Tính khoán theo m2, mét dài, đơn, tổ và người |

## 2. ECOUNT

Điểm mạnh được công bố:

- Bao phủ bán hàng, mua hàng, tồn kho, sản xuất, kế toán và groupware.
- Có ứng dụng mobile.
- Có phân quyền theo menu, chức năng và phạm vi dữ liệu.
- Có lịch sử chỉnh sửa, truy vết và khôi phục dữ liệu đã xóa.
- Cho phép tùy chỉnh menu, màn hình nhập và báo cáo.
- Có Excel import/export và Open API.

Rủi ro phù hợp với TPCo:

- Tùy chỉnh chủ yếu trong khung ERP có sẵn; quy trình đặc thù có thể phải thích nghi theo sản phẩm.
- Cần kiểm chứng khả năng quản lý nhiều phiên bản đơn và chỉ định một phiên bản hạch toán.
- Cần kiểm chứng công thức khoán sản xuất theo m2, mét dài, tổ và từng người.
- Trải nghiệm mobile cần kiểm tra bằng đúng thao tác thực tế, không chỉ xác nhận là có app.

Điểm demo cần thắng:

- Ít bước hơn khi tạo và duyệt đơn.
- Luồng sửa đơn và chọn phiên bản hạch toán rõ ràng.
- Báo cáo đúng ngữ cảnh TPCo, không cần ghép nhiều màn hình ERP.

## 3. Base.vn Work+

Điểm mạnh được công bố:

- Mạnh về giao việc, cộng tác, quy trình liên phòng ban và đề xuất/phê duyệt.
- Cho phép thiết kế quy trình, biểu mẫu và trường dữ liệu.
- Có mobile app và thông báo tập trung.
- Phù hợp quản lý công việc văn phòng và ký duyệt.
- Hệ sinh thái Base hiện còn có CRM và Finance, nhưng Work+ vẫn tập trung vào công việc, quy trình và phê duyệt.

Rủi ro phù hợp với TPCo:

- Không phải hệ thống lõi cho đơn hàng, hạch toán, kho và sản xuất.
- Dữ liệu giao việc có thể tách khỏi dữ liệu giao dịch nếu không có lớp tích hợp riêng.
- Version đơn hàng, lập lịch sản xuất và tính khoán cần ứng dụng khác hoặc phát triển bổ sung.
- Tài liệu Base Workflow công bố một số giới hạn cần lưu ý với dữ liệu vận hành lớn: tối đa 30 giai đoạn mỗi quy trình, 1.000 nhiệm vụ hiển thị và báo cáo dựa trên 2.000 công việc mới nhất trong khoảng thời gian chọn.
- Workflow và WeWork vẫn cho phép xóa dữ liệu; tài liệu Base ghi rõ dữ liệu đã xóa không thể khôi phục. Có thể hạn chế quyền và dùng lưu trữ/trạng thái thất bại, nhưng chưa đáp ứng tuyệt đối yêu cầu "không bao giờ xóa cứng".

Lý do khách không duyệt:

- Giải quyết tốt bài toán chia việc.
- Không đáp ứng đủ các bài toán ngoài chia việc: đơn hàng, version, hạch toán, Google Sheets, sản xuất và khoán.

Bài học cần lấy:

- UX giao việc rõ ràng.
- Mobile task flow ngắn.
- Phê duyệt và thông báo dễ hiểu.
- Tổ chức việc theo owner, deadline và trạng thái.

Điểm giải pháp của mình phải hơn Base:

- Đơn hàng là dữ liệu lõi, không chỉ là task.
- Version đơn hàng và bản hạch toán là thiết kế lõi.
- Luồng đơn hàng nối sang sản xuất và tính khoán.
- Google Sheets được kế thừa có kiểm soát trong từng phase.

## 4. MISA AMIS

Điểm mạnh được công bố:

- Mạnh về kế toán và nghiệp vụ tài chính tại Việt Nam.
- Có các ứng dụng bán hàng, kho, công việc, quy trình và phê duyệt.
- Có bộ Sản xuất - Cung ứng riêng.
- Hỗ trợ sản xuất theo đơn hàng (MTO), BOM nhiều cấp và quản lý version BOM.
- Công bố khả năng lập lịch tự động theo đơn, cân bằng năng lực và theo dõi tiến độ realtime.
- Có mobile app, phân quyền và API kết nối hệ thống ngoài.
- AMIS Quy trình cho phép thiết kế luồng, biểu mẫu, phê duyệt và ký số.

Rủi ro phù hợp với TPCo:

- Các năng lực nằm ở nhiều ứng dụng; cần kiểm tra trải nghiệm thực tế xuyên suốt giữa đơn hàng, kế toán, sản xuất và giao việc.
- Version BOM đã được công bố, nhưng version đơn hàng và quy tắc chọn một phiên bản hạch toán vẫn cần kiểm chứng.
- Công thức khoán theo m2, mét dài, tổ và từng người chưa được chứng minh qua tài liệu công khai.
- Cần kiểm tra khả năng cùng vận hành với Google Sheets thay vì yêu cầu chuyển đổi toàn bộ.
- Cần đánh giá tổng chi phí license, triển khai và tùy chỉnh cho số người dùng thực tế.

Điểm demo cần thắng:

- Sửa đơn đã phát hành mà vẫn quản lý rõ phiên bản hạch toán.
- Tích hợp Google Sheets theo từng phase.
- Tính khoán đúng công thức riêng của TPCo.
- Thao tác mobile ngắn hơn trong đúng kịch bản người dùng thực tế.

Kết luận:

- Đây là đối thủ cần benchmark trực tiếp trước khi đầu tư làm demo.
- Nếu MISA xử lý được các ngoại lệ trên bằng cấu hình với chi phí chấp nhận được, lợi thế của giải pháp viết riêng sẽ yếu.
- Nếu không xử lý được, chính các ngoại lệ này là lý do rõ nhất để khách chọn giải pháp tùy chỉnh.

## 5. Định vị giải pháp

Không định vị là một công cụ giao việc giống Base.
Không định vị là một ERP tổng quát nếu chưa chứng minh được quy trình riêng của TPCo.

Định vị phù hợp hơn:

> Hệ thống vận hành lõi cho đơn hàng và sản xuất của TPCo, triển khai từng phần, kế thừa Google Sheets hiện tại và mở rộng bằng Odoo hoặc hệ thống PHP/Node.js tùy mức phù hợp.

Các điểm khác biệt phải chứng minh:

1. Không phá quy trình đang chạy tốt.
2. Mobile-first cho thao tác ngắn và thường xuyên.
3. Phân quyền theo đúng vai trò và phạm vi dữ liệu.
4. Version hóa đơn hàng và audit trail là thiết kế lõi.
5. Đơn hàng nối trực tiếp sang duyệt, lịch sản xuất, tiến độ và khoán.
6. Cho phép triển khai theo phase nhưng dùng chung dữ liệu và lịch sử.

Hướng cung cấp khả thi:

- Odoo nếu cần tận dụng năng lực ERP, kho, kế toán, sản xuất và API.
- PHP/Node.js nếu quy trình riêng, mobile UX, version đơn hàng và khoán sản xuất quan trọng hơn việc dùng ERP sẵn.
- Hybrid nếu Odoo làm backend nghiệp vụ chuẩn, còn PHP/Node.js làm lớp workflow/mobile/custom logic riêng.

Không dùng các điểm sau làm thông điệp khác biệt vì đối thủ đều đã có:

- Mobile app.
- Phân quyền.
- Phê duyệt online.
- Báo cáo realtime.
- Workflow tùy chỉnh.
- API tích hợp.

## 6. Kịch bản demo đề xuất

1. Sale tạo đơn trên điện thoại.
2. Người có thẩm quyền duyệt hoặc từ chối, hệ thống lưu lý do và lịch sử.
3. Sale sửa đơn đã phát hành; hệ thống tạo phiên bản mới, không ghi đè.
4. Kế toán chọn phiên bản được hạch toán.
5. Đơn được duyệt xuất hiện trong danh sách chờ sản xuất, có khối lượng và ngày giao.
6. Dashboard hiển thị trạng thái đơn, người phụ trách và lịch sử thay đổi.

Demo nên có thêm một màn hình hoặc prototype thể hiện hướng phase 2:

- Tổ trưởng báo cáo sản lượng cuối ngày.
- Hệ thống bóc tách theo đơn vị m2 hoặc mét dài.
- Tính hiệu suất và tiền khoán theo tổ hoặc người.

## 7. Các câu hỏi phải kiểm chứng bằng dữ liệu mẫu

- Cấu trúc và trạng thái của một đơn hàng.
- Khi nào đơn được coi là đã phát hành.
- Những trường nào được phép sửa sau phát hành.
- Quy tắc chọn phiên bản hạch toán.
- Vai trò nào được tạo, sửa, duyệt và hạch toán.
- Công thức lập lịch sản xuất.
- Công thức khoán và phân bổ tiền.
- Cách Google Sheets hiện liên kết dữ liệu giữa các bộ phận.
- Dữ liệu nào tiếp tục ở Google Sheets trong từng phase.
- Tích hợp Google Sheets cần một chiều hay hai chiều, và dữ liệu nào là nguồn chính.

## 8. Checklist benchmark sản phẩm

Chạy cùng một kịch bản trên ECOUNT và MISA AMIS nếu có tài khoản demo. Base không cần pilot lại; chỉ dùng làm benchmark UX giao việc.

1. Tạo đơn trên điện thoại.
2. Duyệt đơn trên điện thoại.
3. Sửa đơn sau duyệt và giữ cả hai phiên bản.
4. Chọn một phiên bản để hạch toán.
5. Đẩy đơn được chọn sang lịch sản xuất.
6. Báo cáo sản lượng theo đơn, tổ và người.
7. Tính khoán theo m2 và mét dài.
8. Trao đổi dữ liệu với Google Sheets theo chiều cần thiết.

Ghi lại:

- Số bước thao tác.
- Phần làm được bằng cấu hình.
- Phần cần viết thêm.
- Giới hạn phân quyền và audit.
- Chi phí license, triển khai và tùy chỉnh.

## 9. Áp lực thương mại

Giá công khai chỉ dùng làm mốc tham khảo, cần lấy báo giá chính thức:

- ECOUNT ERP: khoảng 1 triệu đồng/tháng, không giới hạn người dùng ERP; Groupware tính riêng sau số tài khoản miễn phí.
- Base Workflow: các gói công khai khoảng 1,2-2,4 triệu đồng/tháng tùy số tài khoản.
- MISA AMIS Sản xuất: trang giá công bố 150 triệu đồng/năm cho tối đa 10 người dùng; người dùng bổ sung và dịch vụ triển khai tính riêng.

Giải pháp viết riêng phải chứng minh giá trị lớn hơn chênh lệch tổng chi phí sở hữu, không chỉ khác giao diện.

## 10. Nguồn tham khảo chính thức

- ECOUNT: https://www.ecount.com/vn/
- ECOUNT tùy chỉnh hệ thống: https://www.ecount.com/vn/ecount/product/erp_tuy-chinh-he-thong-erp
- ECOUNT mobile: https://www.ecount.com/vn/ecount/product/erp_app-tren-dien-thoai
- ECOUNT Open API: https://www.ecount.com/vn/ecount/product/erp_open-api
- ECOUNT lịch sử dữ liệu: https://www.ecount.com/vn/ecount/product/erp_kiem-tra-luoc-su-du-lieu
- ECOUNT phân quyền: https://www.ecount.com/vn/ecount/product/erp_quan-ly-tai-khoan-nguoi-dung
- ECOUNT bảng giá: https://www.ecount.com/vn/ecount/join/bang-gia
- Base.vn Work+: https://base.vn/platform/work
- Base.vn WeWork: https://base.vn/wework
- Base.vn Workflow: https://base.vn/workflow/help
- Base.vn giới hạn Workflow: https://help.base.vn/support/solutions/articles/63000253494-base-workflow-c%C3%A1c-con-s%E1%BB%91-gi%E1%BB%9Bi-h%E1%BA%A1n-gi%E1%BB%9Bi-h%E1%BA%A1n-trong-workflow-
- Base.vn Request: https://help.base.vn/support/solutions/articles/63000284976-base-request-introduce-base-request-and-table-of-contents
- MISA AMIS Công việc: https://amis.misa.vn/amis-cong-viec/
- MISA AMIS Quy trình: https://amis.misa.vn/amis-quy-trinh/
- MISA AMIS Kế toán: https://amis.misa.vn/amis-ke-toan/
- MISA AMIS Sản xuất - Cung ứng: https://amis.misa.vn/amis-san-xuat-cung-ung/
- Giá MISA AMIS Sản xuất: https://amis.misa.vn/250037/gia-phan-mem-quan-ly-san-xuat-misa-amis/
