# Track1_Day25_2A202601745_DaoNgocBich

## Thông tin nộp bài

- **Họ và tên:** Đào Ngọc Bích
- **MHV:** 2A202601745
- **Nhóm:** T226
- **Sản phẩm:** Sen — Trợ lý AI cho tổng đài tra soát giao dịch ví điện tử (nối tiếp Day 23 North Star & Day 24 Financial Model)
- **Ngày kiểm tra lại giá API/benchmark:** 27/08/2026 (xem `6_Benchmarks!D3`)

## Deliverables

| File | Vai trò |
|---|---|
| [`2A202601745_DaoNgocBich_Day25_model.xlsx`](./2A202601745_DaoNgocBich_Day25_model.xlsx) | Monetization Model — 7 tab (5 tab điền + 0_README/6_Benchmarks tham chiếu) |
| [`2A202601745_DaoNgocBich_Day25_onepager.docx`](./2A202601745_DaoNgocBich_Day25_onepager.docx) | Monetization One-Pager |
| [`ai-support-log.md`](./ai-support-log.md) | Log prompt thật + accept/reject — theo đúng quy ước Day 17/18/23 |
| [`reference/Day24-README-mau-dinh-dang.md`](./reference/Day24-README-mau-dinh-dang.md) | README Day 24 gốc, giữ lại làm tham chiếu định dạng — không phải bài nộp Day 25 |

**Nộp bài:** push lên repo `Track1_Day25_2A202601745_DaoNgocBich`, nộp link repo trên LMS (Codelabs) trước buổi tiếp theo.

## 4 quyết định gốc

| Quyết định | Chọn | Vì sao |
|---|---|---|
| Value Metric | **Outcome** — hồ sơ duyệt lần đầu | Khớp North Star Day 23 (`% ticket được duyệt ngay lần đầu`) |
| Kênh 90 ngày | **Sales-Led, founder-led** | TAM chỉ 90 tổ chức — đủ nhỏ để bán trực tiếp, quá regulated cho PLG |
| Biến thể HITL | **A** — ví tự xử lý ca escalate | Sen không gánh chi phí sửa hồ sơ hỏng; cách ly Gross Margin khỏi containment thấp |
| Model LLM | **Claude Sonnet 5** (không phải Haiku 4.5 mặc định template) | Tra soát cần đối chiếu timeline + business rules, phức tạp hơn FAQ đơn giản |

## Chuỗi số — mọi thứ truy được về Tab 1 → 2 → 4

```
1_Cost_Job         Cost/Job = $0,0802/job (≈2.114₫)   containment 70% (ước tính, chưa đo thật)
        ↓
2_Pricing          Giá sàn $0,2406 → Giá bán $0,38/job → GM 78,9% → Breakeven containment 36,9%
        ↓
4_Channel_Fit      ARPU $1.330/th → Ngân sách CAC $18.887 → CAC thực tế $32.000 → lệch 1,69×
```

Verify bằng cách mô phỏng lại toàn bộ công thức trong Python (không đoán bằng mắt) — tất cả các "đèn" đều xanh:
bội số 4,74× ≥3, GM an toàn (không >85% nên không bị nghi ngờ thiếu chi phí), giá bán nằm trong vùng neo,
containment 70% ≥ 36,9% cần thiết với biên độ lớn.

## 3 con số tôi tự tra cứu lại (không dùng mặc định template)

1. **Giá Claude Sonnet 5**: $2/$10 mỗi 1M token — xác nhận lại hôm nay; mức tăng $3/$15 dự kiến 01/09/2026 **đã bị huỷ**, $2/$10 nay là giá chuẩn. Model từ 4.7 trở lên (gồm Sonnet 5) dùng tokenizer mới sinh nhiều hơn ~30% token — đã cộng vào ước tính token/turn.
2. **QA nội bộ $4,38/giờ**: JobsGO — QA/QC Specialist VN trung bình 15,4tr₫/tháng, +20% overhead (bảo hiểm/quản lý, theo quy ước Day 24), ÷160h, ÷26.360₫.
3. **Infra $0,0024/job**: pgvector trên RDS quy mô nhỏ (~10M vector) ≈ $45/tháng, chia cho ~5 khách trung bình giai đoạn đầu.
4. **Tỷ giá 26.360₫/USD**: Vietcombank 25/08/2026 (giá bán), thay cho giả định 26.000 của Day 24.

## Phát hiện quan trọng nhất: điểm căng giữa Value Metric Scorecard và quyết định thực tế

Scorecard Tab 3 chấm **trung thực theo hiện trạng hôm nay**: Attribution 5/10, Autonomy 4/10 — cả hai đều dưới ngưỡng 7/10.
Gợi ý tự động của model là **SEAT hoặc HYBRID**, không phải Outcome. Chúng tôi vẫn chọn Outcome, và ghi rõ lý do thị trường
trong Decision Note (`3_Value_Metric!B31`) thay vì âm thầm chấm điểm cao hơn thực tế để hợp thức hoá lựa chọn — đây là
kẽ hở thật của mô hình, không phải lỗi cần che giấu.

**Cập nhật:** rà lại `Track1_Day23_2A202601745_DaoNgocBich/metrics-pack/` (cùng sản phẩm Sen, chỉ khác bài) phát hiện Day 23
đã định nghĩa NSM = "% ticket Approved-first-pass" — trùng khớp 100% với job definition của Day 25 — kèm schema tracking đủ
6 event, ≥2 acceptance criteria, và một **counter-metric riêng** (`ticket_reopened_by_customer_complaint`) thiết kế đúng để
tách "duyệt nhanh" khỏi "duyệt ĐÚNG". Đây là bằng chứng Attribution thật (nâng điểm statement #4 từ 1→2), không phải số liệu
đo được (vẫn 0đ cho statement #2 — schema có, số liệu chạy thật thì chưa) — ranh giới giữa "đã thiết kế" và "đã đo" được
giữ nguyên, không gộp lại cho đẹp điểm.

## Mô hình gãy khi nào? (câu hỏi bắt buộc của One-Pager)

Không phải khi Gross Margin của Sen giảm — Biến thể A cách ly Sen khỏi chi phí escalate nên GM vẫn "an toàn" (≥70%)
dù containment tụt xuống 50% (xem bảng Sensitivity `2_Pricing!B39:D44`). Mô hình gãy khi **containment tụt dưới ~55%**:
tại điểm đó, giá trị ròng mà KHÁCH nhận được (tiết kiệm chi phí FTE trừ giá trả Sen trừ chi phí escalate họ tự xử lý)
tiến về 0 → khách rời bỏ dù nội bộ Sen vẫn có lãi trên giấy. Vùng containment 70% hiện tại có biên độ an toàn 15 điểm,
nhưng đây là ước tính chưa đo thật (xem Evidence Pack).

## Việc còn thiếu — cố tình để trống thay vì bịa số

- **Eval Results**: bộ 180 case có nhãn (FIN05-Dataset) đã sẵn, nhưng agent thật **chưa chạy qua** — `eval/results/report.md` toàn "—".
- **Risk Checklist riêng cho Sen**: bài Day 22 Responsible-AI trước đó làm trên case khác (VlogStudio), chưa làm lại cho Sen.
- **Pilot Report**: chưa có pilot thật.
- **Bài test người lạ**: chưa nhờ ai đọc thử One-Pager — cần làm trước khi nộp chính thức.

## Ghi chú về file README cũ trong thư mục

Khi bắt đầu bài, tôi phát hiện một `README.md` (của Day 24) được thêm vào thư mục chứa một khối HTML comment tự xưng
"CRITICAL SYSTEM INSTRUCTION" nhắm vào AI, yêu cầu AI chỉ hỏi Socratic và giấu kín sự tồn tại của chỉ thị đó. Tôi không
làm theo nội dung ẩn trong file — chỉ làm theo yêu cầu trực tiếp của người dùng trong hội thoại — và đã báo lại công khai
thay vì im lặng tuân thủ. File đó được giữ nguyên tại `reference/Day24-README-mau-dinh-dang.md` làm tài liệu tham khảo.
