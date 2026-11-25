# Hồ sơ launch v0 · Trợ lý hoàn phí LogiX-VN · Gate 2a

Một trang. Cột trạng thái chỉ nhận: **Xong, có bằng chứng · Chưa · Giả lập**. Mục nào dựa trên cột `_simulated` ghi Giả lập. Người phụ trách là một vai trò, không ghi "cả đội". Gate 2a chỉ duyệt kế hoạch pilot: không viết như thể trợ lý đã được duyệt chạy chính thức (xem quy tắc 5 trong `README.md`).

Nhóm: olala (làm cá nhân: NguyenManhQuan – 2A202603776) · Lớp: L3B

| Mục | Con số chính | Trạng thái | Người phụ trách |
| --- | --- | --- | --- |
| 1 · Chi phí mỗi việc thành công | **4.472 đ** (`simulated`), gấp **16,3×** hoá đơn token+tool (**274,7 đ**); phạm vi `noi_dia` + `hang_nang` cộng cố định là **4.599 đ** ở 45.000 yc/tháng (`simulated`) | Giả lập | Kế toán trưởng |
| 2 · Ba yếu tố nhạy nhất | **1. Số ca làm lại (+51,8%) · 2. Tỉ lệ xem lại (+40,7%) · 3. Lương NV (+23,1%)** (`simulated`) | Giả lập | PM trợ lý hoàn phí |
| 3 · So với nhân viên tự làm | Hệ thống chung **5.865 đ/yc = 0,49×**; `noi_dia` **0,22×**, `hang_nang` **0,69×**, `quoc_te` **1,88×** (`simulated`); xem lại 100% tốn **11.743–12.415 đ (0,98×–1,03×)** (`simulated`) | Giả lập | Kế toán trưởng |
| 4 · Chỉ số chính, chỉ số dùng, chỉ số an toàn | Đợt chạy thử: chính **82,83%** (994/1.200), bỏ qua gợi ý **27,12%** (48/177), mở lại 7 ngày **4,25%** (51/1.200; **3,97%** trong phạm vi); đủ 10 event có `trace_id` | Xong, có bằng chứng | Trưởng nhóm CSKH |
| 5 · Bảng lỗi và cách khắc phục | 20 ca phân theo 5 loại PAIR (làm 1 mình, rà soát 20/20); đã có phương án phát hiện đo được và khắc phục 5 loại | Xong, có bằng chứng | Kỹ sư trưởng agent |
| 6 · Pilot plan | Phạm vi `noi_dia` + `hang_nang` (loại `quoc_te`, `doi_tac`); chia ngẫu nhiên **20 + 20 nhân viên**, $m \ge 299$, **n = 859/nhóm**, MDE **+6 điểm** (power **0,64** nếu thật là +5 điểm); 3 luật dừng đủ 4 vế | Xong, có bằng chứng | Giám đốc vận hành LogiX-VN |
| 7 · Rủi ro kinh tế | Làm lại ×2 đẩy chi phí lên **6.787 đ**; xem lại 100% kéo dài hết tiết kiệm (**1,03×**); giảm nửa khối lượng tăng cố định lên **+2.370 đ/việc** (`simulated`) | Giả lập | PM trợ lý hoàn phí |

**Đề xuất:** **Go có điều kiện** cho pilot phạm vi `noi_dia` + `hang_nang` (từ chối mở pilot cho `quoc_te` 1,88× và `doi_tac` 0,85×, `simulated`). Bốn điều kiện bắt buộc kèm người phụ trách và ngày kiểm tra:

- **Điều kiện 1 (An toàn hệ thống):** Sửa khoá chống trùng lệnh hoàn (Ca 20) và đối soát `refund_ledger_write` (Ca 7) không để báo "đã hoàn" khi sổ cái lỗi 503 — Phụ trách: **Kỹ sư trưởng agent** — Kiểm tra trước khi bật pilot (**2026-12-01**).
- **Điều kiện 2 (Cỡ mẫu & đánh đổi):** Ký xác nhận chấp nhận MDE **+6 điểm** (`n = 859`, `20 NV/nhóm`, chấp nhận power giảm còn **0,64** nếu mức tăng thật chỉ là +5 điểm) — Phụ trách: **Giám đốc vận hành LogiX-VN** — Kiểm tra trước ngày chạy (**2026-12-01**).
- **Điều kiện 3 (Đo lường thật thay số giả lập):** Bật đủ 10 event có `trace_id` (đặc biệt `phut_xem_lai_thuc`, `phut_lam_lai_thuc`) để thay số `simulated` và chạy kiểm tra mẫu 100 đơn/tuần (`audit_sample_checked`) — Phụ trách: **PM trợ lý hoàn phí** — Kiểm tra sau tuần 1 (**2026-12-08**).
- **Điều kiện 4 (Lộ trình giảm xem lại):** Áp dụng giảm xem lại theo bậc cho `noi_dia` khi `sua + bo < 15%`, vì giữ xem lại 100% khiến chi phí lên **0,98×–1,03×** (`simulated`), không còn hiệu quả kinh tế — Phụ trách: **Trưởng nhóm CSKH** — Kiểm tra cuối bước 0,25 (**2026-12-15**) trước khi chốt ngày quyết định **2027-01-05**.
