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

# Đổi tên app flutter
### Thay đổi tên trong file AndroidManifest.xml (cho Android)
Mở file android/app/src/main/AndroidManifest.xml và tìm dòng sau:
```
<application
    android:label="Tên Ứng Dụng Cũ"
    ...
    >
```
Thay đổi giá trị của thuộc tính android:label thành tên mới cho ứng dụng của bạn.
### Thay đổi tên trong file Info.plist (cho iOS)
Mở file ios/Runner/Info.plist và tìm dòng sau:
```
<key>CFBundleDisplayName</key>
<string>Tên Ứng Dụng Cũ</string>
```
Thay đổi giá trị của <string> thành tên mới cho ứng dụng của bạn.

# Đổi icon app
Xem chi tiết [tại đây](https://pub.dev/packages/flutter_launcher_icons)
