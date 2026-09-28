# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | MISSING | 9 |
| center | B2 | SPURIOUS | 20 |
| center | C0 | SPURIOUS | 2 |
| center | C0 | WRONG_CLASS | 1 |
| edge | B2 | SPURIOUS | 1 |
| edge | B2 | STRUCTURE | 1 |
| edge | C0 | SPURIOUS | 1 |
| mid | B2 | ATTRIBUTE | 2 |
| mid | B2 | MISSING | 4 |
| mid | B2 | SPURIOUS | 6 |
| mid | B2 | WRONG_CLASS | 2 |

## Top defects
- SPURIOUS: 30 (ví dụ frame adasind_019560.jpg)
- MISSING: 13 (ví dụ frame adasind_062370.jpg)
- WRONG_CLASS: 3 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy:
  - Ca rõ nhất là `adasind_062370.jpg`, object `L7`. Learner gán chiếc van trắng là `Truck`, trong khi đối chiếu với ảnh và rule R04 cho thấy đây là van chở người, phải gán `Car`. Finding này được phân loại `E1_annotator_error`.
  - `local_quality_conflicts.csv` ghép `L7 Truck` với `R4 Car` ở IoU = 0.965, cho thấy hai box đang nói về cùng một phương tiện.
  - Hai finding `R7` và `R8` của cùng frame được giữ lại dưới `E0_reference_defect`: sau khi kiểm ảnh/overlay, không có đủ bằng chứng để thêm hai object độc lập chỉ vì teaching reference có box. Teaching reference không được coi là gold tuyệt đối.
  - `adasind_086220.jpg L4` vẫn là `E5_unresolved`: chưa đủ bằng chứng để xác định đó là object hợp lệ riêng hay annotation thừa nên được escalation thay vì sửa âm thầm.
  - Số lượng `SPURIOUS` lớn trong bảng tổng hợp không đồng nghĩa tất cả là lỗi annotator, vì findings còn bao gồm khác biệt giữa learner, teaching reference và model.

- Cách sửa và ai nhận việc (`owner`):
  - `owner=annotator` cho ca `L7`: đổi class `Truck` → `Car`, giữ nguyên geometry vì box đã bám đúng phương tiện.
  - Không thêm box cho `R7/R8`; giữ annotation hiện tại với `keep_with_reason` vì có bằng chứng reference có vấn đề.
  - Ca `adasind_086220.jpg L4` giao `owner=qa`, `action=escalate` để cần thêm review độc lập.
  - Sau rework, bảng delta cho thấy vùng `mid`: matched tăng `5 → 6`, missing giảm `1 → 0`, spurious giảm `1 → 0`. Vùng `center` cũng giảm spurious `5 → 3`.

- Bằng chứng:
  - `submission/r3_diag/local_quality_conflicts.csv`: `adasind_062370.jpg`, L7/R4, `Truck` vs `Car`, IoU `0.965`.
  - `submission/findings.csv`: finding `L7` dùng `E1_annotator_error`, rule `R04`, action `rework`; `R7/R8` dùng `E0_reference_defect`; `adasind_086220.jpg L4` dùng `E5_unresolved` và `escalate`.
  - `submission/rework/delta.md`: xác nhận hai finding liên quan L7/R4 đã được sửa và số trước/sau cải thiện.
  - `submission/r1_craft/compare.html`: overlay trực quan learner/reference.
  - R04: van chở người được ánh xạ thành `Car`.
