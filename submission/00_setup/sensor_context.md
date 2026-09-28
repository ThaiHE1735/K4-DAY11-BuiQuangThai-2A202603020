# Sensor Context

- **Slice:** B2-center
- **Nguồn dữ liệu:** ADASIND, ảnh fisheye một camera.
- **Vị trí camera:** Không khẳng định camera là front/rear/left/right vì dữ liệu hiện tại không cung cấp thông tin rig/calibration đủ để xác nhận chính xác vị trí lắp camera.
- **Đặc điểm ảnh:** Ảnh fisheye góc rộng, có biến dạng tăng về phía rìa và có vùng biên/vòng kính cần được kiểm bằng `lens_border`.
- **Ego body:** Chỉ tạo `ignore_region` với `reason=ego_body` ở frame thực sự nhìn thấy phần thân xe; không suy đoán phần không nhìn thấy.
- **Lens border:** Hai polygon `lens_border` từ prefill cần được kiểm lại theo vùng vòng kính thực tế trên từng frame.
- **Giới hạn:** Đây là dữ liệu từ một camera; không dùng slice này để suy ra đầy đủ hành vi của hệ SVM bốn camera hoặc thông số calibration của rig.