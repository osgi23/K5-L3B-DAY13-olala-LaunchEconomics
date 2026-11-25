# Báo cáo cá nhân — NguyenManhQuan-2A202603776

## 1. Thông tin thành viên

- Họ tên: NguyenManhQuan
- MSSV: 2A202603776
- Email: manhquan03122005@gmail.com
- Vai trong nhóm (người viết code, người kiểm số, người gắn nhãn 1, người gắn nhãn 2 kiêm giữ hồ sơ): Kiêm cả 4 vai trò (làm cá nhân 1 mình do đến muộn và các nhóm khác đã đủ 4 người).

## 2. Phần việc phụ trách

- Toàn bộ quy trình từ CP1 đến CP5:
  - Hoàn thiện `src/lab13.py` (Nhiệm vụ A1–A4, B1–B4, D1).
  - Hoàn thiện các file hồ sơ trong `report/team/`: `bang_chi_phi.md`, `bang_loi.md`, `pilot_plan.yaml`, `chi_so.md`, `ho_so_launch_v0.md`, `group_report.md` và cập nhật `TEAM.md`.

## 3. Đóng góp cụ thể

- Viết 3 hàm A1 và hàm `mo_hinh(...)` tính chi phí thật trên trace (token, tool, xem lại, làm lại `simulated`), tách chi phí theo 4 loại yêu cầu (`noi_dia`, `hang_nang`, `quoc_te`, `doi_tac`) và cộng chi phí cố định 40 triệu đ/tháng cho phạm vi pilot.
- Chạy 9 kịch bản độ nhạy B1, cặp B2, so sánh giới hạn 1/2/3 lần trên chi phí cả hệ thống B3, và tính kịch bản xem lại 100% B4 (so sánh cả mức 9 phút giả định và 15,3 phút trung bình thực tế).
- Phân loại 20 ca lỗi theo 5 loại Google PAIR dựa trên nguyên nhân gốc và lập bảng khắc phục 5 ca có chỉ số phát hiện đo được.
- Tính 5 câu cỡ mẫu D1 bằng `statsmodels` và viết `pilot_plan.yaml` hoàn chỉnh với 3 luật dừng đủ 4 vế.
- Tính thử 3 chỉ số E1 trên 1.200 yêu cầu, thiết kế 10 event có `trace_id`, 3 dòng rủi ro kinh tế E2 và tổng hợp trang `ho_so_launch_v0.md` với đề xuất **Go có điều kiện**.

## 4. Bằng chứng

- Code chạy hoàn chỉnh: `src/lab13.py` (ba phép thử A1 in `ĐẠT`: 1,20 · 1,25 · 1,25; A2 CPS = 4.472 đ `simulated`; B3 rẻ nhất tại 2 lần = 6.901.220 đ `simulated`; D1 `n = 859` với 20 nhân viên/nhóm, $m \ge 299$).
- Các file hồ sơ: `report/team/bang_chi_phi.md`, `report/team/bang_loi.md`, `report/team/pilot_plan.yaml` (đọc hợp lệ bằng `yaml.safe_load`, 0 dấu `?`), `report/team/chi_so.md`, `report/team/ho_so_launch_v0.md`, `report/team/group_report.md`, `TEAM.md`.

## 5. Công cụ AI đã dùng

- **Công cụ:** Trợ lý AI lập trình (Antigravity / Gemini) hỗ trợ đọc hiểu yêu cầu repo, gợi ý cấu trúc code Python trong `src/lab13.py`, và rà soát checklist nộp bài.
- **Cách tự kiểm tra:**
  - Chạy trực tiếp `python lab13.py` trong `src/` để xác nhận 3 phép thử A1 in `ĐẠT` và đối chiếu từng con số A2–A4, B1–B4, D1, E1 với công thức trong `docs/du_lieu_va_cong_thuc.md` và `docs/Lab13_Huong_dan_chi_tiet_buoi_chieu.md`.
  - Chạy kiểm tra cú pháp YAML bằng `yaml.safe_load`, kiểm tra không còn `?` ngoài comment và tuân thủ quy tắc 5 (không đề cập triển khai chính thức trong `report/team/`).
  - Tự rà soát phân loại 20 ca lỗi theo nguyên nhân gốc và giữ trung thực thông tin làm cá nhân (không bịa thành viên thứ 2 hay kết quả duyệt chéo).

## 6. Tự đánh giá

- Hoàn thành đầy đủ phần tính toán định lượng (70 điểm đối chiếu đáp án) và 5/6 file hồ sơ nhóm đúng quy chuẩn đặt tên, nhãn `simulated` và phạm vi chỉ duyệt pilot Gate 2a.
- Điểm còn thiếu tại thời điểm đóng gói: phần duyệt chéo Gate 2a (`report/team/phieu_cham.md`) và đánh giá từ nhóm hội đồng cần được giảng viên/coach sắp xếp ghép cặp riêng cho trường hợp làm cá nhân.
