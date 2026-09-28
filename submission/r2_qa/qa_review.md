# QA review · B2-center

Mã khóa: 1306-1794

Đây là cold review cá nhân sau khi đã khóa bản r1_craft; chưa mở teaching reference/model của B2-center.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_062370.jpg | L7 | R04 | Box đang gán Truck nhưng phương tiện nhìn giống van chở người hoặc minibus; cần kiểm lại ánh xạ class theo R04. |
| adasind_062370.jpg | L2 | R03 | Box Bike bao cả người và xe hai bánh; cần kiểm người đang ngồi lái hay đứng/dắt xe để áp dụng đúng quy tắc rider. |
| adasind_062370.jpg | L4 | R05 | ThreeWheeler nằm sát mép trái và phần vật có vẻ bị biên ảnh cắt; cần kiểm thuộc tính truncated. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
