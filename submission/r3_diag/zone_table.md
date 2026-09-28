# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 13 | 2 | 5 | 7 | 10 | SPURIOUS (5) |
| mid | 6 | 1 | 1 | 3 | 5 | WRONG_CLASS (1) |
| edge | 1 | 0 | 0 | 0 | 1 | — |

## Nhận xét

- `center` có số khác biệt tuyệt đối nhiều nhất: L có 2 missing + 5 spurious; M có 7 missing + 10 thừa. `mid` thấp hơn và `edge` chỉ có 1 M-only. Tuy nhiên số reference giữa các zone không cân bằng (center=13, mid=6, edge=1), nên không thể coi số đếm tuyệt đối là tỷ lệ lỗi trực tiếp.
- Ở IoU 0.30 và 0.50 kết quả ghép của L không đổi; khi tăng lên 0.70, matched center của L giảm từ 11 xuống 9 và của M giảm từ 6 xuống 2. Điều này cho thấy một số box, đặc biệt phía model, nhạy với ngưỡng hình học cao hơn.
- Truck và Bus có precision/recall thấp trong slice này, nhưng số mẫu rất nhỏ nên không được suy rộng thành chất lượng chung của hai class.
- Giả thuyết cần kiểm thêm: mật độ vật thể, che khuất, kích thước nhỏ và biến dạng fisheye có thể góp phần tạo khác biệt. Slice chỉ gồm 3 frame nên chưa đủ bằng chứng để kết luận lỗi miền của model hoặc đặc tính chung của hệ SVM.
