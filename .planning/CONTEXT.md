# CONTEXT.md — Delivery Assumptions & Risk Assessment

**Last Updated**: 2026-03-28  
**Owner**: Technical Lead  
**Status**: Locked (not for external communication)

---

## 1. Business Context

### 1.1 Customer Profile
- **Company**: TPCo (tên tương ứng trong video quảng cáo)
- **Industry**: Sản xuất cửa thép vân gỗ (steel door, wood-grain coating)
- **Scale**: Vừa (mid-market)
- **Structure**: 
  - Nhà máy sản xuất
  - Đội ngũ sản xuất, phân phối, tư vấn
  - Mạng lưới đại lý
- **Headcount**: 100-200 nhân viên
- **System users**: Est. 30-50 operational users (khảo sát cần xác nhận)

### 1.2 Current Technology Landscape
- **File sharing**: Microsoft OneDrive (at least for some departments)
- **Data & process management**: Chủ yếu Excel
  - Nhập liệu quy trình hằng ngày
  - Báo cáo tổng hợp
- **Microsoft ecosystem adoption**: **BASIC/RISKY ASSUMPTION**
  - Khách có thể chỉ dùng free OneDrive + crack Excel
  - Có thể không có Microsoft 365 business license, không có Azure AD
  - **Decision**: DO NOT assume Microsoft enterprise ecosystem availability
- **HRM system**: Chưa hỏi kỹ — cần bổ sung vào L-CHECKLIST

### 1.3 Geographic & Logistical Context
- **Location**: Phú Thọ
- **Distance from dev team**: ~5-6h by road
- **Implication**: 
  - High cost of on-site visits
  - Training & support must be largely remote
  - UAT & go-live coordination more complex
  - **Decision**: DO NOT mention in client-facing materials; use internally to design remote-first delivery model

---

## 2. Design Decisions (Based on Context)

### D-01: Remote-First Delivery Model
**Decision**: System must be deployable, trainable, and supportable primarily via remote channels.

**Rationale**: 
- Distance makes frequent on-site visits infeasible
- Will minimize travel cost & duration
- Reduces delivery schedule compression

**Impact on architecture**:
- Cloud-hosted solution preferred (vs on-prem requiring on-site setup)
- Self-service UX priority (minimal on-site handholding needed)
- Video training & async documentation over in-person training
- Remote debugging & support tools built into delivery plan

### D-02: No Microsoft Enterprise Lock-in
**Decision**: Do NOT assume Power Platform or Microsoft 365 will be available/affordable.

**Rationale**:
- Customer likely uses free/cracked Microsoft tools only
- Enterprise Microsoft licensing ($12-22/user/month × 30-50 users) probably won't be acceptable
- Reduces scope and potential approval barriers

**Impact on architecture**:
- ~~Power Platform removed from option set~~ (or marked as contingent)
- Focus on open-source alternatives: Odoo Community, ERPNext, custom Python/JS
- If integrating with OneDrive, do so via API at application level (not via Power Platform)

### D-03: Excel as Baseline, Not Constraint
**Decision**: Use Excel proficiency as a training advantage; don't force Excel-identical UI, but ensure learning curve is gentle.

**Rationale**:
- User base is comfortable with Excel row-column model
- Can leverage that familiarity without being locked into spreadsheet paradigm
- Grid-based UI + clear workflow beats "different but better"

**Impact on architecture**:
- Prioritize solutions with intuitive data-entry screens (grid, form, import/export)
- Training should reference Excel concepts ("like Excel pivot tables, but...") for onboarding speed
- Export/import from/to Excel should be seamless for first 6-12 months

### D-04: Manufacturing Domain Fit Required
**Decision**: Selected architecture must have native (or easily customizable) manufacturing module.

**Rationale**:
- Cửa thép vân gỗ production has:
  - BOM management (components, raw materials)
  - Work order tracking (production->QC->warehouse->delivery)
  - Time tracking for work orders (labor cost)
  - Inventory with material types (steel, paint, wood coating)
- Generic ERP without manufacturing defaults = scope creep

**Impact on architecture**:
- Odoo + manufacturing module
- ERPNext + manufacturing module
- Custom ERP must prioritize manufacturing schema from Day 1

---

## 3. Technology Option Evaluation

### Rejected
- **Power Platform**: License cost too high for profile; Microsoft ecosystem not established
- **Pure low-code (no-code platforms)**: Customization ceiling too low for manufacturing complexity; AI support weak
- **ERPNext**: Highcode (not lowcode), team lacks ERPNext ecosystem knowledge, weaker AI support coverage vs Odoo
- **Full Odoo Community monolith**: Good but tightly couples backend to Odoo UI paradigm; harder to customize for TPCo's unique domain

### Selected: Odoo Community (Backend Only) + Custom Frontend Architecture

**Approach**: Use Odoo as backend/database for manufacturing modules, but build a custom frontend application (React/Vue).

**Why this hybrid model**:
1. ✅ **Leverage Odoo's manufacturing strength**: Battle-tested BOM, work orders, inventory, costing — no need to rebuild
2. ✅ **Reduce Odoo dependency**: Frontend is decoupled, can use modern stack (React/Vue)
3. ✅ **Simplified training/UX**: Custom UI tailored to TPCo's workflow, not forced into Odoo's paradigm
4. ✅ **Team comfort**: Python backend + JavaScript frontend; AI support excellent for both
5. ✅ **Headcount 100-200**: Justifies proper backend/frontend separation (not monolith)
6. ✅ **Remote deployment**: Odoo backend cloud-hosted, frontend can be static CDN or Node.js
7. ✅ **Reduce complexity**: Team only needs to know Odoo API + business logic, not entire Odoo codebase

**Architecture breakdown**:

| Layer | Technology | Maintained By | Purpose |
|-------|-----------|-----------------|---------|
| **Backend** | Odoo Community + Python customization | Dev team | Manufacturing modules (BOM, WO, inventory, accounting), business logic, REST API |
| **Database** | PostgreSQL (Odoo-managed) | Odoo | Store manufacturing, inventory, customer, financial data |
| **Frontend** | React/Vue (custom) | Dev team | User-facing UI tailored to TPCo workflows, data entry forms, reporting |
| **Integration** | API layer (Odoo REST) | Dev team | Frontend ↔ Backend communication, OneDrive integration |

**What Odoo provides**:
- Manufacturing module (BOM, work order, production tracking)
- Inventory management (multi-location, stock moves)
- Accounting (journals, suppliers, customers, invoices)
- HR base (employee records; can extend via API)
- API layer (REST) for custom frontend to consume
- Database (PostgreSQL) managed by Odoo

**What we build custom**:
- Frontend UI (React/Vue) tailored to TPCo's workflow
- UX workflows matching how users think (Excel-like grids for data entry, structured forms for orders/WOs)
- OneDrive integration (import/export docs, attach files to orders)
- Reporting dashboard (KPI, production status, delivery tracking)
- Optional Phase 2: Mobile app for warehouse/production floor (React Native or Flutter)

**Training impact**:
- Users learn custom app, not Odoo's web interface
- Admins can access raw Odoo for backend config
- Learning curve reduced vs full Odoo

**Risk & Mitigation**:
- ⚠️ **Risk**: Maintain two systems (Odoo + frontend). **Mitigation**: Clear separation of concerns via API contract; frontend & backend can scale independently
- ⚠️ **Risk**: Integration testing complexity. **Mitigation**: E2E tests covering backend/frontend interactions early in project

### Backup Option
If timeline compresses or budget tightens: **Full Odoo Community** (accept less custom UX, use Odoo web interface directly)

### Not Recommended
- ERPNext (ecosystem, AI support risk)
- Custom ERP from scratch (too long, too risky for mid-market)
- Odoo Enterprise (cost unjustified for this customer profile)

---

## 4. Outstanding Questions for L

### Critical (P1)
1. **HRM current state**: 
   - Có sử dụng phần mềm quản lý nhân sự hay toàn bộ quản lý nhân sự bằng Excel?
   - Có time tracking device (máy chấm công) không?
   - Tính lương & phúc lợi là cách nào?

2. **Manufacturing process**:
   - Quy trình SX cửa thép: những bước chính từ đơn hàng → thành phẩm?
   - Có QC check points?
   - Labor cost tracking: tính theo nhân công, hay theo công đoạn, hay chi phí chung?

3. **Delivery & fleet**:
   - Hiện có quản lý đội xe bằng cách nào?
   - Giao hàng cho đại lý hay trực tiếp end customer?

4. **Excel scope clarification** (from previous discussion):
   - Excel đang được dùng ở đâu: chỉ ban giám đốc, hay cả sale, kế toán, kho, sản xuất?
   - Ngoài Excel, khách có đang dùng phần mềm kế toán, máy chấm công, hoặc công cụ quản lý nào khác không?
   - Excel hiện là nơi nhập liệu vận hành hằng ngày hay chỉ là nơi tổng hợp báo cáo cuối cùng?

### Secondary (P2)
5. **Vendor management & integration**: Có quản lý nhà cung cấp nguyên liệu hay bán hàng thông qua hệ thống nào không?
6. **Financial integration**: Có dùng phần mềm kế toán riêng (Thương mại điện tử/Sage/Kingfisher/VNAccounting) không?
7. **Data volume**: ~Bao nhiêu đơn hàng/tháng? ~Bao nhiêu SKU sản phẩm?

---

## 5. Assumptions Locked

- ✅ **Excel-heavy (not exclusive)**: Customer is Excel-dependent but not exclusively Excel; some departments may have custom tools
- ✅ **No Microsoft enterprise ecosystem**: Power Platform, Azure, Microsoft 365 business licenses are NOT available
- ✅ **Remote-first delivery**: Delivery model must be largely remote (minimize on-site visits, cost savings)
- ✅ **Manufacturing module non-negotiable**: Solution must have native manufacturing support (BOM, work orders, inventory)
- ✅ **Headcount 100-200**: Moderately complex org; justifies backend/frontend separation
- ✅ **System users 30-50**: Estimate based on operational staff; actual TBD from L confirmation
- ✅ **Selected architecture**: Odoo Community (backend) + custom frontend (React/Vue)
- ⏳ **Pending confirmation**: HRM status, time tracking, financial software, manufacturing process detail

---

## 6. Updated Risk Register

| Risk | Severity | Mitigation Strategy |
|------|----------|-------------------|
| **Geographic distance → delivery cost overrun** | High | Remote-first design, async training, cloud hosting |
| **Excel-dependent users → adoption resistance** | High | Gentle learning curve, custom UI matches mental models, Excel import/export, phased rollout |
| **Backend/frontend separation → integration complexity** | Medium | Clear API contract, automated E2E tests, early integration tests |
| **Manufacturing domain → scope creep** | Medium | Lock BOM/work order/labor tracking as MVP; future-phase advanced MFG features |
| **Fragmented IT (OneDrive + separate tools) → integration complexity** | Medium | API-level integrations, data consolidation phase, avoid forcing all-in-one |
| **No ERPNext expertise → hiring/ramp risk** | Low | Not selecting ERPNext; using Odoo (team knows ecosystem) |
| **Khách hàng không có IT staff → training depth risk** | Medium | Super-simple custom UX, video library, post-go-live support budget |
| **Scaling custom frontend → maintenance burden** | Low-Medium | Modular React/Vue architecture, component libs, automated testing from Day 1 |

---

## 7. Next Steps

**Before Architecture Finalization**:
1. Get L to confirm answers to P1 + P2 questions above
2. Validate manufacturing process detail (work order workflow)
3. Confirm budget/timeline constraints from customer
4. Select between Odoo vs ERPNext based on L feedback + team composition
5. Site visit OR detailed video walkthrough of current processes

**After Architecture Selection**:
1. Create ARCHITECTURE.md with option rationale
2. Create PRICING.md with delivery phases, man-hour estimates, travel/infra costs factored in
3. Prepare go/no-go decision points for L

