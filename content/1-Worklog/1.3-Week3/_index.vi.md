---
title: "Worklog Tuần 3"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3

- Hiểu cách hoạt động của các **Amazon EC2** instance trong hạ tầng AWS.
- Học cách cấu hình và khởi chạy EC2 instance sử dụng **AMI**, **Instance Types**, và **Key Pairs**.
- Khám phá mối quan hệ giữa **EC2**, **EBS volumes**, và **Instance Store**.
- Thực hành **tạo snapshot**, **gắn volume**, và **chiến lược backup**.
- Học cách tự động hóa thiết lập EC2 sử dụng **User Data** và truy xuất **Metadata** để cấu hình instance.
- Có kiến thức cơ bản về **EFS** và **FSx** cho lưu trữ file có thể mở rộng và chia sẻ.

---

### Các công việc cần thực hiện trong tuần này

| Ngày | Công việc                                                                                                                                                                                                                                              | On-site? | Ngày       |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ---------- |
| 1    | - Giới thiệu về **Amazon EC2** <br> - Hiểu cách hoạt động của ảo hóa: các lớp **Hardware Node**, **Hypervisor**, và **EC2 Instance** <br> - Khám phá **Instance Types** và tác động của chúng đến hiệu năng CPU, Memory, và Network                    |          | 09/22/2025 |
| 2    | - Tìm hiểu về **AMI (Amazon Machine Image)**: cách chọn và khởi chạy EC2 instance <br> - Hiểu **root volume mapping** và tạo AMI tùy chỉnh <br> - Nghiên cứu **mô hình giá** EC2 (On-demand, Reserved, Spot, Savings Plan)                             | ✅       | 09/23/2025 |
| 3    | - Nghiên cứu **Instance Store**: lưu trữ tạm thời hiệu năng cao dựa trên NVMe <br> - So sánh với **EBS Volumes** và thảo luận về tính bền vững, độ tin cậy, và sao chép <br> - Thực hành khởi chạy instance với Instance Store và EBS                  |          | 09/24/2025 |
| 4    | - Tìm hiểu kiến trúc **EBS (Elastic Block Store)** và cách kết nối với EC2 qua EBS Network <br> - Khám phá **các loại EBS Volume** (SSD, HDD) và độ bền (99.999%) <br> - Thực hiện các thao tác **snapshot** và **restore** EBS                        |          | 09/25/2025 |
| 5    | - Hiểu về **User Data** và **Metadata** <br> - Viết script user-data đơn giản để tự động cài đặt package và thiết lập <br> - Truy xuất metadata EC2 (IP, hostname, security groups) sử dụng `http://169.254.169.254/latest/meta-data/`                 |          | 09/26/2025 |
| 6    | - Khám phá các dịch vụ lưu trữ nâng cao: **EFS (Elastic File System)** và **FSx** <br> - Tìm hiểu use case cho **truy cập file chia sẻ** và **workload hiệu năng cao** <br> - Giới thiệu **AWS Application Migration Service** để di chuyển VM lên AWS |          | 09/27/2025 |

---

### Kết quả đạt được Tuần 3

- **Hiểu được kiến trúc EC2**:

  - EC2 instance chạy trên **lớp hypervisor** (Nitro/KVM) trên các node phần cứng vật lý.
  - Mỗi instance sử dụng **template AMI** để định nghĩa OS và cấu hình.
  - Có cái nhìn sâu sắc về cách instance types định nghĩa năng lực tính toán, bộ nhớ, và mạng.

- **Tìm hiểu về Instance Store vs EBS**:

  - Instance Store cung cấp **lưu trữ NVMe tạm thời, siêu nhanh** gắn với node phần cứng.
  - EBS cung cấp **lưu trữ block bền vững** được sao chép trên các storage node trong một AZ để đảm bảo tin cậy.
  - Hiểu các use case: instance store cho workload IOPS cao, EBS cho độ bền.

- **Khám phá kiến trúc và vận hành EBS**:

  - Nghiên cứu cách EBS kết nối qua **EBS Network chuyên dụng** trong một Availability Zone.
  - Tìm hiểu về **các loại EBS volume** (SSD, HDD), **EBS-optimized instance**, và hỗ trợ **multi-attach**.
  - Thực hành tạo, gắn, tháo, và tạo **snapshot** để backup.

- **Cấu hình EC2 instance và Key Pairs**:

  - Tạo SSH key pair để truy cập an toàn.
  - Kết nối đến EC2 qua public subnet sử dụng SSH.
  - Hiểu về mã hóa key pair và liên kết với private/public subnet.

- **Sử dụng User Data và Metadata để tự động hóa**:

  - Viết bash script để cài đặt package và thiết lập môi trường khi khởi động.
  - Truy cập metadata endpoint để lấy dữ liệu cấu hình (IP, hostname, SG).
  - Học cách tự động hóa provisioning EC2 mà không cần thiết lập SSH thủ công.

- **Làm quen với các dịch vụ lưu trữ cấp cao hơn**:

  - Tổng quan về **EFS** cho hệ thống file POSIX chia sẻ giữa các instance.
  - Tìm hiểu về **FSx** cho workload dựa trên Windows hoặc hiệu năng cao.
  - Khám phá **Application Migration Service** như công cụ di chuyển workload lên AWS.

- Phát triển hiểu biết rõ ràng về **cách các lớp compute và storage tương tác** bên trong AWS Availability Zone, và cách chúng tạo nền tảng cho các dịch vụ cấp cao hơn.
