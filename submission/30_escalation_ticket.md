# Escalation ticket

## Ticket 1

- **Frame:** `adasind_086220.jpg`, object `L4` (`Bike`, learner-only / `L_only`)
- **Ảnh chụp:** `submission/screenshots/adasind_086220_L4.png`
- **Expected impact:** L4 nằm sát và bị che một phần bởi ThreeWheeler bên phải. Nếu đây không phải một `Bike` độc lập thì giữ box sẽ tạo annotation thừa; ngược lại, nếu đây là một Bike hợp lệ mà teaching reference/model bỏ sót thì xóa box sẽ làm mất nhãn đúng. Một frame hiện tại chưa đủ bằng chứng để kết luận chắc chắn.
- **Owner:** `qa`
- **Recommendation:** QA độc lập mở ảnh gốc full-resolution, kiểm L4 có phải một physical object riêng hay chỉ là phần của phương tiện lân cận; đồng thời kiểm R01 về ngưỡng H >= 40 px và phạm vi hợp lệ. Nếu xác nhận Bike hợp lệ thì giữ box. Nếu xác nhận không phải object độc lập hoặc không đạt scope thì chuyển cho annotator rework. Nếu vẫn chưa đủ bằng chứng thì giữ `E5_unresolved` và trạng thái escalated.
