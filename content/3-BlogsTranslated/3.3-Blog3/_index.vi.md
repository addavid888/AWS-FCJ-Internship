---
title: "Trí tuệ Vị trí hướng tới Vận tải Bền vững trên AWS"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

[Xem bài viết gốc tại đây](https://aws.amazon.com/vi/blogs/apn/location-intelligence-for-sustainable-transportation-on-aws/)

*bởi Mahesh Geeniga, Lev Levine, và Nicolas Legros – 14 THÁNG 5 2025*

*Bởi Mahesh Geeniga, Senior Partner Solutions Architect – AWS, Lev Levine, Principal Partner Development Manager – AWS, Nicolas Legros, Director Product Marketing – HERE Technologies*

Trí tuệ vị trí (Location intelligence), được vận hành bởi dữ liệu địa lý theo thời gian thực, đang cách mạng hóa ngành vận tải và logistics bằng cách cho phép doanh nghiệp tối ưu hóa lộ trình, giảm tiêu thụ nhiên liệu, và giảm thiểu tác động môi trường trong khi vẫn đáp ứng nhu cầu ngày càng tăng của nền kinh tế toàn cầu.

HERE Technologies, hợp tác cùng AWS, mang đến các giải pháp location intelligence tiên tiến, bao gồm smart routing, giám sát giao thông theo thời gian thực, và lập kế hoạch giao hàng last-mile tinh vi. Các giải pháp này giúp công ty giảm khí thải đồng thời tối ưu hóa việc giao hàng, quản lý đội xe, và hiệu suất tổng thể.

Trong bài viết này, bạn sẽ khám phá cách mà các giải pháp bản đồ thế hệ tiếp theo của HERE trên AWS đang giúp doanh nghiệp đạt được mục tiêu bền vững. Các giải pháp này chứng minh rằng doanh nghiệp có thể duy trì hiệu quả vận hành đồng thời có trách nhiệm với môi trường.

**Tối ưu Lộ trình Thông minh**

HERE Technologies, tiên phong trong lĩnh vực location intelligence, dựa vào hạ tầng AWS Cloud cho các giải pháp định tuyến và điều hướng tiên tiến, chẳng hạn như [HERE Fleet Optimization](https://aws.amazon.com/marketplace/seller-profile?id=cc033bc0-fe05-4d79-ba58-9a132b1fe9d3). Các dịch vụ AWS, bao gồm Amazon S3, Amazon EC2, và AWS Batch, cho phép HERE xử lý lượng lớn dữ liệu thời gian thực và lịch sử, biến nó thành thông tin định tuyến tiên tiến.

[HERE Tour Planning API](https://aws.amazon.com/marketplace/pp/prodview-izb3zaa6bhepo) tối ưu hóa toàn bộ đội xe bằng cách tạo lộ trình tiết kiệm cả thời gian lẫn chi phí. Bằng cách sử dụng AWS Graviton processors, [HERE cải thiện hiệu năng API](https://aws.amazon.com/solutions/case-studies/here-technologies-case-study/) đồng thời giảm chi phí cho khách hàng. API này tạo các tuyến cân bằng trong khi tối ưu hóa việc sử dụng phương tiện, bao gồm các ràng buộc vận hành khác nhau như ca làm của tài xế và yêu cầu thời gian công việc cụ thể. Nó có tính năng định tuyến theo thời gian thực nhận biết giao thông, được thiết kế riêng cho xe tải, với khả năng lập kế hoạch lại tuyến động dựa trên vị trí hiện tại của xe. API ghép các yêu cầu công việc cụ thể với khả năng của phương tiện một cách thông minh, ví dụ như vận chuyển cần làm lạnh, đồng thời phối hợp nhiều phương tiện để giảm tổng thời gian và nhiên liệu di chuyển. Thông qua việc xem xét khung giờ giao hàng nghiêm ngặt và điều kiện giao thông & đường xá theo thời gian thực, API cho phép hiệu suất giao hàng đáng tin cậy trong khi vẫn duy trì sự linh hoạt để thích ứng khi điều kiện thay đổi.

Hình 1 cho thấy cách HERE Fleet Optimization giải quyết nhiều vấn đề quản lý đội xe khác nhau.

![image-1](images/3-BlogsTranslated/3.3-/image-1.png)

*Hình 1: Kiến trúc điển hình sử dụng HERE Fleet Optimization*

**Định tuyến Tập trung vào Lượng phát thải dựa trên Trí thông minh theo Thời gian thực**

Hệ thống định tuyến tiên tiến của HERE biến đổi điều hướng truyền thống bằng cách cân bằng hiệu quả môi trường, chi phí, và tốc độ. Nó sử dụng các thuật toán mạnh mẽ để phân tích nhiều biến số thời gian thực nhằm xác định tuyến đường bền vững nhất cho mỗi chuyến đi. Cách tiếp cận thông minh này xem xét rằng ngay cả những biến động nhỏ trong mẫu giao thông, thông số phương tiện, hoặc điều kiện môi trường cũng có thể ảnh hưởng đến tiêu thụ nhiên liệu và khí thải.

Các công cụ định tuyến tiên tiến liên tục xử lý dữ liệu giao thông thời gian thực và cung cấp thông tin định tuyến cập nhật thông qua APIs của HERE. Hệ thống quản lý đội xe sử dụng khả năng định tuyến của HERE có thể chủ động yêu cầu tính toán lại tuyến khi cần thiết, cho phép phản ứng với các thay đổi trong điều kiện đường (như thay đổi quy định giao thông), tai nạn, công trình xây dựng hoặc tình trạng đường khác. Bằng cách triển khai khả năng tái điều hướng và gọi APIs của HERE ở khoảng thời gian thích hợp, hệ thống có thể giúp phương tiện tránh tắc đường và giao thông dừng-đi. Cách tiếp cận này giảm thời gian chờ và tăng tốc không cần thiết – hai nguyên nhân chính gây ra khí thải dư thừa.

Việc tích hợp HERE Real-Time Traffic và các tính năng cảnh báo đường đi giúp tăng cường hệ thống định tuyến thông minh. Các tính năng này cung cấp cập nhật nhanh về tình trạng đường và nguy hiểm tiềm tàng, cho phép phương tiện duy trì tốc độ ổn định và tránh các nút thắt giao thông. Các tùy chọn tuyến khác nhau có thể được đánh giá về hiệu quả nhiên liệu và tác động môi trường thông qua so sánh dự báo khí thải. Hệ thống đánh giá khí thải dự kiến cho các tùy chọn định tuyến khác nhau, so sánh tiêu thụ nhiên liệu và tác động môi trường. Một tuyến được đề xuất có thể trông dài hơn, nhưng khí thải dự báo lại thấp hơn do tránh được vùng tắc nghẽn, cuối cùng mang lại các lựa chọn tuyến đường hiệu quả về môi trường. Phương pháp định tuyến toàn diện này kết hợp dữ liệu giao thông thời gian thực với các đặc điểm riêng của từng phương tiện và các yếu tố môi trường. Bằng cách xem xét các biến số này, doanh nghiệp có thể giảm mức tiêu thụ nhiên liệu, thời gian chạy không tải và lượng khí thải carbon so với các phương pháp định vị truyền thống chỉ tập trung vào thời gian di chuyển hoặc khoảng cách.

**Viễn thông Vận tải (Vehicle Telematics)**

Hệ thống định tuyến của HERE có thể tích hợp với vehicle telematics để giám sát các chỉ số hiệu suất môi trường khi có quyền truy cập [dữ liệu CAN bus](https://en.wikipedia.org/wiki/CAN_bus). Hệ thống có thể phân tích nhiều khía cạnh quan trọng cho các đội xe với dữ liệu phương tiện kết nối, bao gồm dữ liệu tiêu thụ nhiên liệu thực tế từ phương tiện, các hành vi lái xe ảnh hưởng đến hiệu suất và cơ hội tối ưu hóa tuyến & lịch trình. 

Khả năng hiển thị này cho phép quản lý đội xe đưa ra quyết định dựa trên dữ liệu về hiệu quả định tuyến, đào tạo tài xế, và cải tiến vận hành. Các insight này giúp tổ chức đo lường và đạt mục tiêu giảm khí thải.

**Giải pháp Tăng cường Khả năng hiển thị**

Giao hàng chặng cuối (Last Mile Delivery) đặt ra những thách thức đặc thù trong môi trường đô thị, nơi giao thông phức tạp và thường xuyên dừng đỗ ảnh hưởng đáng kể đến lượng khí thải. Tính năng hiển thị lô hàng của HERE kết hợp dữ liệu từ nhiều nguồn theo dõi – bao gồm cảm biến IoT và hệ thống viễn thông – và tăng cường thông tin này với dữ liệu vị trí chính xác. Điều này mang đến cho khách hàng cái nhìn toàn diện về lô hàng của mình bằng cách tích hợp và làm giàu dữ liệu từ nhiều thiết bị và nền tảng theo dõi khác nhau. Quá trình nâng cao này ánh xạ thông tin vị trí đến các vị trí chính xác, cho phép theo dõi tình trạng giao hàng theo thời gian thực so với các tuyến đường và lịch trình đã định.

Nền tảng này đánh giá liệu các chuyến hàng đang chạy đúng giờ, chậm tiến độ hay vượt tiến độ, cho phép các nhà quản lý đội xe theo dõi toàn diện tiến độ giao hàng. Thông qua việc theo dõi vị trí xe và trạng thái giao hàng theo thời gian thực, các nhà quản lý có thể đánh giá việc tuân thủ lịch trình và hiệu suất giao hàng, đồng thời đánh giá sự tuân thủ lộ trình và các biến động thời gian. Khả năng hiển thị này cho phép họ thực hiện các điều chỉnh linh hoạt khi cần thiết để tối ưu hóa hiệu quả giao hàng trên toàn bộ hoạt động. 

Khả năng hiển thị nâng cao này cho phép các nhóm vận hành chủ động giải quyết sự chậm trễ, tối ưu hóa các quyết định về lộ trình và loại bỏ mức tiêu thụ nhiên liệu không cần thiết cho mỗi kiện hàng trên toàn bộ phân khúc giao hàng cuối cùng.

**Quyết định dựa trên thời tiết**

HERE Destination Weather là một dịch vụ động (trực tiếp) cung cấp thông tin thời tiết địa phương chi tiết, cập nhật từng phút, chính xác và theo ngữ cảnh, nhằm nâng cao nhận thức và sự an toàn cho tài xế. Dịch vụ này cung cấp thông tin về điều kiện thời tiết hiện tại, dự báo, cảnh báo thời tiết khắc nghiệt và các điều kiện thay đổi trong suốt hành trình. Bằng cách tích hợp dữ liệu thời tiết chi tiết này vào việc lập kế hoạch tuyến đường, các nhà quản lý đội xe có thể đưa ra quyết định sáng suốt hơn, tránh sự chậm trễ do thời tiết và chi phí nhiên liệu tăng cao. Phương pháp tiếp cận chủ động này giúp tối ưu hóa tuyến đường bằng cách xem xét tác động của thời tiết hiện tại và dự báo đối với điều kiện di chuyển.

**Kết quả khách hàng có thể đo lường được**

Việc triển khai các giải pháp HERE đã chứng minh được giá trị đáng kể về mặt môi trường và kinh doanh, với mức độ lợi ích khác nhau tùy thuộc vào nền tảng của mỗi công ty. Đối với các tổ chức mới làm quen với việc tối ưu hóa tuyến đường dựa trên máy tính, các công nghệ này có thể giúp [giảm tới 20% thời gian tuyến đường](https://aws.amazon.com/partners/success/kovix-here-technologies/), chi phí nhiên liệu và lượng khí thải carbon thông qua việc lập kế hoạch tuyến đường và tối ưu hóa giao hàng hiệu quả. Các công ty đã sử dụng các giải pháp định tuyến số hóa cơ bản thường thấy mức tăng trưởng từ 5-8%, thậm chí có thể đạt tới 10%, khi nâng cấp lên các hệ thống tiên tiến hơn.

**Kết luận**

Bằng cách kết hợp dữ liệu không gian địa lý, thuật toán định tuyến tiên tiến và khả năng quản lý đội xe toàn diện, các doanh nghiệp giờ đây có thể đạt được các mục tiêu về môi trường mà không ảnh hưởng đến hiệu quả hoạt động. Khi các tổ chức trên toàn thế giới đang phải đối mặt với áp lực ngày càng tăng trong việc giảm thiểu tác động đến môi trường, nền tảng công nghệ của HERE, có sẵn trên AWS Marketplace, mang đến một lộ trình đã được chứng minh hướng đến hoạt động bền vững, đồng thời duy trì lợi thế cạnh tranh trong chuỗi cung ứng toàn cầu. 

HERE Location Services và HERE Tour Planning hiện có sẵn dưới dạng dịch vụ SaaS trên [AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=cc033bc0-fe05-4d79-ba58-9a132b1fe9d3) và có các gói dùng thử để giúp khách hàng kiểm tra các giải pháp. Truy cập trang web của [HERE Technologies](https://www.here.com/) để tìm hiểu thêm.

**HERE Technologies–Đối tác tiêu biểu của AWS**

HERE Technologies, một Đối tác Chiến lược của AWS, cung cấp dữ liệu vị trí và nền tảng công nghệ được công nhận là hoàn thiện nhất trong ngành, giúp khách hàng tối ưu hóa việc giao hàng từ chặng đầu đến chặng cuối, xây dựng chuỗi cung ứng thế hệ mới với khả năng hiển thị lô hàng và tài sản, phát triển hệ thống lái xe tự động và cabin kỹ thuật số. HERE cho phép các đối tác và khách hàng đổi mới sáng tạo trong khi vẫn kiểm soát dữ liệu và bảo vệ quyền riêng tư. Khách hàng có thể truy cập các dịch vụ vị trí của HERE trực tiếp thông qua AWS Marketplace, giúp việc tích hợp bản đồ và thông tin vị trí vào các ứng dụng chạy trên nền tảng AWS của họ trở nên liền mạch.

[Liên hệ HERE](https://partners.amazonaws.com/contactpartner?partnerId=001E000001K9eOvIAJ&partnerName=HERE%20Technologies) | [Tổng quan về Đối tác](https://partners.amazonaws.com/partners/001E000001K9eOvIAJ/HERE%20Technologies) | [AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=cc033bc0-fe05-4d79-ba58-9a132b1fe9d3)