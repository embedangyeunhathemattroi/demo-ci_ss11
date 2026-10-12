# Bài 3: Gradle Dependency Caching

Đã thêm cache: 'gradle' vào bước actions/setup-java@v5
để lưu và khôi phục cache Gradle giữa các lần chạy.

## Kết quả so sánh

| Nội dung | Lần 1: chưa khôi phục cache | Lần 2: đã khôi phục cache |
|---|---|---|
| Thời gian setup-java | 1 giây | 5 giây |
| Thời gian ./gradlew test | 42 giây | 15 giây |
| Tổng thời gian job | 63 giây | 89 giây |
| Trạng thái job | Success | Success |

## Log xác nhận cache ở lần 2

Cache restored from key: setup-java-Linux-x64-gradle-05f84ce06572e9688903daf690ec63ac23438fb5bdd77788bd98f28d1af8e37a

## Link các lần chạy

- Lần 1: https://github.com/embedangyeunhathemattroi/demo-ci_ss11/actions/runs/38255020804
- Lần 2: https://github.com/embedangyeunhathemattroi/demo-ci_ss11/actions/runs/38255049021

## Nhận xét

Lần chạy thứ hai đã khôi phục cache Gradle.

Thời gian chạy ./gradlew test giảm từ 42 giây xuống
15 giây, giảm 27 giây, tương đương khoảng 64,3%.

Thời gian setup-java tăng từ 1 giây lên 5 giây.

Tổng thời gian job tăng từ 63 giây lên 89 giây,
tăng 26 giây, tương đương khoảng 41,3%.
Như vậy, bước kiểm thử nhanh hơn nhưng tổng thời gian
job chưa giảm trong hai lần đo này. Cần xem thời gian
các bước còn lại để xác định nguyên nhân.

Cả hai lần chạy đều có trạng thái Success.