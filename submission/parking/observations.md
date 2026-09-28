
# Parking observations

- Tôi chọn các đoạn sơn trắng ở tiền cảnh làm `parking_line` vì chúng tạo ranh giới giữa các ô đỗ riêng biệt.
- Tôi đã vẽ nhiều hơn mức tối thiểu để thể hiện rõ các ranh giới ô đỗ nhìn thấy trên ảnh.
- Tôi không gán các vạch trắng nằm xa ở khu vực lối xe chạy làm `parking_line`, vì không đủ căn cứ cho rằng chúng là ranh giới của từng ô đỗ.
- `free_space` được vẽ trên phần mặt đường trống nhìn thấy của lối xe chạy và không đi xuyên qua chiếc xe, curb hay vật cản rõ ràng.
- Polygon `free_space` chỉ mô tả vùng mặt đường trống nhìn thấy trên ảnh tĩnh, không được hiểu là vùng lái xe an toàn.
- Ca cần lưu ý: một số vạch ở xa khó xác định chắc chắn là vạch ô đỗ hay vạch phục vụ lối xe chạy, nên tôi không dùng các vạch đó làm căn cứ chính.
