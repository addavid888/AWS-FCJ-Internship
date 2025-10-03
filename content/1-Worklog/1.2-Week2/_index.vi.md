---
title: "Worklog Tuần 2"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu Tuần 2:

- Hiểu sâu hơn về **các nguyên tắc cơ bản về mạng AWS** (VPC, Subnets, Route Tables, IGW).
- Học cách thiết kế và cấu hình **VPC tùy chỉnh** với cả public và private subnets.
- Thực hành quản lý kết nối: thiết lập **route entries**, gắn **Internet Gateway**, và liên kết **Elastic IPs**.
- Khám phá **Elastic Network Interfaces (ENI)** và **VPC Endpoints** để kết nối an toàn với các dịch vụ AWS.
- Củng cố kỹ năng kết hợp **AWS Management Console** và **AWS CLI** để quản lý tài nguyên song song.

### Các công việc cần thực hiện trong tuần này:

| Ngày | Công việc                                                                                                                                                                                                         | On-site? | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------ | --------------- | ------------------ |
| 1    | - Ôn tập quy định thực tập & thiết lập tài khoản AWS cơ bản <br> - Tìm hiểu về **hạ tầng toàn cầu AWS** (Regions, Availability Zones, Edge Locations)                                                             | ✅       | 09/15/2025   |                 |                    |
| 2    | - Giới thiệu về **Amazon VPC** và tại sao mạng lại quan trọng trong AWS <br> - Hiểu về CIDR blocks và IPv4 vs IPv6 <br> - Tạo VPC đơn giản với subnet mặc định                                                    |          | 09/16/2025   |                 |                    |
| 3    | - Tìm hiểu về **Subnets** (Public vs Private) <br> - Các IP được bảo lưu trong subnets <br> - Thực hành tạo nhiều subnets trong các Availability Zones khác nhau                                                  |          | 09/17/2025   |                 |                    |
| 4    | - Nghiên cứu **Route Tables**: mặc định vs tùy chỉnh <br> - Cấu hình routes cho giao tiếp nội bộ VPC <br> - Thêm route entry để cho phép truy cập internet (0.0.0.0/0 → IGW)                                      |          | 09/18/2025   |                 |                    |
| 5    | - Tìm hiểu về **Internet Gateway (IGW)** và cách nó kết nối VPCs với internet <br> - Khám phá **Elastic IPs (EIP)** và các cân nhắc về tính phí <br> - Thực hành gắn EIP vào một instance EC2                     |          | 09/19/2025   |                 |                    |
| 6    | - Hiểu về **Elastic Network Interfaces (ENI)** và tính di động của chúng <br> - Tìm hiểu về **VPC Endpoints** (Interface vs Gateway) <br> - Khám phá các trường hợp sử dụng thực tế cho private vs public traffic |          | 09/20/2025   |                 |                    |

### Kết quả đạt được Tuần 2

- Hiểu được các Dịch vụ Mạng AWS và vai trò của chúng trong hạ tầng cloud:

  - Amazon VPC (Virtual Private Cloud)
  - Subnets (Public & Private)
  - Route Tables
  - Internet Gateway (IGW)
  - Elastic Network Interface (ENI)
  - Elastic IP (EIP)
  - VPC Endpoints (Interface & Gateway)

- Học cách tạo và cấu hình VPC:

  - Định nghĩa dải CIDR (`10.10.0.0/16` cho VPC, `10.10.x.0/24` cho subnets).
  - Phân biệt giữa _public subnets_ (có routes IGW) và _private subnets_.
  - Hiểu về việc bảo lưu IP trong subnet (network, broadcast, router, DNS, sử dụng tương lai).

- Thực hành làm việc với Route Tables:

  - Xác định route table mặc định và vai trò của nó trong giao tiếp nội bộ VPC.
  - Tạo và chỉnh sửa các route tables tùy chỉnh.
  - Thêm các route entries (ví dụ: `0.0.0.0/0 → IGW`) để cho phép truy cập internet của public subnet.

- Khám phá Elastic Network Interface (ENI) và Elastic IP (EIP):

  - Hiểu rằng ENI có thể được di chuyển giữa các instance EC2 trong khi vẫn giữ IP và MAC.
  - Liên kết Elastic IP tĩnh với ENI để có thể truy cập internet.
  - Tìm hiểu về việc AWS tính phí cho các EIP không sử dụng để tránh lãng phí.

- Có kiến thức về Internet Gateway (IGW):

  - Vai trò là gateway có khả năng mở rộng ngang do AWS quản lý để kết nối internet.
  - Các bước: Tạo IGW → Gắn vào VPC → Thêm route trong Route Table → Liên kết với Public Subnet.
  - Hiểu cách tiếp cận đơn giản hóa so với các thiết bị mạng truyền thống.

- Phân tích Topo VPC bằng sơ đồ:

  - Xác định mối quan hệ giữa VPCs, Availability Zones, và subnets.
  - Theo dõi kết nối EC2 thông qua ENI, Route Table, và IGW.
  - Phân biệt cách private vs. public subnets tương tác với lưu lượng bên ngoài.

- Có được mô hình tinh thần rõ ràng về cách các thành phần mạng AWS kết hợp với nhau để hỗ trợ các kịch bản thực tế (web servers công cộng, cơ sở dữ liệu riêng tư, kết nối hybrid, v.v.).
