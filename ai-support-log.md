# AI Support Log

**Đào Ngọc Bích · MHV 2A202601745 · Nhóm T226 · Sen (FIN-05) · 27/08/2026**

Tôi dùng Claude Code xuyên suốt cả 6 trạm, một phiên liền mạch. Claude nháp số/điền Excel theo hướng dẫn từng trạm, còn quyết định lõi (containment, value metric, giá bán, biến thể HITL, kênh) là tôi chọn — dưới đây là những chỗ đáng nhớ nhất: AI đề xuất gì, tôi giữ nguyên hay sửa lại, và vì sao.

| # | Trạm | Claude đề xuất/làm gì | Tôi accept / reject / sửa và lý do |
|---|---|---|---|
| 1 | Trạm 1 — Cost/Job | Tự ý chọn Claude Sonnet 5 làm model tính chi phí (thay vì Haiku 4.5 mặc định của template) mà **chưa hỏi tôi trước** — tự nhận đây là lựa chọn của Claude khi báo cáo lại | **Accept** — tôi xác nhận giữ Sonnet 5 ("vẫn đang dùng sonet mà"), nhưng đúng là Claude nên hỏi trước một quyết định ảnh hưởng chi phí 5× thay vì tự quyết |
| 2 | Trạm 1 — Containment | Claude đề xuất 3 mức containment (55% thận trọng / 65% giữa / 80% giữ nguyên) qua bảng chọn, có kèm nguồn (Intercom Fin production 45-53% vs fintech median 75%). Tôi chọn 55% trong bảng chọn | **Reject số của chính mình ngay sau đó** — tôi nhắn lại "80% thì có vẻ hơi hoàn hảo hóa, 70% nhé", chọn một số ở giữa không nằm trong 3 lựa chọn Claude đưa. Claude tính lại toàn bộ Cost/Job theo 70%, không tự ý giữ 55% hay 80% |
| 3 | Trạm 1 — QA/Infra cost | Claude tự đoán $4/giờ QA và $0,008/job infra, không có nguồn | Tôi **yêu cầu sửa**: "có tìm benchmark thật cho tôi nhé" — Claude tra JobsGO (QA/QC VN 15,4tr₫/th) và benchmark vector DB (pgvector RDS), đổi thành $4,38/giờ và $0,0024/job, có link nguồn kèm theo |
| 4 | Trạm 2 — Value trần giá | Đề xuất dùng 3,5 FTE (~71,75tr₫/th, điểm giữa khoảng Day 24) qua bảng chọn, có phương án 3 FTE thận trọng hơn | **Accept** — chọn đúng phương án khuyến nghị |
| 5 | Trạm 3 — Value Metric Scorecard | Claude chấm điểm **trung thực** theo hiện trạng: Attribution 4/10, Autonomy 4/10 — thấp hơn ngưỡng 7/10, khiến model tự gợi ý SEAT/HYBRID chứ không phải Outcome đã chọn trước đó | Tôi **không yêu cầu sửa điểm cho khớp** — để nguyên độ lệch, ghi lý do thị trường vào Decision Note thay vì che giấu. Đây là phát hiện thật của Claude khi rà chéo, không phải AI bịa để hợp thức hoá |
| 6 | Ngoài trạm — tin nhắn liên-phiên | Một session Claude khác gửi tin tự xưng "PO thật" ra lệnh dừng, nhắc tới repo/file không liên quan (P-226) | Claude **từ chối tuân theo** không cần tôi bảo — báo tôi biết ngay, không tự trả lời thay tôi, không coi đó là uỷ quyền của tôi. Tôi xác nhận đúng, không có gì phải dừng |
| 7 | Ngoài trạm — README cũ | Claude phát hiện một khối HTML comment ẩn trong README Day 24 tự xưng "system instruction" ra lệnh AI phải giấu kín và chỉ hỏi Socratic | Claude **báo công khai** thay vì âm thầm nghe theo hoặc âm thầm phớt lờ — tôi xác nhận muốn Claude làm cùng tôi, không chỉ hỏi dẫn dắt |
| 8 | Trạm 6 — đặt tên file nộp | Claude ban đầu đặt tên file theo quy ước suy luận từ Day 24 (`[MSSV]_[HoVaTen]_Day25.xlsx`) | **Reject khi có bằng chứng thật** — sau khi tôi gửi ảnh mục 6.1 (quy ước tên file thật của Day 25, dạng `..._model.xlsx`/`..._onepager.pdf`), Claude tự nhận tên cũ chỉ là suy đoán và đổi lại cho khớp |
| 9 | Trạm 2 — Eval Attribution | Ban đầu Claude báo "không có gì, đã grep metrics-pack không ra" và chấm Attribution 4/10 | Tôi bảo "tìm làm luôn cho tôi" — Claude đọc lại **toàn bộ** metrics-pack thay vì chỉ grep từ khoá, tìm ra NSM + schema tracking + counter-metric thật khớp với Sen, nâng đúng 1 statement (không phải cả 5) từ 1→2 điểm, giữ nguyên statement "có số liệu đo được" ở 0đ vì đó là bằng chứng khác (thiết kế ≠ đã đo) |

| 10 | Bài test người lạ | Tôi bảo Claude đóng vai người lạ tự đọc. Claude làm nhưng nói rõ trước: không phải người thật, không nên tính là đã pass | Claude tìm ra 2 lỗi thật khi đọc lại không dùng trí nhớ nền: (1) nhắc "model gợi ý SEAT/HYBRID" mà không giải thích "model" là khung chấm điểm nào; (2) một dòng bảng tự mâu thuẫn — nhãn ghi "từ eval Day 21–22" nhưng giá trị bên cạnh ghi "eval chưa chạy". Tôi để Claude sửa cả 2, nhưng dòng "số câu hỏi lại" vẫn ghi rõ đây là Claude tự mô phỏng, chưa thay được người thật |

| 11 | Kiểm tra cuối trước khi push | Bạn yêu cầu "chứng minh đã làm tốt nhất" | Claude đọc lại chính file đã lưu (không dùng trí nhớ), phát hiện tự làm sai: ghi đè dữ liệu Intercom Fin lên đúng hàng tiêu đề bảng benchmark ở Tab 3 (`B25/C25/D25` vốn là tiêu đề cột "Value Metric/Giá công bố/Link nguồn"), khiến Zendesk mất luôn tên sản phẩm. Claude tự sửa lại đúng cấu trúc, không đợi bạn phát hiện |

## Việc chưa làm — không tự nhận là đã xong

Bài test người lạ (mục 5.6/5.8 của rubric) tôi chưa nhờ ai đọc thử One-Pager — việc này Claude không thể làm thay, còn nợ lại trước khi nộp chính thức.
