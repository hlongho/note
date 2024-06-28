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
Thay đổi giá trị cũ <string> thành tên mới cho ứng dụng của bạn.

# Đổi icon app
Xem chi tiết [tại đây](https://pub.dev/packages/flutter_launcher_icons)
