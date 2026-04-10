# Ansible-Network-Automation-Lab
## 🏗️ Kiến trúc hệ thống (Architecture)
* **Control Node:** Vận hành trên môi trường `WSL (Ubuntu)` với công cụ `Ansible` được cài đặt.
* **Managed Nodes:** 02 thiết bị mạng Cisco Router được mô phỏng trên nền tảng `GNS3`.
* **Kênh truyền thông (Connectivity):** Sử dụng giải pháp `Tailscale VPN` để thiết lập mạng LAN ảo (Tailnet), cho phép Control Node quản trị thiết bị từ xa qua giao thức SSH một cách an toàn và xuyên suốt.

---

## 📂 Cấu trúc thư mục (Project Structure)
Dự án được tổ chức theo tiêu chuẩn Best Practices dành cho Ansible Automation:

    Ansible-Network-Automation-Lab/
    ├── ansible.cfg          # Cấu hình môi trường Ansible (tắt host_key_checking)
    ├── hosts.ini            # File Inventory chứa định tuyến IP của các thiết bị mạng
    ├── README.md            # Tài liệu dự án
    ├── group_vars/
    │   └── routers.yml      # Lưu trữ biến hệ thống tập trung (thông tin xác thực SSH, loại OS)
    ├── playbooks/           # Khu vực làm việc chính: Chứa các kịch bản tự động hóa (.yml)
    │   ├── setup_network.yml
    │   └── backup_configs.yml
    └── backups/             # Kho lưu trữ các bản sao lưu cấu hình (.txt) được xuất về từ Router

---

## ⚙️ Yêu cầu môi trường (Prerequisites)
Để tham gia phát triển và vận hành kịch bản cấu hình, các thành viên cần đảm bảo:
1. Máy tính cá nhân có môi trường Linux (Khuyến nghị cài đặt **WSL Ubuntu** trên Windows).
2. Đã cài đặt core **Ansible** (`sudo apt install ansible`).
3. Đã cài đặt và xác thực tham gia vào mạng **Tailnet** của nhóm thông qua Tailscale.
4. Môi trường hạ tầng GNS3 (Host Lab) phải đang ở trạng thái **Online**.

---

## 🚀 Hướng dẫn sử dụng (How to Run)

**Bước 1: Đồng bộ mã nguồn và cấu hình IP mới nhất**

    git pull origin main

**Bước 2: Kiểm tra khả năng thông mạng (Ping Test)**

    ansible routers -m ping

**Bước 3: Thực thi kịch bản tự động hóa (Deploy/Run)**
*(Ví dụ minh họa: Chạy Playbook tiến hành sao lưu toàn bộ cấu hình mạng)*

    ansible-playbook playbooks/backup_configs.yml
