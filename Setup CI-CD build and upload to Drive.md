# Thiết lập một pipeline CI/CD với GitHub Actions để xây dựng APK cho ứng dụng Flutter và lưu trữ vào Google Drive

## Bước 1: Tạo kho lưu trữ GitHub và thêm mã nguồn Flutter
1. Tạo một kho lưu trữ mới trên GitHub nếu bạn chưa có.
2. Đẩy mã nguồn Flutter của bạn lên kho lưu trữ này.

## Bước 2: Thiết lập GitHub Actions
1. Tạo thư mục .github/workflows trong gốc của kho lưu trữ của bạn.
2. Tạo một tệp YAML mới trong thư mục này, ví dụ flutter.yml.

## Bước 3: Cấu hình tệp YAML cho GitHub Actions
Dưới đây là một mẫu tệp flutter.yml:
```
name: Build Flutter APK

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      #1 Checkout repository
      - name: Checkout Repository
        uses: actions/checkout@v3

        #2 setup java
      - name: Set Up Java
        uses: actions/setup-java@v3.12.0
        with:
          distribution: 'oracle'
          java-version: '17'

      - name: Set up Flutter
        uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.19.0'
          channel: 'stable'

      - name: Install dependencies
        run: flutter pub get

      - name: Build APK
        run: flutter build apk --release

      - name: Upload APK to Google Drive
        env:
          GDRIVE_CREDENTIALS: ${{ secrets.GDRIVE_CREDENTIALS }}
          GDRIVE_FOLDER_ID: ${{ secrets.GDRIVE_FOLDER_ID }}
        run: |
          sudo apt-get install -y python3-pip
          pip3 install google-api-python-client google-auth-httplib2 google-auth-oauthlib
          python3 upload_to_gdrive.py
```
## Bước 4: Thiết lập thông tin đăng nhập API của Google Drive
### 1. Tạo tài khoản dịch vụ trên Google Cloud
#### Truy cập Google Cloud Console:

[Mở Google Cloud Console](https://console.cloud.google.com/?hl=vi).
#### Tạo dự án mới:
Nhấn vào menu dự án ở phía trên cùng của trang, sau đó nhấn "New Project" và điền thông tin cần thiết.
#### Kích hoạt Google Drive API:

- Vào "APIs & Services" > "Library".
- Tìm kiếm "Google Drive API" và nhấn vào "Enable".
#### Tạo thông tin đăng nhập:

- Đi tới "APIs & Services" > "Credentials".
- Nhấn "Create Credentials" và chọn "Service account".
- Điền thông tin cho tài khoản dịch vụ và tạo nó.
- Trong bước "Create key", chọn JSON và nhấn "Create". Tệp JSON sẽ được tải xuống máy tính của bạn.
### 2. Tạo và chia sẻ thư mục Google Drive
#### Tạo thư mục trên Google Drive:

- Mở Google Drive.
- Nhấn "New" > "Folder" và đặt tên cho thư mục.
#### Chia sẻ thư mục với tài khoản dịch vụ:

- Nhấp chuột phải vào thư mục và chọn "Share".
- Nhập email của tài khoản dịch vụ từ tệp JSON (email thường có dạng [email protected]).
- Đặt quyền "Editor" và nhấn "Send".
#### Lấy ID của thư mục:

Mở thư mục và sao chép phần ID từ URL của thư mục (chuỗi ký tự sau folders/).
### 3. Thêm thông tin đăng nhập vào GitHub Secrets
#### Mở kho lưu trữ trên GitHub:

Truy cập vào kho lưu trữ của bạn trên GitHub.
#### Đi tới "Settings":

Nhấn vào "Settings" ở góc phải trên cùng.
#### Thêm Secrets:

- Trong "Settings", chọn "Secrets and variables" > "Actions".
- Nhấn "New repository secret".
#### Thêm GDRIVE_CREDENTIALS:

- Tên secret: GDRIVE_CREDENTIALS.
- Giá trị: Mở tệp JSON đã tải xuống và sao chép toàn bộ nội dung vào đây.
- Nhấn "Add secret".
#### Thêm GDRIVE_FOLDER_ID:

- Tên secret: GDRIVE_FOLDER_ID.
- Giá trị: Dán ID của thư mục Google Drive.
- Nhấn "Add secret".
## Bước 5: Tạo tập lệnh Python để tải lên Google Drive
Tạo một tập lệnh Python có tên upload_to_gdrive.py trong gốc của kho lưu trữ:
```
import json
import os
from google.oauth2.service_account import Credentials
from googleapiclient.discovery import build
from googleapiclient.http import MediaFileUpload

# Load credentials
credentials_info = json.loads(os.environ["GDRIVE_CREDENTIALS"])
credentials = Credentials.from_service_account_info(credentials_info)

# Create the service
service = build('drive', 'v3', credentials=credentials)

# File to upload
file_metadata = {
    'name': 'app-release.apk',
    'parents': [os.environ["GDRIVE_FOLDER_ID"]]
}
media = MediaFileUpload('build/app/outputs/flutter-apk/app-release.apk', mimetype='application/vnd.android.package-archive')

# Upload the file
file = service.files().create(body=file_metadata, media_body=media, fields='id').execute()
print(f"File ID: {file.get('id')}")
```

## Bước 6: Kiểm tra và triển khai
- Đẩy các thay đổi lên kho lưu trữ GitHub.
- Kiểm tra Actions trên GitHub để đảm bảo rằng quá trình xây dựng và tải lên diễn ra suôn sẻ.
