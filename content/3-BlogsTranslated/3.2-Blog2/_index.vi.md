---
title: "Giới thiệu trải nghiệm lập trình với trí tuệ nhân tạo hành động độc lập trong Visual Studio và JetBrains IDEs"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

[Xem bài viết gốc tại đây](https://aws.amazon.com/vi/blogs/devops/introducing-an-agentic-coding-experience-in-visual-studio-and-jetbrains-ides/)


*bởi Artur Rodrigues và Neeraj Handa, ngày 05 THÁNG 6 2025*

Các lập trình viên dành vô số giờ cho các công việc lặp đi lặp lại như debug code, viết unit tests, và xác thực quy trình build – khoảng thời gian lẽ ra có thể được dùng tốt hơn cho đổi mới và giải quyết vấn đề. Để giải quyết những thách thức này, Amazon Q Developer đã mở rộng khả năng trợ lý lập trình thông minh của mình đến Visual Studio và JetBrains Integrated Development Environments (IDEs). Trải nghiệm agentic mới này hoạt động chủ động thay mặt bạn, tự động phân tích workspace của bạn, sinh code fixes, và thực thi các commands để tối ưu hóa quy trình phát triển của bạn.

*(Trải nghiệm Agentic: trải nghiệm lập trình với trí tuệ nhân tạo có khả năng hành động độc lập, đưa ra quyết định và đạt được mục tiêu một cách tự chủ thay cho lập trình viên)*

Trong bài blog này, chúng ta sẽ khám phá cách Amazon Q Developer tự động hóa việc tạo và thực thi unit tests để xác thực thay đổi code, cũng như tối ưu quy trình build bằng cách nhận diện và xử lý các vấn đề phổ biến.

Vào tháng 5 năm 2025, đồng nghiệp của chúng tôi Brian Beach đã viết về [trải nghiệm lập trình agentic mới trong Amazon Q Developer cho VS Code](https://aws.amazon.com/blogs/devops/amazon-q-developer-agentic-coding-experience/). Bằng cách mở rộng trải nghiệm agentic sang Visual Studio và JetBrains IDEs, Amazon Q Developer giờ đây mang tự động hóa thông minh đến với nhiều lập trình viên hơn.

**Lợi ích cho Lập trình viên**

Amazon Q Developer thay đổi cách các lập trình viên làm việc bằng cách tích hợp mượt mà sự hỗ trợ AI vào quy trình hằng ngày mà không cần chuyển đổi ngữ cảnh hoặc rời khỏi môi trường phát triển ưa thích của họ. Với các tính năng như [@workspace](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/workspace-context.html) và [@files](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/ide-chat-context.html#context-explicit), bạn có thể nhận được gợi ý có liên quan cao ngay trong IDE. Với khả năng của Q Developer trong việc thực hiện hành động như sinh code diffs và chạy commands, bạn có thể tự động hóa các tác vụ lặp đi lặp lại, triển khai tính năng phức tạp nhanh hơn, và xử lý sự cố mà không làm gián đoạn dòng công việc. Với việc [hỗ trợ nhiều ngôn ngữ bao gồm tiếng Anh, tiếng Trung, tiếng Nhật, và tiếng Tây Ban Nha](https://aws.amazon.com/blogs/devops/amazon-q-developer-global-capabilities/), Amazon Q Developer làm cho hỗ trợ AI tiên tiến trở nên dễ tiếp cận cho các nhóm phát triển toàn cầu, thúc đẩy cộng tác toàn diện trong các tổ chức quốc tế.

**Tối Đa Hóa Hiệu Quả Phát Triển với Amazon Q Developer**

Bạn có thể hướng dẫn Q Developer rõ ràng bằng cách định nghĩa các file hoặc folder cụ thể trong prompt context. Không biết tìm thông tin ở đâu? Không thành vấn đề! Q Developer có thể điều hướng hiệu quả qua codebase của bạn bằng cách dùng @workspaces để thu thập code snippets liên quan từ nhiều file. Điều này đặc biệt quan trọng khi bạn muốn tạo tài liệu trải rộng nhiều file hoặc khi bạn cần sửa một bug mà không biết bắt đầu từ đâu.

Tính năng agentic chat tự động suy ra context từ các folder của codebase và thực thi commands thay bạn. Nó có cùng khả năng reasoning thông minh được dùng trong Q Developer CLI, vốn đã chiếm được cảm tình của nhiều lập trình viên.

Quản lý context còn mở rộng đến cấu hình thông qua thư mục .amazonq/rules/. Trong thư mục này, bạn có thể định nghĩa các [rule](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/context-project-rules.html) cho coding standards, testing requirements, security protocols, và documentation practices. Một số khách hàng đã tạo một rule định nghĩa cách Q Developer commit changes. Rule này cung cấp một template cho Git commit (bao gồm chi tiết message) và cho các agentic actions sửa file. Điều này giúp dễ dàng hơn để nhận diện và review các đóng góp của Q Developer cho codebase của bạn.

**Tham Quan Nhanh Trải Nghiệm Agentic**

Hãy cùng đi qua hai use case. Trong ví dụ của chúng tôi, chúng tôi sẽ sử dụng Visual Studio IDE. Các khả năng agentic tương tự cũng đã được hỗ trợ trong [JetBrains IDEs](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE.html#supported-ides-features). Chúng tôi mời bạn làm theo bằng cách clone [repo mẫu Bob’s Used Books](https://github.com/aws-samples/bobs-used-bookstore-sample) và mở nó trong Visual Studio 2022. Đừng quên thêm hoặc cập nhật [extension Amazon Q Developer](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.AWSToolkitforVisualStudio2022).


***Tạo unit tests***

Project **Bookstore.Domain** chứa các domain objects như **Book** và **ShoppingCart**.

![image-1](/images/3-BlogsTranslated/3.2/Figure1-QDevVSAgentic.jpg)

Hình 1: Domain objects trong Bookstore.Domain

Chúng tôi có một project riêng tên là Bookstore.Domain.Tests chứa các tests cho lớp Book.

![image-2](/images/3-BlogsTranslated/3.2/Figure2-QDevVSAgentic.jpg)

Figure 2: Tests for Book class

Chúng ta muốn thêm unit tests cho lớp **ShoppingCart**. Hãy nhờ Amazon Q Developer tạo unit tests cho **ShoppingCart**. Chúng tôi cũng muốn Amazon Q Developer tuân theo pattern hiện có là tạo test classes trong một project test riêng biệt.

Theo mặc định, trải nghiệm agentic được bật. Nếu bạn đang trong giai đoạn planning của Software Development Lifecycle (SDLC) và muốn sử dụng kiểu chat truyền thống qua lại, bạn có thể tắt trải nghiệm agentic. Để bật hoặc tắt agentic experience, chọn cặp dấu ngoặc nhọn ở góc trái dưới của cửa sổ chat Q Developer.

Sau đó, chúng tôi hỏi Q Developer: *“Can you create a test for @ShoppingCart.cs? Look at existing test and use the same libraries.”* Đầu tiên, hãy chú ý rằng chúng tôi đưa ra một command thay vì chỉ đặt câu hỏi. Thứ hai, chúng tôi tham chiếu rõ ràng file ShoppingCart.cs để cung cấp context phù hợp cho Q Developer. Trong hình tiếp theo, bạn có thể thấy rằng Q Developer đang hành động thay mặt chúng tôi. Trong chế độ agentic coding, Q Developer có thể thực hiện hành động và chạy commands. Trong ví dụ của chúng tôi, nó đang đọc file, ghi vào file, và chạy commands với sự cho phép của bạn.

![image-3](/images/3-BlogsTranslated/3.2/Figure3-QDevVSAgentic-537x1024.jpg)

Hình 3: Prompt để tạo các bài test mới

Bằng cách dùng commands, Q Developer có thể phân tích cấu trúc solution của chúng tôi, hiểu rằng chúng tôi có một project tên là **Bookstore.Domain.Tests**, và tạo một file mới chứa unit tests cho **ShoppingCart**.

![image-4](/images/3-BlogsTranslated/3.2/Figure4-QDevVSAgentic.jpg)

Hình 4: Tóm tắt về các test case

Ta có thể thấy rằng đã có một file mới tên là **ShoppingCartTests** trong project **Bookstore.Domain.Tests**, phù hợp với chiến lược tạo test hiện có.

![image-5](/images/3-BlogsTranslated/3.2/Figure5-QDevVSAgentic.jpg)

Hình 5: File mới với test cases được sinh ra

Trong Visual Studio, chúng tôi bây giờ có thể chạy các unit tests và xác nhận rằng chúng pass.

![image-6](/images/3-BlogsTranslated/3.2/Figure6-QDevVSAgentic.jpg)

Hình 6: Chạy các bài test mới thành công

**Xử lý build errors**

Trong ví dụ tiếp theo, chúng tôi sẽ minh họa sức mạnh của trải nghiệm agentic coding bằng cách dùng Q Developer để build ứng dụng của chúng tôi và xử lý build errors.

Trong ví dụ, chúng tôi cố ý viết sai chính tả một method trong interface **IShoppingCartRepository**. Method **AddAsync** đã bị viết sai thành **AddAsyn**.

![image-7](/images/3-BlogsTranslated/3.2/Figure7-QDevVSAgentic-1024x414.jpg)

Hình 7: Lỗi chính tả trong tên method

Khi chúng tôi cố gắng build project **Bookstore.Domain**, chúng tôi nhận được build error như mong đợi. Hãy nhờ Q Developer sửa lỗi này. Nếu không có agentic coding experience, chúng tôi sẽ phải copy text của build error vào cửa sổ chat và yêu cầu Q Developer đưa ra khuyến nghị. Sau đó chúng tôi sẽ phải làm theo khuyến nghị bằng cách chỉnh sửa thủ công và thử build lại. Đây chỉ là một trong nhiều ví dụ về sức mạnh của agentic chat, cái có thể chạy commands và dùng output của commands để làm giàu context cho prompt nhằm thực hiện hành động.

Với agentic coding experience, chúng tôi chỉ cần hỏi Q Developer: *“Can you fix the error I am getting while building the solution? Please build and check it.”* Trong hình dưới đây, bạn sẽ thấy Q Developer chạy các lệnh build .NET để lấy build errors và đọc các file liên quan.

![image-8](/images/3-BlogsTranslated/3.2/Figure8-QDevVSAgentic.jpg)

Hình 8: Amazon Q Developer đang tạo ra giải pháp

Trong hình tiếp theo, Amazon Q Developer cung cấp một bản tóm tắt của lỗi, các hành động nó đã thực hiện để build, và thậm chí giúp tôi với một số khuyến nghị để sửa các warnings mà nó gặp trong khi chạy build.

![image-9](/images/3-BlogsTranslated/3.2/Figure9-QDevVSAgentic.jpg)

Hình 9: Sửa lỗi chính tả

In the following image, Amazon Q Developer provides a summary of the error, the actions it took to build it. It even helps me with some recommendations to fix the warnings it got while running the build.

![image-10](/images/3-BlogsTranslated/3.2/Figure10-QDevVSAgentic.jpg)

Hình 10: Tóm tắt các thay đổi và gợi ý

**Kết luận**

Việc bổ sung trải nghiệm agentic của Amazon Q Developer vào Microsoft Visual Studio và JetBrains IDEs đưa Amazon Q Developer vượt xa khỏi các tương tác chat truyền thống đến hỗ trợ thông minh, định hướng hành động. Khả năng tự động đọc file, sinh code diffs, chạy shell commands, và xác thực các thay đổi thể hiện một mức độ tự chủ có thể tăng tốc đáng kể các nhiệm vụ phát triển trong khi vẫn duy trì chất lượng code. Các ví dụ mà chúng ta đã khám phá – từ tạo test tự động đến xử lý build errors – cho thấy cách trải nghiệm agentic có thể tối ưu hóa các tác vụ phát triển phổ biến vốn trước đây đòi hỏi nhiều bước thủ công. Khả năng mới này, kết hợp với hỗ trợ đa ngôn ngữ và các tiêu chuẩn phát triển tùy biến, biến Amazon Q Developer thành một đồng minh mạnh mẽ trong workflows phát triển phần mềm hiện đại. Khi các nhóm phát triển tiếp tục tìm cách cải thiện năng suất mà không làm giảm chất lượng code, trải nghiệm agentic của Amazon Q Developer đại diện cho một bước tiến có ý nghĩa trong IDE-integrated AI assistance. Cho dù bạn đang viết tests, sửa bugs, hay tối ưu code, khả năng có một AI assistant không chỉ gợi ý giải pháp mà còn có thể triển khai chúng trong khi vẫn duy trì nhận thức ngữ cảnh là một bổ sung thay đổi cuộc chơi cho bộ công cụ của lập trình viên.
