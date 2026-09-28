# Guideline patch

- **Rule mới đề xuất:** **R12 — Phân xử khi teaching reference mâu thuẫn với ảnh gốc.** Teaching reference không được xem là ground truth tuyệt đối. Nếu reference có box nhưng khi kiểm ảnh gốc không thấy một object độc lập hợp lệ, hoặc box reference trùng với cùng một physical object đã được gán nhãn, annotator không được thêm/xóa/sửa box chỉ để khớp reference. Phải ghi lại frame, object_ref và bằng chứng; dùng `E0_reference_defect` khi có đủ bằng chứng reference sai, hoặc `E5_unresolved` + `escalate` khi chưa đủ bằng chứng.

- **Áp dụng cho:** Tất cả 6 class (`Car`, `Bus`, `Truck`, `ThreeWheeler`, `Bike`, `Pedestrian`) và mọi zone (`center`, `mid`, `edge`). Rule này áp dụng khi phân xử bất đồng learner/reference; không thay đổi R01 về ngưỡng H=40, R02 về geometry hay các rule attribute/ignore hiện có.

- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R01 quy định vật cao ≥40 px trong vùng hợp lệ phải có box và R02 quy định box phải bám phần nhìn thấy trên ảnh gốc, nhưng chưa nêu rõ phải làm gì khi teaching reference tự tạo ra một `MISSING` không được ảnh gốc hỗ trợ. Trong `adasind_062370.jpg`, reference `R7` có dấu hiệu chồng lên cùng một ThreeWheeler đã tồn tại, còn `R8` báo một Truck nhưng khi kiểm ảnh/overlay không thấy một Truck độc lập tương ứng. Nếu chỉ làm theo compare report, annotator có thể thêm box sai chỉ để khớp reference. Taxonomy của lab đã cho phép `E0_reference_defect`, vì teaching reference chưa phải gold set đã được phê duyệt, nhưng quy tắc này nên được nêu trực tiếp trong guideline gán nhãn để tránh sửa nhãn đúng theo reference sai.

- **`rules_version` mới:** `v1.1.0`

- **Hiệu lực từ:** Áp dụng cho các round mới sau khi patch được Lab Coach/QA chấp thuận; không áp dụng hồi tố để thay đổi bản `r1_craft` đã khóa. Với round hiện tại, bất đồng được ghi trong `findings.csv` bằng `E0_reference_defect`, `keep_with_reason` hoặc `escalate` theo bằng chứng.
