# Tạo package flutter
```
flutter create --template=package package_name
```
Xem chi tiết [tại đây](https://mobisoftinfotech.com/resources/blog/how-to-create-packages-for-flutter-a-developers-guide/)
# Đưa package lên pub.dev
### Chạy thử nghiệm
```
dart pub publish --dry-run
```
hoặc
```
flutter packages pub publish --dry-run
```
### Xuất bản
```
dart pub publish
```
hoặc
```
flutter packages pub publish
```
Khi cần update version thì chỉ cần điều chỉnh code và version trong **pubspec.yaml**

Xem chi tiết [tại đây](https://viblo.asia/p/flutter-huong-dan-dua-plugin-len-pubdev-LzD5dMjoKjY)
