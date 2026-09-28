# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: **không nên tự động coi là lỗi `DUPLICATE`**. Hai camera có thể cùng nhìn thấy một physical object trong vùng chồng nên hai box có thể đều hợp lệ nếu output được định nghĩa theo từng camera. Cần một policy riêng quy định annotation/output mong muốn. Trước khi kết luận duplicate, xoá một box hoặc ghép chúng thành cùng identity, cần có timestamp đồng bộ, calibration xác định vùng overlap và policy output đích.

2. Với một vật đi qua nhiều frame trên cùng camera, tôi giữ cùng track ID khi vẫn xác định đó là cùng một physical object và nó còn được quan sát liên tục. Khi hình học/vị trí thay đổi đáng kể thì thêm keyframe để mô tả đúng shape/box ở thời điểm đó; khi vật ra khỏi trường nhìn thì đặt trạng thái `Outside` theo guideline của task thay vì tạo một identity mới tùy ý. Trước khi nối track qua hai camera, tôi cần ít nhất timestamp đồng bộ, calibration/camera geometry để chứng minh vùng nhìn chồng và policy quy định output có cho phép identity cross-camera hay không; chỉ giống hình ảnh là chưa đủ bằng chứng.

3. Ca bất đồng thực tế của tôi là `adasind_062370.jpg`, đặc biệt reference `R7` và `R8`. Ban đầu compare report cho thấy chúng là `MISSING`, nhưng khi tôi kiểm lại ảnh/overlay thì `R7` có dấu hiệu chồng lên cùng một ThreeWheeler đã được annotation, còn ở `R8` tôi không thấy một Truck độc lập đủ rõ để thêm box. Vì vậy tôi không sửa annotation chỉ để khớp teaching reference; hai finding được ghi `E0_reference_defect` và `keep_with_reason`. Nếu làm lại slice này, tôi sẽ kiểm ảnh gốc và overlay trước khi coi mọi `R_only/MISSING` là lỗi annotator, đồng thời ghi bằng chứng ngay tại thời điểm phát hiện bất đồng để tránh phải phân xử lại về sau. Ảnh minh chứng: `submission/screenshots/adasind_062370_R7_R8.png`.
