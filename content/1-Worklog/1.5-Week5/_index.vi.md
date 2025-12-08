---
title: "Worklog Tuần 5"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

## Mục tiêu Tuần 5

- Hiểu về **Mô hình Trách nhiệm Chia sẻ** và ranh giới bảo mật nào AWS xử lý so với những gì bạn phải xử lý.
- Học cách quản lý quyền hạn và danh tính sử dụng **AWS IAM**, bao gồm các chính sách, vai trò và nguyên tắc đặc quyền tối thiểu.
- Khám phá **Amazon Cognito** để xác thực người dùng và cách nó tích hợp với các ứng dụng hiện đại.
- Nghiên cứu **AWS Organizations** và **AWS Identity Center (SSO)** cho việc quản lý đa tài khoản và quản trị tập trung.
- Học cách mã hóa hoạt động trong AWS thông qua **AWS Key Management Service (KMS)** và tại sao việc xử lý khóa đúng cách lại quan trọng.

---

## Nhiệm vụ cần thực hiện trong tuần này

| Ngày | Nhiệm vụ                                                                                                                                                                                                            | On-site? | Ngày       |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| 1    | - Nghiên cứu sâu về **Mô hình Trách nhiệm Chia sẻ** <br> - Hiểu về ranh giới bảo mật: bảo mật **của** AWS trên cloud vs bảo mật **trong** cloud của bạn <br> - Xem xét hậu quả thực tế của việc cấu hình sai        |          | 10/06/2025 |
| 2    | - Học các khái niệm cốt lõi của **IAM**: Người dùng, Nhóm, Vai trò, Chính sách <br> - Thực hành viết chính sách IAM bằng JSON <br> - Khám phá ranh giới quyền hạn, đặc quyền tối thiểu và logic đánh giá chính sách |          | 10/07/2025 |
| 3    | - Giới thiệu về **Amazon Cognito** <br> - Hiểu về User Pools vs Identity Pools <br> - Triển khai quy trình xác thực ứng dụng cơ bản (đăng ký, đăng nhập, token)                                                     |          | 10/08/2025 |
| 4    | - Học **AWS Organizations**: cấu trúc đa tài khoản, thiết kế OU, SCPs <br> - Khám phá **AWS Identity Center** cho truy cập tập trung và SSO                                                                         |          | 10/09/2025 |
| 5    | - Tìm hiểu sâu về **AWS KMS** <br> - Học về CMKs, chính sách khóa, ngữ cảnh mã hóa <br> - Thực hành mã hóa/giải mã dữ liệu và hiểu về mã hóa envelope                                                               |          | 10/10/2025 |
| 6    | - Kết hợp tất cả khái niệm: xây dựng mô hình quản trị đa tài khoản bảo mật <br> - Tạo vai trò IAM cho truy cập ứng dụng, thực thi SCPs và mã hóa tài nguyên với KMS                                                 |          | 10/11/2025 |

---

## Thành tựu Tuần 5

- **Hiểu được Mô hình Trách nhiệm Chia sẻ**:

  - Phân tích chính xác ranh giới bảo mật giữa AWS và khách hàng.
  - Xác định các điểm lỗi thông thường do hiểu sai về những ranh giới này.
  - Học được tại sao việc cấu hình sai thường quan trọng hơn lỗi cơ sở hạ tầng.

- **Thành thạo nền tảng IAM**:

  - Viết chính sách IAM và debug việc từ chối truy cập bằng logic đánh giá chính sách.
  - Học khi nào sử dụng vai trò thay vì thông tin xác thực tồn tại lâu dài.
  - Áp dụng nguyên tắc đặc quyền tối thiểu trên các môi trường test.

- **Triển khai xác thực hiện đại với Cognito**:

  - Học cách Cognito xử lý danh tính người dùng, luồng OAuth và phát hành token.
  - Nghiên cứu các mẫu tích hợp cho ứng dụng web và mobile.
  - Hiểu được các lỗ hổng bảo mật khi tự triển khai xác thực.

- **Khám phá AWS Organizations & Identity Center**:

  - Thiết kế Organization Units và áp dụng Service Control Policies (SCPs).
  - Quản lý danh tính tập trung với SSO cho nhiều tài khoản AWS.
  - Hiểu các mô hình quản trị được sử dụng bởi các doanh nghiệp lớn.

- **Học quản lý khóa bảo mật với KMS**:

  - Hiểu cách AWS quản lý khóa mã hóa và tại sao mã hóa envelope là tiêu chuẩn.
  - Thực hành mã hóa tài nguyên và kiểm soát truy cập với chính sách khóa.
  - Khám phá khóa đa vùng, xoay vòng tự động và kiểm toán với CloudTrail.
