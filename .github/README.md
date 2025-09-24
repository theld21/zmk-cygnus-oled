# GitHub Actions cho ZMK Cygnus OLED

Repository này đã được cấu hình với GitHub Actions để tự động build firmware mỗi khi có commit.

## Workflows có sẵn

### 1. Build ZMK Firmware (build.yml)

- **Trigger**: Tự động chạy khi push/PR vào main/master
- **Chức năng**: Build tất cả configurations song song
- **Output**: UF2 và HEX files cho từng configuration
- **Artifacts**:
  - `cygnus_central_dongle-uf2`
  - `cygnus_central_left-uf2`
  - `cygnus_peripheral_left-uf2`
  - `cygnus_peripheral_right-uf2`
  - `settings_reset-uf2`
  - `cygnus_central_dongle_with_logging-uf2`

### 2. Quick Build (quick-build.yml)

- **Trigger**: Manual trigger (workflow_dispatch)
- **Chức năng**: Build nhanh tất cả configurations
- **Output**: Tất cả UF2 và HEX files trong một artifact

## Cách sử dụng

### Tự động build

1. Push code lên branch main/master
2. GitHub Actions sẽ tự động chạy
3. Vào tab "Actions" để xem tiến trình
4. Download artifacts từ build results

### Manual build

1. Vào tab "Actions"
2. Chọn "Quick Build"
3. Click "Run workflow"
4. Chọn branch và click "Run workflow"

## Cấu trúc Artifacts

Mỗi build sẽ tạo ra:

- **UF2 files**: Để flash vào keyboard
- **HEX files**: Để flash bằng programmer
- **Release archive**: Tất cả files trong một file zip

## Troubleshooting

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
