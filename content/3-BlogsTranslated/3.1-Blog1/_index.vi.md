---
title: "Định tuyến động các request với routing rules của Amazon API Gateway"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

[Xem bài viết gốc tại đây](https://aws.amazon.com/vi/blogs/compute/dynamically-routing-requests-with-amazon-api-gateway-routing-rules/)

*bởi Anton Aleksandrov và Giedrius Praspaliauskas vào 3 THÁNG 6 2025*

Quản lý API hiệu quả và khả năng định tuyến là yếu tố then chốt đối với các tổ chức vận hành hệ thống ứng dụng phức tạp. Dù bạn là công ty công nghệ triển khai các phiên bản API mới cho hàng triệu người dùng, hay tổ chức tài chính chạy thử nghiệm A/B để tối ưu trải nghiệm khách hàng, thì khả năng định tuyến lưu lượng API một cách động và hiệu quả là vô cùng quan trọng.

[Amazon API Gateway](https://aws.amazon.com/api-gateway/) hiện đã hỗ trợ Dynamic Routing Rules cho [custom domain names](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-custom-domains.html) trên tất cả các [AWS Region](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/). Tính năng này cho phép bạn định tuyến request dựa trên giá trị HTTP header, độc lập hoặc kết hợp với URL path. Trong bài viết này, bạn sẽ học cách sử dụng tính năng mới để triển khai chiến lược định tuyến như API versioning hay gradual rollout mà không cần chỉnh sửa endpoint. 

## **Tổng Quan Về Dynamic Routing Rules**

Nhiều tổ chức yêu cầu khả năng định tuyến API động để đáp ứng các nhu cầu kinh doanh ngày càng phát triển. Với vai trò là một persona thuộc bộ phận kinh doanh, bạn muốn có thể thử nghiệm trải nghiệm người dùng mới với những phân khúc khách hàng cụ thể, đồng thời vẫn giữ nguyên các luồng hoạt động hiện có. Là một kỹ sư, bạn muốn có khả năng duy trì nhiều phiên bản API trên các ứng dụng client khác nhau trong khi vẫn đảm bảo tuân thủ quy định. Trước khi có Dynamic Routing Rules, các nhà phát triển sử dụng API Gateway đã triển khai định tuyến động bằng cách dùng các URL path khác nhau, như "/v1/products" và "/v2/products".

Với Dynamic Routing Rules, bạn có thể triển khai logic định tuyến động bằng một cấu hình khai báo đơn giản trong phần cài đặt custom domain name. Cơ chế routing rule mới cho phép bạn đưa ra các quyết định định tuyến dựa trên HTTP headers, base paths, hoặc kết hợp cả hai. Các nhà phát triển không còn cần phải tạo mới hoặc thay đổi các path hiện có để chuyển đổi mượt giữa các phiên bản API, họ chỉ cần chỉ định giá trị mong muốn trong request HTTP header. Trong số các khả năng khác, bạn có thể triển khai định tuyến kiến trúc cell-based, A/B testing, hoặc lựa chọn backend động dựa trên [hostname](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-custom-domains.html#wildcard-custom-domain-names), tenant ID, accepted response media type, hoặc cookie value. Bằng cách triển khai logic định tuyến trực tiếp trong API Gateway, bạn có thể loại bỏ các proxy layers và các cấu trúc URL phức tạp trong khi vẫn duy trì quyền kiểm soát chi tiết với traffic API của bạn. Tính năng mới này tích hợp liền mạch với các khả năng hiện có của API Gateway và hỗ trợ cả REST APIs công khai và riêng tư. Sơ đồ sau cho thấy cách bạn có thể sử dụng routing rules cho định tuyến dựa trên header và base-path. Ví dụ này sử dụng một tài nguyên cấp một /products để minh họa khớp path, tuy nhiên tùy thuộc vào use-case bạn cũng có thể dùng các path nhiều cấp như /products/items. 

![image-1](/images/3-BlogsTranslated/3.1/image-1.jpg)

Hình 1. Sử dụng routing rules cho định tuyến dựa trên header và base-path

Trong phần tiếp theo, bạn sẽ học cách triển khai header-based routing, sử dụng cấu trúc routing rules mới cho các kịch bản phổ biến như API versioning và A/B testing, và cấu hình các rule với những điều kiện định tuyến và độ ưu tiên khác nhau để đạt được hành vi mong muốn.

## **Routing rule là gì**

[Routing rule](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-routing-mode.html) là một loại tài nguyên mới được liên kết duy nhất với một custom domain. Nó biểu diễn một tập hợp các điều kiện mà, khi được khớp, sẽ khiến request đến được chuyển tiếp đến một API và stage cụ thể. Routing rules có ba thuộc tính cấu hình:

-   **Thuộc tính Conditions** định nghĩa các tiêu chí phải được đáp ứng để hành động được thực hiện. Một rule có thể bao gồm tối đa hai header conditions và một base path condition, và tất cả các điều kiện được chỉ định phải được đáp ứng để kích hoạt hành động. Nếu không có điều kiện nào được định nghĩa cho một rule, nó đóng vai trò như một rule catch-all khớp với tất cả các request.

-   **Thuộc tính Actions** định nghĩa hành động nào sẽ được thực hiện khi các điều kiện của rule được đáp ứng. Tại thời điểm này, hành động được hỗ trợ là gọi bất kỳ stage nào của bất kỳ REST API nào trong cùng một account và region.

-   **Thuộc tính Priority** định nghĩa thứ tự mà các rule được đánh giá, với 1 là ưu tiên cao nhất và 1,000,000 là thấp nhất. Bạn không thể tái sử dụng cùng một giá trị priority cho nhiều hơn một rule. AWS khuyến nghị bạn để khoảng cách rộng giữa các rule liên tiếp để dễ dàng thêm rule mới trong tương lai, ví dụ sử dụng 100, 200, 300 thay vì 1, 2, 3.

Header conditions, được chỉ định qua thuộc tính MatchHeaders, được dùng để khớp giá trị HTTP request header, ví dụ như x-version=v1. Theo chuẩn [RFC 7230](https://datatracker.ietf.org/doc/html/rfc7230), tên header không phân biệt chữ hoa chữ thường, trong khi giá trị header thì phân biệt. Bạn cũng có thể sử dụng ký tự đại diện (wildcards) trong giá trị header cho các kiểu so khớp prefix, suffix, và contains. Sau đây là các ví dụ sử dụng các template [AWS CloudFormation](https://aws.amazon.com/cloudformation/):

Exact match (khớp chính xác):

```yaml
- MatchHeaders:
	AnyOf:
		- Header: "x-version"
		ValueGlob: "alpha-v2-latest"
```

Chỉ khớp với x-version=alpha-v2-latest.

Prefix match (khớp tiền tố):

```yaml
- MatchHeaders:
	AnyOf:
	- Header: "x-version"
	ValueGlob: "*latest"
```

Khớp x-version=alpha-v2-latest, nhưng không khớp x-version=alpha-v2.

Suffix match (khớp hậu tố):

```yaml
- MatchHeaders:
	AnyOf:
		- Header: "x-version"
		ValueGlob: "alpha*"
```

Khớp x-version=alpha-v2-latest và x-version=alpha-v1, nhưng không khớp
x-version=beta-v1.

Prefix và suffix match:

```yaml
- MatchHeaders:
	AnyOf:
		- Header: "x-version"
		ValueGlob: "*v2*"
```

Khớp x-version=alpha-v2-latest và x-version=beta-v2-test, nhưng không
khớp x-version=alpha-v1.

Base path condition, được chỉ định qua MatchBasePaths, dùng để khớp với request path đến. Việc khớp phân biệt chữ hoa chữ thường.

```yaml
- MatchBasePaths: 
	AnyOf: 
		- "products"
```

Bạn có thể có tối đa hai MatchHeaders và một MatchBasePaths cho mỗi routing rule. Các điều kiện được đánh giá bằng toán tử AND, nghĩa là tất cả điều kiện phải được đáp ứng để hành động được thực hiện. Cả hai loại điều kiện đều hỗ trợ một giá trị so sánh duy nhất dưới thuộc tính AnyOf. Ví dụ sau đây minh họa một routing rule với hai điều kiện MatchHeaders và một điều kiện MatchBasePaths:

```yaml
ProductsV1RoutingRule: 
	Type: 'AWS::ApiGatewayV2::RoutingRule' 
	Properties: 
		DomainNameArn: !Sub "arn:aws:apigateway:${AWS::Region}::/domainnames/${ApiCustomDomain}" 
		Priority: 100 
		Conditions: 
			- MatchHeaders: 
				AnyOf: 
					- Header: "x-version" 
					ValueGlob: "v2" 
			- MatchHeaders: 
				AnyOf: 
					- Header: "x-user-cohort" 
					ValueGlob: "beta-testers" 
			- MatchBasePaths: 
				AnyOf: 
					- "products" 
		Actions: 
				- InvokeApi:
					ApiId: !Ref ProductsV2Api 
					Stage: !Ref ProductsV2Stage
```


Rule này sẽ khớp các request tới [https://example.com/products](https://example.com/products) khi cả hai header condition đều được đáp ứng -- x-version=v2 và x-user-cohort=beta-testers. Rule này sẽ không khớp các request tới base path khác, ví dụ [https://example.com/orders](https://example.com/orders), hoặc các request không đáp ứng ít nhất một header condition.

Trong các kịch bản như API versioning, bạn có thể tạo rule để đánh giá các header như "accept" hoặc "version" để định tuyến lưu lượng đến các API implementation khác nhau. Ví dụ, để định tuyến request chứa "x-version: api-beta" tới API beta của bạn, bạn sẽ tạo một rule chỉ định điều kiện header này và đặt action để định tuyến tới triển khai API beta.

Header-based routing cũng đơn giản hóa việc A/B testing bằng cách cho phép bạn định nghĩa các nhóm client dựa trên custom headers, cho phép thực hiện thử nghiệm có kiểm soát với các cấu hình khác nhau. Bạn có thể tạo rule kiểm tra một custom header như x-test-group để định tuyến người dùng cụ thể tới các implementation API khác nhau. Hệ thống priority đảm bảo hành vi định tuyến có thể dự đoán -- khi nhiều rule khớp với một request, rule có số priority thấp nhất (tức là precedence cao nhất) sẽ quyết định định tuyến. Việc kết hợp cả header và path conditions trong một rule duy nhất cho phép các kịch bản định tuyến phức tạp, ví dụ như định tuyến theo version cụ thể cho các tài nguyên API cụ thể thay vì toàn bộ API, như minh họa trong sơ đồ sau.

![image-2](/images/3-BlogsTranslated/3.1/image-2-1.jpg)

Hình 2. Cấu hình định tuyến với hai header và một bộ path conditions trong API Gateway Console.

Tham khảo [tài liệu](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-routing-mode.html) về API Gateway để xem hướng dẫn chi tiết về cách tạo routing rules.

## **Cấu hình Routing Mode**

Trước khi bạn bắt đầu tạo routing rules, bạn phải trước tiên tạo ít nhất một API, một stage, và một custom domain name. Bạn có thể cấu hình custom domain name của bạn với cài đặt routing mode mới.

-   **API mappings only**. Đây là chế độ mặc định. Khi sử dụng chế độ này, bạn có thể tiếp tục dùng base path mappings để định tuyến requests tới các API khác nhau, và không dùng Routing Rules chút nào. Chế độ này duy trì hành vi hiện tại, nơi mà requests chỉ được định tuyến dựa trên base path mappings.

-   **Routing rules then API mappings.** Với chế độ này bạn có thể dùng Routing Rules đồng thời vẫn giữ base path mappings như là một fallback. Khi bạn sử dụng chế độ này, Routing Rules luôn được ưu tiên, và các requests không được khớp sẽ được đánh giá với base path mappings. Chế độ này hữu ích để chuyển đổi dần dần các API của bạn sang Routing Rules.

-   **Routing rules only.** Chế độ này mang đến cho bạn sự linh hoạt để chỉ dùng routing rules, và không phụ thuộc vào base paths mà bạn có thể đã tạo trước đó trên domain bằng API mappings. Đây là routing mode được khuyến nghị; nó hữu ích khi bạn bắt đầu với một custom domain mới hoặc đã hoàn tất việc chuyển đổi từ API mappings sang Routing Rules cho một custom domain hiện có.

Khi chuyển đổi từ một routing mode sang một mode khác, hãy luôn kiểm thử cấu hình mới của bạn trong môi trường không phải production trước. Ví dụ, khi chuyển đổi mode từ API mappings only sang Routing rules only, lưu lượng của bạn sẽ chỉ được định tuyến bằng Routing rules; các API mappings hiện có sẽ không còn hiệu lực nữa.

## **Bắt đầu với Header-Based Routing**

Bạn có thể áp dụng Header-Based Routing mới cho các custom domain API Gateway hiện có của bạn với cách tiếp cận zero-downtime, giảm thiểu rủi ro. Bước đầu tiên là cấu hình custom domain của bạn để sử dụng chế độ Routing rules then API mappings bằng API Gateway console, [AWS CLI](https://aws.amazon.com/cli/), hoặc công cụ hạ tầng dưới dạng code (IaC) của bạn. Cấu hình này đảm bảo rằng trong khi bạn dần dần tạo Routing Rules, các base path mappings hiện có của bạn tiếp tục hoạt động như các route dự phòng (fallback). Do Routing Rules được đánh giá trước base path mappings, và trong trường hợp không có rule nào khớp, các request sẽ tự động quay lại (fall back) sang base path mappings hiện có, lưu lượng API hiện tại của bạn vẫn không bị ảnh hưởng trong quá trình chuyển đổi này.

Khi bạn đã cấu hình routing mode, bạn có thể đưa dần Routing Rules vào song song với thiết lập hiện tại. Ví dụ, bạn có thể bắt đầu bằng cách tạo một rule với một test header cụ thể định tuyến tới một phiên bản API mới, cho phép bạn xác thực hành vi định tuyến với lượng lưu lượng kiểm soát trong khi lưu lượng production vẫn tiếp tục đi qua base path mappings hiện tại của bạn. Khi bạn tự tin với cấu hình routing mới, bạn có thể dần mở rộng rules, điều chỉnh priority, và tùy chọn di chuyển hoàn toàn khỏi base path mappings. Cách tiếp cận gia tăng này, kết hợp với các khả năng observability (quan sát) của API Gateway được mô tả ở phần tiếp theo, cho phép bạn xác thực từng thay đổi và đảm bảo rằng người sử dụng API của bạn không gặp gián đoạn trong quá trình chuyển đổi.

## **Observability (Khả năng quan sát)**

API Gateway cung cấp khả năng quan sát toàn diện về cách các routing rules của bạn xử lý requests thông qua access logging. Mỗi request bây giờ bao gồm các biến ngữ cảnh bổ sung giúp bạn hiểu quá trình quyết định định tuyến. Biến \$context.customDomain.routingRuleIdMatched xác định rule nào đã được khớp và áp dụng cho request. Trong khi các biến hiện có như \$context.domainName, \$context.apiId, và \$context.stage cung cấp đầy đủ ngữ cảnh định tuyến. Bằng cách phân tích các access logs này, bạn có thể xác minh hành vi định tuyến, khắc phục sự cố liên quan đến unexpected routes, và thu thập thông tin chi tiết về mẫu lưu lượng giữa các phiên bản API hoặc các biến thể thử nghiệm khác nhau.

## **Ví dụ tổng thể**

Xem xét một kịch bản thực tế, nơi một nhóm cần phải dần dần di chuyển người dùng sang một phiên bản API mới, chẳng hạn như một nền tảng thương mại điện tử đang cập nhật API checkout của họ từ v1 sang v2. Trước tiên, nhóm này tạo hai REST API khác nhau -- một cho mỗi phiên bản. Sau đó, họ thiết lập một Routing Rule với priority 100 để kiểm tra header x-version=v2 và định tuyến các request khớp đến API v2. Họ cũng tạo một rule khác với priority 200 để định tuyến tất cả các request có path bắt đầu bằng /checkout đến API v1 như một fallback.

![](media/image1.png){width="6.299212598425197in" height="3.5972222222222223in"}

Hình 3. Dần dần chuyển đổi clients từ v1 sang v2 API

Trong mã nguồn của ứng dụng, họ thêm header x-version cho một tỷ lệ nhỏ người dùng. Họ theo dõi hiệu năng và tỷ lệ lỗi bằng cách sử dụng khả năng telemetry của API Gateway, bằng cách theo dõi access logs và execution logs, cùng với các metrics được phát ra. Khi đủ tin tưởng, họ dần tăng tỷ lệ người dùng gửi header v2. Cách tiếp cận này đảm bảo một quá trình chuyển dịch có kiểm soát với rủi ro tối thiểu và khả năng rollback nhanh chóng chỉ bằng cách loại bỏ header khỏi các request hoặc thay đổi một routing rule.

## **Mẫu thử**

Làm theo hướng dẫn trong [repository GitHub này](https://github.com/aws-samples/serverless-samples/tree/main/apigw-header-routing) để provision sample trong tài khoản AWS của bạn. Project này minh họa việc sử dụng dynamic routing với API Gateway.

## **Kết luận**

Header-based routing mang lại những lợi thế đáng kể cho người dùng API Gateway. Tính năng này có khả năng backward compatibility (tương thích ngược) đảm bảo một con đường chuyển đổi mượt mà -- bạn có thể duy trì các base path mappings hiện có trong khi dần dần áp dụng Routing Rules, hoặc sử dụng cả hai cơ chế đồng thời với tùy chọn fallback. Sự linh hoạt này cho phép bạn chuyển dịch theo tốc độ của riêng mình mà không làm gián đoạn các ứng dụng hiện tại. Giải pháp này tiết kiệm chi phí, nhờ vào việc không có khoản phí bổ sung nào khi sử dụng Routing Rules trên REST APIs. Giải pháp này còn giảm yêu cầu phải tận dụng các dịch vụ và hạ tầng bổ sung cho việc định tuyến động. Hệ thống đánh giá dựa trên priority cung cấp hành vi định tuyến có tính quyết định (deterministic), giúp dễ dàng hiểu và khắc phục sự cố các quyết định về định tuyến.

Để tìm hiểu thêm về API Gateway header-based routing, hãy xem [tài liệu về dịch vụ](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-routing-mode.html).

Để tìm hiểu thêm về các cấu trúc Serverless, truy cập [Serverless Land](https://serverlessland.com/).
