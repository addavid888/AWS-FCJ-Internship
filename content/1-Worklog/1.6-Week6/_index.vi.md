---
title: "Worklog Tuần 6"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

## Mục tiêu Tuần 6

- Hiểu các **khái niệm cơ sở dữ liệu cốt lõi**: bảng, schema, khóa chính, khóa ngoại, chỉ mục, phân vùng, kế hoạch thực thi truy vấn, nhật ký cơ sở dữ liệu và hành vi buffer/cache.
- Tìm hiểu sự khác biệt giữa cơ sở dữ liệu **quan hệ** và **phi quan hệ**, và nơi mỗi loại phù hợp.
- Phân biệt giữa workload **OLTP** và **OLAP** và cách các lựa chọn thiết kế ảnh hưởng đến hiệu suất.
- Khám phá các dịch vụ cơ sở dữ liệu AWS: **Amazon RDS**, **Amazon Aurora**, **Amazon ElastiCache** và **Amazon Redshift**, bao gồm các trường hợp sử dụng lý tưởng và sự khác biệt về kiến trúc.

---

## Các tác vụ cần thực hiện trong tuần này

| Ngày | Tác vụ                                                                                                                                                                                                                              | On-site? | Ngày       |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| 1    | - Học **kiến thức cơ bản về cơ sở dữ liệu** <br> - Hiểu về bảng, hàng và thiết kế schema <br> - Tìm hiểu **khóa chính** vs **khóa ngoại** và tại sao cần chuẩn hóa                                                                  |          | 10/13/2025 |
| 2    | - Khám phá **chỉ mục**, cách chúng hoạt động và tại sao chúng tăng tốc truy vấn <br> - Học về **phân vùng**, trình lập kế hoạch truy vấn và **kế hoạch thực thi** <br> - Tìm hiểu về nhật ký giao dịch, WAL và hành vi buffer/cache |          | 10/14/2025 |
| 3    | - So sánh cơ sở dữ liệu **quan hệ** vs **phi quan hệ** <br> - Hiểu các cân nhắc CAP và đánh đổi tính nhất quán <br> - Tìm hiểu nơi phù hợp cho document, key-value, graph và wide-column stores                                     |          | 10/15/2025 |
| 4    | - Học về hệ thống **OLTP** (giao dịch) vs **OLAP** (phân tích) <br> - Hiểu cách mô hình hóa dữ liệu khác nhau cho từng loại <br> - Tìm hiểu tại sao các hệ thống phân tích cần lưu trữ theo cột                                     |          | 10/16/2025 |
| 5    | - Giới thiệu **Amazon RDS** và các engine quan hệ được quản lý <br> - Khám phá snapshots, Multi-AZ, backups, storage autoscaling                                                                                                    |          | 10/17/2025 |
| 6    | - Tìm hiểu sâu **Amazon Aurora**, lớp lưu trữ phân tán của nó <br> - Tìm hiểu thiết kế mở rộng đọc hiệu suất cao và failover                                                                                                        |          | 10/18/2025 |
| 7    | - Khám phá **Amazon ElastiCache** (Redis/Memcached) cho caching, sessions và workload độ trễ thấp <br> - Học **Amazon Redshift** cho OLAP và truy vấn phân tích quy mô lớn                                                          |          | 10/19/2025 |

---

## Thành tựu Tuần 6

- **Thành thạo các khái niệm cơ sở dữ liệu cơ bản**:

  - Hiểu cách khóa chính/khóa ngoại thực thi các mối quan hệ.
  - Tìm hiểu cách chỉ mục ảnh hưởng đến hiệu suất và tại sao những chỉ mục được thiết kế kém làm cơ sở dữ liệu "khóc".
  - Phân tích kế hoạch thực thi truy vấn và thấy cách bộ tối ưu hóa quyết định đường dẫn truy cập.
  - Hiểu nhật ký, WAL và quản lý buffer như một phần của tính bền vững và hiệu suất.

- **Phân biệt các loại cơ sở dữ liệu và trường hợp sử dụng**:

  - Đánh giá mô hình quan hệ cho tính nhất quán mạnh và dữ liệu có cấu trúc.
  - Khám phá mô hình phi quan hệ cho schema linh hoạt và mở rộng phân tán.
  - Hiểu khi nào chọn hệ thống OLTP vs OLAP và tại sao việc kết hợp chúng thường là thảm họa.

- **Tìm hiểu các dịch vụ cơ sở dữ liệu được quản lý của AWS**:

  - Sử dụng **Amazon RDS** để quản lý engine quan hệ đơn giản với backups và Multi-AZ.
  - Hiểu tại sao **Aurora** đạt được throughput cao hơn bằng cách sử dụng lớp lưu trữ chia sẻ.
  - Khám phá **ElastiCache** như một hệ thống in-memory để tăng tốc và quản lý trạng thái.
  - Sử dụng **Amazon Redshift** như một warehouse OLAP theo cột được thiết kế cho các truy vấn phân tích phức tạp.
