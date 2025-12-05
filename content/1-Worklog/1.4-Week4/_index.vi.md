---
title: "Worklog Tuần 4"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

# Chương Trình Tuần 4: Dịch Vụ Lưu Trữ Cốt Lõi và Các Khái Niệm

## Mục Tiêu Tuần 4

- Hiểu cách **Amazon S3** hoạt động như một dịch vụ lưu trữ đối tượng quy mô toàn cầu.
- Học cách quản lý quyền truy cập S3 sử dụng **Access Points**, **Bucket Policies**, **IAM**, và **CORS**.
- Khám phá **S3 Storage Classes**, bao gồm chuyển đổi vòng đời và tối ưu hóa chi phí.
- Thực hành thiết lập **S3 Static Websites**, cấu hình CORS, và điều chỉnh hiệu suất với **thiết kế khóa đối tượng**.
- Học cách lưu trữ và truy xuất dữ liệu dài hạn sử dụng **S3 Glacier** và các cấp độ truy xuất.
- Hiểu các giải pháp lưu trữ lai: **Snow Family** cho các thiết bị truyền dữ liệu và **Storage Gateway** cho tích hợp tại chỗ.
- Làm quen cơ bản với AWS **Backup** cho quản lý sao lưu tự động tập trung qua các dịch vụ.

---

## Các Nhiệm Vụ Thực Hiện Trong Tuần

| Ngày | Nhiệm Vụ                                                                                                                                                                                                                                      | Tại văn phòng? | Ngày       |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ---------- |
| 1    | - Giới thiệu các khái niệm cơ bản **Amazon S3** <br> - Hiểu về đối tượng, bucket, vùng, tính nhất quán dữ liệu <br>- Nghiên cứu **S3 Access Points**, chính sách bucket, và mô hình kiểm soát truy cập                                        |                | 09/29/2025 |
| 2    | - Học **S3 Storage Classes** (Standard, IA, One Zone, Intelligent Tiering, các cấp Glacier) <br> - Khám phá quy tắc vòng đời và lập kế hoạch lưu trữ tối ưu chi phí                                                                           | ✅             | 09/30/2025 |
| 3    | - Thiết lập **S3 Static Website** <br> - Cấu hình **CORS** cho ứng dụng web <br> - Hiểu cài đặt truy cập công khai và các cân nhắc bảo mật                                                                                                    |                | 10/01/2025 |
| 4    | - Học **chiến lược đặt tên khóa đối tượng S3** và cách chúng ảnh hưởng đến hiệu suất <br> - Khám phá **multipart upload**, phiên bản, và các tùy chọn sao chép                                                                                |                | 10/02/2025 |
| 5    | - Tìm hiểu sâu về **S3 Glacier** và các cấp độ truy xuất <br> - Thực hành tạo vault, tải lên archive, và yêu cầu khôi phục                                                                                                                    |                | 10/03/2025 |
| 6    | - Khám phá lưu trữ lai và biên: thiết bị **Snow Family** cho truyền dữ liệu quy mô lớn <br> - Học các trường hợp sử dụng **AWS Storage Gateway** (File/Volume/Tape Gateway) <br> - Giới thiệu **AWS Backup** cho điều phối sao lưu đa dịch vụ |                | 10/04/2025 |

---

## Thành Tựu Tuần 4

- **Hiểu Kiến Trúc Lưu Trữ Đối Tượng S3**:

  - Học cách bucket và đối tượng có thể truy cập toàn cầu qua URL duy nhất.
  - Hiểu tính nhất quán đọc-sau-ghi mạnh mẽ và thiết kế phân tán của S3.
  - Khám phá Access Points để truy cập dữ liệu đơn giản và có kiểm soát ở quy mô lớn.

- **Có Cái Nhìn Sâu Sắc về S3 Storage Classes**:

  - So sánh chi phí, độ bền, và thời gian truy xuất qua các lớp (Standard, IA, One Zone, Intelligent Tiering, họ Glacier).
  - Thiết kế quy tắc vòng đời cho chuyển đổi và xóa tự động.
  - Hiểu các tình huống sử dụng lưu trữ lưu trữ.

- **Cấu Hình S3 Static Hosting và CORS**:

  - Thiết lập lập chỉ mục trang web, trang lỗi, và cài đặt truy cập công khai.
  - Cấu hình CORS cho các yêu cầu cross-origin từ ứng dụng web.
  - Hiểu rủi ro bảo mật của truy cập công khai cấu hình sai.

- **Học về Đặt Tên Khóa, Hiệu Suất, và Quản Lý Dữ Liệu**:

  - Nghiên cứu tính song song yêu cầu của S3 và tác động của phân phối khóa.
  - Thực hành multipart upload cho các tệp lớn.
  - Cấu hình phiên bản đối tượng và sao chép (CRR/SRR).

- **Khám Phá Glacier và Lưu Trữ Dài Hạn**:

  - Tạo archive và yêu cầu truy xuất qua các cấp độ truy xuất khác nhau.
  - Hiểu các trường hợp sử dụng cho lưu trữ lạnh, không thường xuyên, và lưu trữ sâu.

- **Hiểu Dịch Vụ Lưu Trữ Lai**:

  - Học về **Snowcone, Snowball, Snowmobile** và vai trò của chúng trong truyền dữ liệu số lượng lớn.
  - Khám phá **Storage Gateway** để kết nối các hệ thống tại chỗ với lưu trữ đám mây bằng giao diện file, volume, hoặc tape.
  - Có kiến thức cơ bản về **AWS Backup** cho sao lưu tự động dựa trên chính sách qua các dịch vụ AWS.

- Phát triển hiểu biết vững chắc về **cách lưu trữ đối tượng, lưu trữ, và lưu trữ lai kết hợp với nhau** trong AWS, tạo nền tảng cho quản lý dữ liệu có thể mở rộng, hiệu quả chi phí, và bảo mật.
