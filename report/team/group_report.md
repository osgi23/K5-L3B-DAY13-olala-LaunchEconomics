# Báo cáo nhóm

Báo cáo ngắn, tối đa 2 trang. Số liệu chi tiết nằm trong các file hồ sơ; ở đây chỉ dẫn lại con số chính.

## 1. Thông tin nhóm

- Tên nhóm: olala (làm cá nhân 1 người)
- Lớp: L3B
- Thành viên: NguyenManhQuan (MSSV: `2A202603776`, chi tiết trong [TEAM.md](../../TEAM.md))

## 2. Mục tiêu và cách tiếp cận

Xây dựng bộ **hồ sơ launch v0** cho trợ lý hoàn phí LogiX-VN tại cổng **Gate 2a** trên dữ liệu giả lập gồm 1.200 yêu cầu và 1.624 lần chạy (`src/logix_requests.csv`, `src/logix_runs.csv`). Cách tiếp cận đi lần lượt từ: (1) mô hình hoá chi phí thật mỗi việc thành công và phân tích độ nhạy bằng Python (`src/lab13.py`), (2) phân loại 20 ca lỗi theo khung Google PAIR, (3) tính cỡ mẫu có hiệu chỉnh cụm cho pilot, và (4) tổng hợp chỉ số, danh sách event, rủi ro kinh tế để ra đề xuất **Go có điều kiện**.

## 3. Giải pháp

- **Nhiệm vụ A & B ([bang_chi_phi.md](bang_chi_phi.md)):** Hoàn thiện 3 hàm A1 đạt chuẩn (1,20 · 1,25 · 1,25) và hàm `mo_hinh` trong [src/lab13.py](../../src/lab13.py) để tính chi phí thật trên trace (gồm token, tool mọi lần chạy, cộng giờ xem lại và làm lại `simulated`), tách theo 4 loại yêu cầu, cộng chi phí cố định 40 triệu đ/tháng cho `noi_dia + hang_nang`, và chạy 9 kịch bản độ nhạy B1, cặp B2, chi phí hệ thống B3, xem lại 100% B4.
- **Nhiệm vụ C ([bang_loi.md](bang_loi.md)):** Phân loại 20 ca lỗi theo nguyên nhân gốc (4 Do người dùng, 5 Hệ thống, 4 Ngữ cảnh, 4 Giới hạn hệ thống, 3 Ngầm) và đề xuất phương án phát hiện đo được kèm 1 vai trò phụ trách cho 5 ca đại diện.
- **Nhiệm vụ D ([pilot_plan.yaml](pilot_plan.yaml)):** Tính 5 câu cỡ mẫu D1 bằng `statsmodels`, chọn chia ngẫu nhiên theo nhân viên (`20 + 20`, $m \ge 299$, `n = 859/nhóm`), kiểm tra 5 câu tách tác động D2 và thiết lập 3 luật dừng 4 vế `NẾU – TRONG – THÌ – KHÔNG THÌ`.
- **Nhiệm vụ E ([chi_so.md](chi_so.md), [ho_so_launch_v0.md](ho_so_launch_v0.md)):** Tính thử 3 chỉ số trên 1.200 yêu cầu, đề xuất thêm 2 chỉ số, thiết kế 10 event có `trace_id`, lập 3 dòng rủi ro kinh tế và chốt hồ sơ 1 trang.

## 4. Kết quả

- **Chi phí thật:** **4.472 đ/việc thành công** (`simulated`), gấp **16,3×** hoá đơn token + tool (**274,7 đ**); làm lại chiếm **51,8%** và xem lại chiếm **40,7%** (`simulated`). Tính cả 222 ca chuyển nhân viên, chi phí cả hệ thống là **5.865 đ/yêu cầu = 0,49×** mức 12.000 đ (`simulated`). Ở phạm vi `noi_dia + hang_nang` cộng cố định 40 triệu/tháng là **4.599 đ = 0,38×** (`simulated`), còn `quoc_te` lỗ (**22.515 đ = 1,88×**, `simulated`).
- **Độ nhạy:** Top 3 yếu tố ảnh hưởng mạnh nhất là số ca làm lại (**+51,8%**), tỉ lệ xem lại (**+40,7%**) và lương nhân viên (**+23,1%**) (`simulated`). Nếu xem lại 100%, chi phí lên **11.743–12.415 đ (0,98×–1,03×)** (`simulated`).
- **Đề xuất Gate 2a:** **Go có điều kiện** cho pilot phạm vi `noi_dia + hang_nang` (loại `quoc_te`, `doi_tac`), kèm 4 điều kiện cụ thể về sửa lỗi Ca 7/20, ký nhận đánh đổi MDE +6 điểm (power 0,64 ở +5 điểm), thu thập đủ 10 event thật và lộ trình giảm xem lại.
- **Kết quả duyệt chéo:** Chưa có phiếu chấm từ hội đồng (chờ ghép cặp duyệt chéo cho trường hợp làm cá nhân).

## 5. Khó khăn và cách xử lý

- **Làm bài một mình thay vì nhóm 4 người:** Do đến lớp muộn khi các nhóm khác đã đủ 4 thành viên, học viên (`NguyenManhQuan`, MSSV `2A202603776`) phải tự đảm nhiệm cả 4 vai trò (viết code, kiểm số, gắn nhãn lỗi, giữ hồ sơ).
- **Xử lý yêu cầu 2 người ở Nhiệm vụ C và duyệt chéo Gate 2a:** Không tự bịa tên thành viên thứ 2 hay tỉ lệ đồng thuận giả trong [bang_loi.md](bang_loi.md), mà ghi rõ thực tế làm 1 mình, rà soát lại 20/20 ca theo đúng nguyên nhân gốc Google PAIR và báo cáo giảng viên/coach để được phân công duyệt chéo [phieu_cham.md](phieu_cham.md).

## 6. Tổng hợp đóng góp

Chi tiết đóng góp của thành viên duy nhất (`NguyenManhQuan - 2A202603776`) nằm trong [TEAM.md](../../TEAM.md) và [2A202603776_NguyenManhQuan.md](2A202603776_NguyenManhQuan.md).

## 7. Hạn chế và hướng cải thiện

- Dữ liệu thời gian xem lại/làm lại hiện là số `simulated`, và dữ liệu chạy thử 2 tuần chưa có nhóm đối chứng nên chưa thể khẳng định tác động nhân quả trước khi chạy pilot.
- Với 40 nhân viên, cách chia cụm đạt power 0,80 buộc phải nới MDE lên +6 điểm; cần bổ sung logging thời gian thật ngay tuần đầu pilot và cân nhắc kéo dài thời gian thu mẫu nếu muốn phát hiện mức chênh +5 điểm.

## 8. Tài liệu tham khảo

- Erol et al., *Cost-of-Pass: An Economic Framework for Evaluating Language Models*, [arxiv.org/abs/2504.13359](https://arxiv.org/abs/2504.13359)
- Google PAIR, *People + AI Guidebook*, chương "Errors + Graceful Failure"
- Tài liệu `statsmodels.stats.power.NormalIndPower` và đề bài Lab 13 (`docs/`)
