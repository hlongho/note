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
Thay đổi giá trị cũ <string> thành tên mới cho ứng dụng của bạn.

# Đổi icon app
Xem chi tiết [tại đây](https://pub.dev/packages/flutter_launcher_icons)

# Tạo một API tĩnh với github
Dưới đây là một ví dụ đơn giản sử dụng GitHub Pages để tạo một API tĩnh:

### Tạo repository:
Tạo một repository mới trên GitHub, ví dụ: my-static-api.

### Tạo dữ liệu JSON:
Tạo một file data.json trong repository với nội dung JSON mà bạn muốn cung cấp qua API.

### Enable GitHub Pages:
Vào phần Settings của repository, tìm phần GitHub Pages, chọn source là main branch và thư mục gốc / (nếu bạn sử dụng thư mục khác, hãy chọn đúng thư mục đó).
Truy cập API:

Sau khi GitHub Pages đã được kích hoạt và deploy thành công, bạn có thể truy cập dữ liệu JSON của bạn qua URL dạng https://username.github.io/my-static-api/data.json.
