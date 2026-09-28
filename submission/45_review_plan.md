# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_062370.jpg` | So sánh L/R có 3 khác biệt chính: 1 `WRONG_CLASS` ở `L7/R4` và 2 `MISSING` ở `R7`, `R8`. P4 xác định `L7` là `E1_annotator_error`; `R7/R8` có bằng chứng `E0_reference_defect`. | Frame này có đồng thời lỗi class của annotator và khả năng lỗi teaching reference. Nếu chỉ sửa theo reference mà không nhìn ảnh gốc có thể thêm box sai. Đây cũng là frame có rework thực tế `Truck -> Car`. | Ảnh gốc; `submission/r1_craft/compare.html`; `submission/r3_diag/local_quality_conflicts.csv`; các dòng `L7`, `R7`, `R8` trong `findings.csv`; `submission/rework/delta.md`. |
| `adasind_086220.jpg` | So sánh L/R có 1 `ATTRIBUTE` ở `L7/R1` và 2 `SPURIOUS` ở `L1`, `L4`. Riêng `L4` được giữ `E5_unresolved`, `owner=qa`, `action=escalate`. | `L4` nằm sát và bị che bởi ThreeWheeler nên chưa đủ bằng chứng xác định là một Bike độc lập hay annotation thừa. Ca này cần review độc lập thay vì tự sửa để khớp reference/model. | Ảnh gốc; `submission/screenshots/adasind_086220_L4.png`; `submission/r1_craft/compare.html`; dòng finding `L4`; `submission/30_escalation_ticket.md`. |

Giới hạn của kết luận từ ba frame ADASIND: chỉ có ba frame nên số mẫu rất nhỏ, phân bố class và zone không cân bằng, teaching reference chưa phải gold set đã được xác nhận độc lập, và các khác biệt quan sát được không đủ để suy rộng thành tỷ lệ lỗi của toàn bộ ADASIND hoặc hệ SVM bốn camera. `center/mid/edge` chỉ là bin vị trí tương đối trong vòng kính, không trực tiếp cho biết mức rủi ro hay độ khó chung.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`: kiểm đủ tám ô `front/rear/left/right × normal/hard`; trong mỗi ô chọn dữ liệu từ nhiều cảnh hoặc đoạn thời gian khác nhau, không coi nhiều frame liên tiếp của cùng một cảnh là nhiều ca độc lập. Khi soát cần giữ camera/source, frame hoặc timestamp, điều kiện normal/hard và lý do chọn; đồng thời kiểm có đủ các tình huống như vật nhỏ, che khuất, méo rìa, vùng seam và mật độ phương tiện khác nhau.

Kế hoạch 200 frame này chỉ giúp chủ động tìm và review các hard case cần chú ý. Vì đây là phân bổ có chủ đích, số frame hữu hạn và các frame trong cùng chuỗi có thể tương quan, nó không phải mẫu ngẫu nhiên đại diện và không dùng để ước lượng trực tiếp tỷ lệ lỗi của toàn hệ thống.
