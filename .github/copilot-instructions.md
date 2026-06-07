# Hướng dẫn Copilot cho dự án TPCo ERP

## Bối cảnh Dự án

**Loại dự án:** Pre-sale (Phân tích & Đề xuất)  
**Khách hàng:** TPCo (Công ty sản xuất, quy mô chưa xác định)  
**Account Manager:** L (Cựu CTO, nắm rõ bối cảnh khách hàng)  
**Đội phát triển:** Chúng ta  

### Mục tiêu Phase Pre-sale

1. **Phân tích nhu cầu** từ diagram trong `truongphat.drawio` (ngoại trừ sheet "nháp")
2. **Đề xuất kiến trúc giải pháp** kỹ thuật phù hợp với bối cảnh Việt Nam
3. **Chuẩn bị bảng báo giá** chi tiết

---

## Tài liệu Chính

### `truongphat.drawio`

Cấu trúc diagrams hiện tại:

- **Sheet 1: Hình Dung tổng quan**  
  Hệ thống với 6 modules chính:
  - CRM (Quản lý khách hàng)
  - HRM (Quản lý nhân sự)
  - Hệ thống đặt hàng
  - Quản lý sản phẩm (với metadata: mã hàng, loại, vật liệu sắt/thép/tôn/sơn)
  - Báo cáo tổng hợp (lãi/chi phí/vật liệu/tổ sản xuất/hiệu suất)
  - Quản lý đội xe (xe ngoài, xe nhà máy, lái xe, chuyến đi, bảo trì)

- **Sheet 2: Sơ đồ cơ cấu**  
  Cấu trúc tổ chức (chưa hoàn chỉnh trong file)

- **Sheets khác:** Bỏ qua các sheet có chữ "nháp"

---

## Workflow Pre-sale

### Phase 1: Phân tích Nhu cầu  
- Phân tích từng module trong diagram
- Xác định core features & scope
- Liên hệ L nếu có câu hỏi về TPCo

### Phase 2: Đề xuất Kiến trúc  
- Lựa chọn tech stack (backend/frontend/database)
- Xác định integration points giữa modules
- Xem xét bối cảnh: VN-based users, multi-language support, offline-capable?

### Phase 3: Báo Giá  
- Tính t/c phát triển theo modules
- Thêm budget cho testing, deployment, training
- Chuẩn bị proposal document

---

## Quy tắc & Convention

### Naming & Language

- **Tài liệu nội bộ:** Tiếng Việt (ease of communication with VN stakeholders)
- **Code comments & documentation:** Tiếng Anh (standard practice)
- **Proposal & Pricing:** Tiếng Việt (for TPCo)

### File Structure

```
.github/
  copilot-instructions.md  (file này)
.planning/
  REQUIREMENTS.md          (phân tích nhu cầu chi tiết)
  ARCHITECTURE.md          (kiến trúc giải pháp đề xuất)
  PRICING.md               (báo giá & timeline)
truongphat.drawio          (tài liệu chính từ khách)
```

### Communication Checkpoints

1. **Với L:** Xác nhận architecture & scope trước phase 3
2. **Với bộ phát triển nội bộ:** Daily sync trên progress
3. **Output:** PDF proposal document cho TPCo

---

## Quy tắc Tạo & Cập nhập Tài liệu

**IMPORTANT:** Khi tạo hoặc cập nhập bất kỳ tài liệu nào trong dự án, Copilot PHẢI xác nhận với user điểm sau TRƯỚC khi bắt tay vào viết:

### 1. Xác nhận Audience (Người đọc)

Hỏi hoặc xác nhận rõ:

- **Ai sẽ đọc tài liệu này?**
  - Chỉ dùng nội bộ đội dev?
  - Dùng để trình L hoặc chủ khách?
  - Dùng để submit cho TPCo?
  - Dùng chung cho nhiều audiences?

- **Hệ quả của xác nhận:**
  - Nếu tài liệu cho L (account): Cần rõ ràng, không mơ hồ, focus vào xác nhận bài toán.
  - Nếu tài liệu cho TPCo: Cần chuyên nghiệp, trở sáng, bao quát, tự khúc tích (stand-alone).
  - Nếu tài liệu nội bộ: Có thể ngắn gọn hơn, focus vào action items.

### 2. Xác nhận Giọng văn (Tone & Style)

Hỏi hoặc xác nhận rõ:

- **Giọng văn nên như thế nào?**
  - Chính thức (formal) hay thân thiện (informal)?
  - Ngôn ngữ: Tiếng Việt hay tiếng Anh?
  - Mức độ chi tiết: Sâu / cân bằng / tóm lược?
  - Cần có bố cục chuẩn như BRD / RFP / Proposal hay tự do?

- **Hệ quả của xác nhận:**
  - Giọng xác nhận bài toán với L ≠ giọng proposal cho khách.
  - Giọng nội bộ có thể dùng kiểu checklist ≠ giọng hình thức.

### 3. Cách thực hiện Xác nhận

- **Lý tưởng:** User chủ động nói rõ khi yêu cầu tài liệu.
  - Ví dụ: "Tạo BRD để trình L, focus vào xác nhận bài toán, tone chuyên nghiệp".
  
- **Nếu user không nói rõ:** Copilot phải hỏi lại TRƯỚC khi bắt tay viết.
  - Ví dụ: "Tôi sắp tạo ARCHITECTURE.md. Tài liệu này dùng để:
    - Trình L và xin input kiến trúc? hay
    - Dùng làm proposal cho TPCo? hay  
    - Dùng nội bộ để plan development?
    
    Vui lòng xác nhận để tôi chọn tone và cấu trúc phù hợp."

### 4. Dictionary Tone & Audience Tiêu chuẩn

Để tiện xác nhận, dưới đây là các kết hợp phổ biến trong dự án này:

| Tài liệu | Audience | Tone | Ngôn ngữ | Note |
|---|---|---|---|---|
| REQUIREMENTS.md | Dev team nội bộ | Cân bằng, xác nhận bài toán | Tiếng Việt | Để plan design & architecture |
| BRD.md | Anh L + Dev team | Chuyên nghiệp, rõ ràng | Tiếng Việt | Xác nhận business bài toán trước solution |
| L-CHECKLIST.md | Làm việc trực tiếp với L | Hỏi đáp, checklist | Tiếng Việt | Check nhanh lại scope, không quá formal |
| ARCHITECTURE.md | Dev lead + có thể trình L sau | Kỹ thuật, cân bằng chi tiết | Tiếng Việt/ Anh | Design & decision record |
| PRICING.md | Trình TPCo (qua L) | Chính thức, detail, business-focused | Tiếng Việt | Báo giá chuyên nghiệp |
| Meeting Notes | Dev team + L | Ngắn gọn, action items | Tiếng Việt | Ghi biên bản, dễ tra cứu |

---

## Hướng dẫn cho Copilot Agents

### Khi phân tích nhu cầu (gsd-discuss-phase)
- Tập trung vào 6 modules chính, bỏ qua "nháp"
- Hỏi về scalability, user count, current IT infrastructure của TPCo
- Xác định MVP scope  vs. future phases

### Khi phân tích codebase  
- Hiện này chủ yếu là diagram + documentation phase
- Không có code repository chính thức
- Sẽ phát triển tech stack proposal dựa trên nhu cầu

### Khi tạo proposal
- Đảm bảo bảng báo giá rõ ràng, tách từng module
- Bao gồm timeline estimate (effort), risk, assumptions  
- Định dạng: Markdown + có thể export PDF

---

## Liên hệ & Escalation

- **Account Manager (L):** Tiếp cận khi cần thông tin từ khách, hoặc xác nhận scope
- **Technical Lead:** Chịu trách nhiệm finalize architecture proposal
- **Pricing / Sales:** Người chịu trách nhiệm final proposal document

---

## Next Steps

1. Analyze `truongphat.drawio` → create `REQUIREMENTS.md`
2. Based on requirements, propose tech stack & architecture → create `ARCHITECTURE.md`
3. Build pricing model → create `PRICING.md`
4. Review with L before finalizing proposal
