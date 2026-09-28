# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_062370.jpg
- L7+R4 mid WRONG_CLASS
- R7 center MISSING
- R8 center MISSING
## adasind_086220.jpg
- L7+R1 mid ATTRIBUTE
- L1 center SPURIOUS
- L4 center SPURIOUS
## adasind_117120.jpg
- L2 center SPURIOUS
- L8 center SPURIOUS
- L9 center SPURIOUS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 13 | 11 | 2 | 5 |
| mid | 6 | 5 | 1 | 1 |
| edge | 1 | 1 | 0 | 0 |
