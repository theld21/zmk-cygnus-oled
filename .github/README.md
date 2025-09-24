# GitHub Actions cho ZMK Cygnus OLED

Repository này đã được cấu hình với GitHub Actions để tự động build firmware mỗi khi có commit.

## Workflows có sẵn

### 1. Test Build (test-build.yml) - **RECOMMENDED FOR TESTING**

- **Trigger**: Manual trigger (workflow_dispatch)
- **Chức năng**: Test build một configuration để kiểm tra setup
- **Output**: Test UF2 file
- **Sử dụng**: Chạy trước để đảm bảo mọi thứ hoạt động

### 2. Simple Build (simple-build.yml) - **RECOMMENDED FOR PRODUCTION**

- **Trigger**: Tự động chạy khi push/PR vào main/master
- **Chức năng**: Build tất cả configurations tuần tự
- **Output**: Tất cả UF2 và HEX files
- **Artifacts**:
  - `zmk-cygnus-all-uf2`
  - `zmk-cygnus-all-hex`

### 3. Final Build (final-build.yml) - **ADVANCED**

- **Trigger**: Tự động chạy khi push/PR vào main/master
- **Chức năng**: Build song song với matrix strategy
- **Output**: UF2 và HEX files riêng cho từng configuration
- **Artifacts**:
  - `cygnus_central_dongle-uf2`
  - `cygnus_central_left-uf2`
  - `cygnus_peripheral_left-uf2`
  - `cygnus_peripheral_right-uf2`
  - `settings_reset-uf2`
  - `cygnus_central_dongle_with_logging-uf2`

## Cách sử dụng

### 1. Test trước (RECOMMENDED)

1. Vào tab "Actions"
2. Chọn "Test ZMK Build"
3. Click "Run workflow"
4. Kiểm tra kết quả

### 2. Build production

1. Push code lên branch main/master
2. GitHub Actions sẽ tự động chạy
3. Vào tab "Actions" để xem tiến trình
4. Download artifacts từ build results

### 3. Manual build

1. Vào tab "Actions"
2. Chọn "Simple ZMK Build"
3. Click "Run workflow"
4. Chọn branch và click "Run workflow"

## Cấu trúc Artifacts

Mỗi build sẽ tạo ra:

- **UF2 files**: Để flash vào keyboard
- **HEX files**: Để flash bằng programmer
- **Release archive**: Tất cả files trong một file zip

## Troubleshooting

### Build fails với "source directory app does not exist"

- **Nguyên nhân**: ZMK project chưa được khởi tạo đúng cách
- **Giải pháp**: Sử dụng "Test Build" trước để kiểm tra setup

### Build fails

- Kiểm tra logs trong GitHub Actions
- Đảm bảo config files đúng format
- Kiểm tra dependencies trong west.yml

### Missing artifacts

- Artifacts được giữ trong 30 ngày (UF2/HEX) hoặc 90 ngày (release)
- Download ngay sau khi build hoàn thành

## Cấu hình

Workflows sử dụng:

- Ubuntu Latest
- Python 3.11
- West tool
- Zephyr SDK

Matrix build dựa trên file `build.yaml` trong root directory.

## Thứ tự khuyến nghị

1. **Test Build** - Kiểm tra setup
2. **Simple Build** - Build production
3. **Final Build** - Nếu cần matrix build
