# Bảng lỗi và cách khắc phục · Nhiệm vụ C

20 ca lỗi nằm trong `docs/Ngay13_Lab13_De_bai_hoc_vien.docx`. Năm loại theo Google PAIR: **Do người dùng · Hệ thống · Ngữ cảnh · Giới hạn hệ thống · Ngầm**. Gắn nhãn theo nguyên nhân gốc, không theo chỗ cần sửa.

## Hai bộ nhãn độc lập

Người gắn nhãn 1: NguyenManhQuan (MSSV: 2A202603776) · Người gắn nhãn 2: Không có (làm cá nhân 1 mình do đến muộn và các nhóm đã đủ; không tự bịa người gắn nhãn thứ 2)

| Ca | Nhãn người 1 | Nhãn người 2 | Trùng? | Nhãn thống nhất |
| --: | --- | --- | --- | --- |
| 1 | Do người dùng | — (làm 1 mình) | — | Do người dùng |
| 2 | Hệ thống | — (làm 1 mình) | — | Hệ thống |
| 3 | Ngữ cảnh | — (làm 1 mình) | — | Ngữ cảnh |
| 4 | Giới hạn hệ thống | — (làm 1 mình) | — | Giới hạn hệ thống |
| 5 | Ngầm | — (làm 1 mình) | — | Ngầm |
| 6 | Do người dùng | — (làm 1 mình) | — | Do người dùng |
| 7 | Hệ thống | — (làm 1 mình) | — | Hệ thống |
| 8 | Hệ thống | — (làm 1 mình) | — | Hệ thống |
| 9 | Do người dùng | — (làm 1 mình) | — | Do người dùng |
| 10 | Ngữ cảnh | — (làm 1 mình) | — | Ngữ cảnh |
| 11 | Giới hạn hệ thống | — (làm 1 mình) | — | Giới hạn hệ thống |
| 12 | Ngầm | — (làm 1 mình) | — | Ngầm |
| 13 | Giới hạn hệ thống | — (làm 1 mình) | — | Giới hạn hệ thống |
| 14 | Do người dùng | — (làm 1 mình) | — | Do người dùng |
| 15 | Hệ thống | — (làm 1 mình) | — | Hệ thống |
| 16 | Ngữ cảnh | — (làm 1 mình) | — | Ngữ cảnh |
| 17 | Ngầm | — (làm 1 mình) | — | Ngầm |
| 18 | Ngữ cảnh | — (làm 1 mình) | — | Ngữ cảnh |
| 19 | Giới hạn hệ thống | — (làm 1 mình) | — | Giới hạn hệ thống |
| 20 | Hệ thống | — (làm 1 mình) | — | Hệ thống |

**Tỉ lệ đồng thuận:** Làm cá nhân 1 mình (không tính đồng thuận giữa 2 người để tránh bịa số liệu); đã rà soát độc lập nguyên nhân gốc từng ca theo 5 định nghĩa Google PAIR và đối chiếu chuẩn 20/20 ca.

## Quy tắc phân biệt cho các ca dễ lẫn

Ghi quy tắc phân biệt theo nguyên nhân gốc cho các cặp dễ nhầm:

- **Ca 6, Ca 9 (`Do người dùng` vs `Hệ thống`):** Gốc lỗi là khách chọn sai mục (Ca 6) hoặc nhập sai loại mã (Ca 9); việc trợ lý chưa gợi ý lại thuộc phần khắc phục, không phải nguyên nhân gốc.
- **Ca 13 (`Giới hạn hệ thống` vs `Hệ thống`):** Hoàn phí bảo hiểm đối tác nằm ngoài phạm vi trợ lý nên gốc là giới hạn hệ thống, kể cả khi trợ lý xử lý giới hạn đó chưa rõ ràng.
- **Ca 8, Ca 15 (`Hệ thống` vs `Ngầm`):** Sai đã lộ ra (trích dẫn điều khoản bịa đặt nhìn thấy được ở Ca 8; nhân viên xem lại phát hiện ở Ca 15), còn lỗi ngầm là sai mà cả khách lẫn hệ thống đều không nhận ra tới khi kiểm tra mẫu.
- **Ca 18 (`Ngữ cảnh` vs `Hệ thống`):** Số tiền 15.000 đ hoàn toàn đúng chính sách (50% của 30.000 đ), chỉ giả định "khách tự hiểu cách tính" không khớp hoàn cảnh của khách.
- **Ca 12 (`Ngầm` vs `Hệ thống`):** Câu trả lời cuối đúng nhưng chi phí token ở depot D05 tăng gấp 3 lần suốt 3 tuần mà không có cảnh báo — lỗi ngầm bao gồm cả sai lệch âm thầm về chi phí.

## Bảng khắc phục cho 5 ca, mỗi loại một ca

Cách phát hiện phải đo được (event, ngưỡng, tần suất). Người phụ trách là một vai trò, không ghi "cả đội".

| Ca | Loại lỗi | Phát hiện bằng gì | Khắc phục thế nào | Ai phụ trách |
| --: | --- | --- | --- | --- |
| 9 | Do người dùng | Event `input_validation_failed` gắn `trace_id`; cảnh báo khi vượt **2%** tổng yêu cầu/ngày | Nhận diện định dạng mã sàn TMĐT để tra sang mã vận đơn; nếu không tra được thì hiển thị hướng dẫn kèm ảnh minh hoạ | PM trợ lý hoàn phí |
| 7 | Hệ thống | Đối soát mỗi giờ giữa tin nhắn "đã hoàn" và bản ghi sổ cái `status=ok` cùng `trace_id`; ngưỡng **0 ca** lệch | Chỉ gửi thông báo "đã hoàn" khi API sổ cái trả `ok`; nếu lỗi 503 sau 3 lần thử thì báo "đang xử lý" và chuyển nhân viên | Kỹ sư trưởng agent |
| 18 | Ngữ cảnh | Tỉ lệ khách mở lại (`mo_lai_trong_7_ngay=1`) với lý do khiếu nại số tiền dù kiểm tra tính đúng, tổng hợp **theo tuần** (ngưỡng > 1%) | Chuẩn hoá mẫu tin nhắn luôn kèm phép tính rõ ràng (ví dụ: `30.000 đ × 50% = 15.000 đ`) | Trưởng nhóm CSKH |
| 4 | Giới hạn hệ thống | Event `handoff_to_staff` với `reason=thieu_du_lieu` theo cột `loai`, theo dõi **hàng ngày** | Giữ cơ chế chuyển thẳng cho nhân viên kèm tóm tắt ngữ cảnh; loại `quoc_te` khỏi phạm vi pilot | PM trợ lý hoàn phí |
| 17 | Ngầm | Kiểm tra ngẫu nhiên **100 đơn/tuần** đối chiếu với bảng giá hiệu lực; ngưỡng cảnh báo **$\ge 1\%$** đơn lệch tiền | Xoá bộ nhớ đệm (cache) ngay khi phát hành bảng giá mới và ghi `price_table_version` vào `trace_id` | Kế toán trưởng |
