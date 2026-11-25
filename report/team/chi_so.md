# Đặc tả chỉ số, event và rủi ro kinh tế · Nhiệm vụ E1, E2

## E1 · Đặc tả chỉ số

| Loại | Chỉ số | Công thức | Tính thử trên 1.200 yêu cầu |
| --- | --- | --- | --- |
| Chính (kết quả) | % yêu cầu đóng trong 24 giờ và không mở lại trong 7 ngày | `dong_trong_24h` bằng 1 và `mo_lai_trong_7_ngay` bằng 0, chia tổng số yêu cầu | 82,83% (994 / 1.200) |
| Dùng | Tỉ lệ bỏ qua gợi ý | `quyet_dinh_xem_lai` là `sua` hoặc `bo`, chia số yêu cầu được xem lại | 27,12% (48 / 177) |
| An toàn | Tỉ lệ lỗi lọt đến khách | `mo_lai_trong_7_ngay` bằng 1, chia tổng số yêu cầu | 4,25% (51 / 1.200) |
| Dùng (tự đề xuất) | Tỉ lệ nhân viên mở trợ lý | Số yêu cầu của nhóm can thiệp có `agent_suggestion_shown` chia tổng yêu cầu của nhóm can thiệp (theo `staff_id`) | Không cần tính |
| An toàn (tự đề xuất) | Tỉ lệ đơn hoàn sai tiền phát hiện qua kiểm tra mẫu | Số đơn lệch tiền trong `audit_sample_checked` chia tổng số đơn kiểm tra mẫu hằng tuần | Không cần tính |

Chỉ số trong đợt chạy thử là **82,83%** (không viết "trợ lý đã nâng chỉ số", vì đợt chạy thử không có nhóm đối chứng).

## Danh sách event

Ít nhất sáu event, mỗi event có `trace_id` để nối với trace của agent.

| Event | Ai tạo | Thuộc tính chính | Thời điểm |
| --- | --- | --- | --- |
| `refund_request_created` | App khách / Ticket | `request_id, loai, so_tien_vnd, arm, staff_id, trace_id` | Khi khách tạo yêu cầu |
| `agent_run_completed` | Trợ lý agent | `attempt, tokens_in, tokens_out, tool_calls, status, price_table_version, trace_id` | Sau mỗi lần chạy, kể cả lỗi |
| `agent_suggestion_shown` | Giao diện CSKH | `staff_id, so_tien_de_xuat, trace_id` | Khi gợi ý hiện cho nhân viên |
| `staff_review_decision` | Nhân viên CSKH | `staff_id, decision` (`giu`/`sua`/`bo`), `phut_xem_lai_thuc, trace_id` | Khi nhân viên bấm gửi, sửa hoặc bỏ |
| `staff_rework_completed` | Nhân viên CSKH | `staff_id, phut_lam_lai_thuc, ly_do, trace_id` | Khi hoàn tất làm lại ca sai |
| `refund_ledger_write` | Dịch vụ sổ cái | `idempotency_key, so_tien, status` (`ok`/`503`), `trace_id` | Khi ghi lệnh hoàn tiền |
| `handoff_to_staff` | Trợ lý agent | `reason, loai, tom_tat, trace_id` | Khi chuyển nhân viên xử lý |
| `ticket_closed` | Hệ thống ticket | `closed_at, trong_24h, trace_id` | Khi yêu cầu được đóng |
| `ticket_reopened` | Khách hàng / CSKH | `reopened_at, trong_7_ngay, reason, trace_id` | Khi khách mở lại yêu cầu |
| `audit_sample_checked` | Kế toán | `so_tien_da_hoan, so_tien_dung, lech_tien, trace_id` | Kiểm tra mẫu 100 đơn hằng tuần |

**Kiểm tra chéo:** với mỗi chỉ số ở bảng E1, ghi event dùng để tính. Chỉ số nào không tính được từ danh sách event thì chưa đo được.

- **Chỉ số chính (`82,83%`):** tính từ `refund_request_created`, `ticket_closed` (`trong_24h=1`) và `ticket_reopened` (không có `trong_7_ngay=1` theo `trace_id`) — **đo được**.
- **Chỉ số dùng — Tỉ lệ bỏ qua gợi ý (`27,12%`):** tính từ `agent_suggestion_shown` và `staff_review_decision` (`decision` là `sua` hoặc `bo`) — **đo được**.
- **Chỉ số an toàn — Tỉ lệ lỗi lọt đến khách (`4,25%`):** tính từ `refund_request_created` và `ticket_reopened` (`trong_7_ngay=1`) — **đo được**.
- **Chỉ số dùng tự đề xuất — Tỉ lệ nhân viên mở trợ lý:** tính từ `refund_request_created` (`arm=treatment`, `staff_id`) và `agent_suggestion_shown` — **đo được** (đồng thời kiểm tra rò rỉ dùng chéo ở nhóm đối chứng).
- **Chỉ số an toàn tự đề xuất — Tỉ lệ hoàn sai tiền qua kiểm tra mẫu:** tính từ `audit_sample_checked` (`lech_tien != 0`) — **đo được** (bắt lỗi ngầm như Ca 5, Ca 17).

## E2 · Rủi ro kinh tế

Ít nhất hai dòng, số lấy từ bảng độ nhạy (`bang_chi_phi.md`).

| Rủi ro | Tác động đã tính | Dấu hiệu theo dõi | Hành động | Người phụ trách |
| --- | --- | --- | --- | --- |
| Số ca làm lại tăng gấp đôi | Chi phí mỗi việc thành công tăng **+51,8%**, từ 4.472 đ lên **6.787 đ** (`simulated`) | Tỉ lệ `lam_lai` theo tuần vượt **7%** (mẫu chạy thử ở phạm vi `noi_dia` + `hang_nang` là **4,9%**) | Tạm dừng `hang_nang`, thu hẹp về `noi_dia` và rà soát 20 trace `lam_lai` gần nhất | PM trợ lý hoàn phí |
| Phải xem lại 100% kéo dài | Chi phí đạt **11.743 đ = 0,98×** (9 phút làm lại) hoặc **12.415 đ = 1,03×** (15,3 phút thực tế) so với 12.000 đ (`simulated`) | Tỉ lệ yêu cầu được xem lại vẫn **> 50%** sau tuần đầu (hết bước rollout 0,25) | Giảm tỉ lệ xem lại theo bậc ở các ca `noi_dia` khi tỉ lệ `sua + bo` < 15% và thời gian xem lại < 4,8 phút | Trưởng nhóm CSKH |
| Khối lượng xử lý thấp hơn dự kiến | Chi phí cố định 40 triệu đ/tháng tăng từ **+1.185 đ/việc** (45.000 yc/tháng) lên **+2.370 đ/việc** nếu giảm một nửa (`simulated`) | Số việc thành công hằng tuần đạt **< 50%** kế hoạch | Không mở rộng pilot, rà lại hạ tầng để cắt chi phí cố định dưới mức hoà vốn | PM trợ lý hoàn phí |
