---
title: "Dynamically routing requests with Amazon API Gateway routing rules"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

_by Anton Aleksandrov and Giedrius Praspaliauskas on 03 JUN 2025_

Effective API management and routing capabilities are crucial for organizations managing complex application architectures. Whether you’re a technology company rolling out new API versions to millions of users, or a financial services organization conducting A/B tests to optimize customer experiences, the ability to route API traffic dynamically and efficiently is essential.

Today, [Amazon API Gateway](https://aws.amazon.com/api-gateway/) announces support for dynamic routing rules for [custom domain names](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-custom-domains.html) in all supported [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/). This new capability enables you to route API requests based on HTTP header values, either independently or in combination with URL paths. In this post, you will learn how to use this new capability to implement routing strategies such as API versioning and gradual rollouts without modifying your API endpoints.

## Dynamic Routing Rules Overview

Many organizations require dynamic API routing capabilities to support their evolving business needs. As a line-of-business persona, you want to be able to test new user experiences with specific customer segments, while maintaining their existing flows intact. As an engineer, you want to be able to maintain multiple API versions across different client applications while ensuring regulatory compliance. Prior to this launch, developers using API Gateway implemented dynamic routing by using different URL paths, such as “**/v1/products**” and “**/v2/products**”.

With this new launch, you can implement dynamic routing logic with a simple declarative configuration within the custom domain name settings. The new routing rule mechanism allows you to make routing decisions based on HTTP headers, base paths, or a combination of both. Developers are no longer required to create new or alter existing paths to smoothly transition between API versions, they can simply specify the desired value in the request HTTP header. Among other possibilities, you can implement cell-based architecture routing, A/B testing, or dynamic backend selection based on [hostname](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-custom-domains.html#wildcard-custom-domain-names), tenant ID, accepted response media type, or cookie value. By implementing routing logic directly within the API Gateway, you can eliminate proxy layers and complex URL structures while maintaining fine-grained control over your API traffic. This new feature seamlessly integrates with existing API Gateway capabilities and supports both public and private REST APIs. The following diagram shows how you can use routing rules for header and base-path based routing. This example uses a single level resource /products to show path matching, however depending on your use-case you could also use multi-level paths like **/products/items**.

![image-1](images/3-BlogsTranslated/3.1-/image-1.png)

Figure 1. Using routing rules for header and base-path based routing

In the following section you’ll learn how to implement header-based routing, use the new routing rules construct for common scenarios like API versioning and A/B testing, and configure rules with different routing conditions and priorities to achieve the desired behavior.

**What is a routing rule**

A [routing rule](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-routing-mode.html) is a new resource type uniquely associated with a single custom domain. It represents a collection of conditions that, when matched, cause the incoming request to be forwarded to a specific API and stage. Routing rules have three configuration properties:

- The Conditions property defines the criteria that must be met for actions to be taken. A rule can include up to two header conditions and one base path condition, and all specified conditions must be met to trigger the action. If no conditions are defined for a rule, it serves as a catch-all rule matching all requests.

- The Actions property defines what actions will be taken when rule conditions are met. At the time of this launch the supported action is invoking any stage of any REST API within the same account and region boundaries.

- The Priority property defines the order that rules are evaluated in, with 1 being highest priority and 1,000,000 the lowest. You cannot reuse same priority value for more than one rule. AWS recommends you leave ample space between sequential rules to make it easy to add new rules in future, for example use 100, 200, 300 instead of 1, 2, 3.

Header conditions, specified via a **MatchHeaders** property, are used to match HTTP request header values, such as x-**version=v1**. Conforming to [RFC 7230](https://datatracker.ietf.org/doc/html/rfc7230), header names are not case sensitive, while header values are. You can also use wildcards in header values for prefix, suffix, and contains match. See the following examples using [AWS CloudFormation](https://aws.amazon.com/cloudformation/) templates:

**Exact match:**

```yaml
- MatchHeaders:
	AnyOf:
		- Header: "x-version"
		ValueGlob: "alpha-v2-latest"
```

Will only match x-version=alpha-v2-latest

**Prefix match:**

```yaml
- MatchHeaders:
	AnyOf:
	- Header: "x-version"
	ValueGlob: "*latest"
```

Matches x-version=alpha-v2-latest, but not x-version=alpha-v2

**Suffix match:**

```yaml
- MatchHeaders:
	AnyOf:
		- Header: "x-version"
		ValueGlob: "alpha*"
```

Will match x-version=alpha-v2-latest and x-version=alpha-v1, but not x-version=beta-v1

**Prefix and suffix match.**

```yaml
- MatchHeaders:
	AnyOf:
		- Header: "x-version"
		ValueGlob: "*v2*"
```

Matches x-version=alpha-v2-latest and x-version=beta-v2-test, but not x-version=alpha-v1

Base path condition, specified via **MatchBasePaths** property, is used to match the incoming request path. The matching is case sensitive.

```yaml
- MatchBasePaths: 
	AnyOf: 
		- "products"
```

You can have up to two **MatchHeaders** and one **MatchBasePaths** conditions per routing rule. Conditions are evaluated using the **AND** operator, meaning all conditions must be met for the action to be taken. Both condition types support a single comparison value under **AnyOf** property. The following snippet illustrates a sample routing rule with two **MatchHeaders** conditions and a single **MatchBasePaths** condition.

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

This rule matches requests to https://example.com/products when both header conditions are met **– x-version=v2** and **x-user-cohort=beta-testers**. This rule does not match requests to any other base path, such as https://example.com/orders, or requests that do not match at least one header condition.

For scenarios like API versioning, you can create rules that evaluate headers such as **“accept”** or **“version”** to route traffic to different API implementations. For example, to route requests containing **“x-version: api-beta”** to your beta API, you would create a rule specifying this header condition and set the action to route to your beta API deployment.

Header-based routing also simplifies A/B testing by allowing you to define client cohorts based on custom headers, allowing controlled experiments with different configurations. You can create rules that check for a custom header like **“x-test-group”** to route specific users to different API implementations. The priority system ensures predictable routing behavior – when multiple rules match a request, the rule with the lowest priority number (highest precedence) determines the routing. Combining header and path conditions within a single rule enables complex routing scenarios such as version-specific routing for specific API resources instead of the entire API, as illustrated in the following diagram.

![image-2](images/3-BlogsTranslated/3.1-/image-2-1.png)

Figure 2. A routing configuration with two header and one path conditions in API Gateway Console.

Review the API Gateway [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-routing-mode.html) for detailed guide on creating routing rules.

**Configuring Routing Mode**

Before you begin creating routing rules, you must first create at least one API, stage, and a custom domain name. You can configure your custom domain name with the new routing mode setting.

- **API mappings only.** This is the default mode. When using this mode, you can continue to use base path mappings to route requests to different APIs, and not use Routing Rules at all. This mode maintains the current behavior, where requests are routed based on base path mappings only.

- **Routing rules then API mappings.** With this mode you can use Routing Rules while continuing to keep base path mappings as a fallback. When you use this mode, the Routing Rules always take precedence, and unmatched requests are evaluated against base path mappings. This mode is useful for gradually transitioning your APIs to Routing Rules.

- **Routing rules only.** This mode gives you the flexibility to use routing rules only, and not rely on the base paths that you may have previously created on the domain using API mappings. This is the recommended routing mode; it is helpful when you are starting off with a new custom domain or finished transitioning from API mappings to Routing Rules for an existing custom domain.

When switching from one routing mode to another, always test your new configuration in non-production environments first. For example, when switching mode from API mappings only to routing rules only, your traffic will only be routed with routing rules; existing API mappings will no longer take effect.

**Onboarding to Header-Based Routing**

You can adopt the new Header-Based Routing for your existing API Gateway custom domains with zero-downtime, risk-minimized approach. The first step is to configure your custom domain to use the **Routing rules then API mappings** mode using the API Gateway console, [AWS CLI](https://aws.amazon.com/cli/), or your infrastructure-as-code (IaC) tool. This configuration ensures that while you gradually create Routing Rules, your existing base path mappings continue to function as fallback routes. Since Routing Rules are evaluated before base path mappings, and in the absence of any matching rules, requests automatically fall back to your existing base path mappings, your current API traffic remains unaffected during this transition.

**Observability**

API Gateway provides comprehensive visibility into how your routing rules are processing requests through [access logging](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-variables-for-access-logging.html). Each request now includes additional context variables that help you understand the routing decision process. The **$context.customDomain.routingRuleIdMatched** variable identifies which rule was matched and applied to the request, while existing variables like **$context.domainName**, **$context.apiId**, and **$context.stage** provide the complete routing context. By analyzing these access logs, you can verify routing behavior, troubleshoot unexpected routes, and gather insights about traffic patterns across different API versions or test variants.

**End-to-end example**

Consider a real-world scenario where a team needs to gradually migrate users to a new API version, such as an e-commerce platform updating its checkout API from v1 to v2. First, the team creates two different REST APIs – one for each version. Then, they set up a Routing Rule with priority 100 that checks for the header **x-version=v2** and routes matching requests to the v2 API. They also create another rule with priority 200 that routes all requests with paths starting with **/checkout** to v1 API as a fallback.

Figure 3. Gradually transitioning clients from v1 to v2 API.

In the application code they add the **x-version** header for a small percentage of users. They monitor the performance and error rates using API Gateway’s telemetry capabilities by tracking the access and execution logs, along with emitted metrics. As their confidence grows, they gradually increase the percentage of users sending the v2 header. This approach ensures a controlled migration with minimal risk and ability to quickly rollback by simply removing the header from requests or changing a routing rule.

**Sample**

Follow the instructions in [this GitHub repository](https://github.com/aws-samples/serverless-samples/tree/main/apigw-header-routing) to provision the sample in your AWS account. The project illustrates using dynamic routing with API Gateway.

**Conclusion**

Header-based routing brings significant advantages to API Gateway users. The feature’s backward compatibility ensures a smooth transition path – you can maintain existing base path mappings while gradually adopting Routing Rules, or use both mechanisms simultaneously with the fallback option. This flexibility allows you to migrate at your own pace without disrupting existing applications. The solution is cost-effective, with no additional charges for using Routing Rules on REST APIs. It reduces requirements to leverage extra service and infrastructure for dynamic routing. The priority-based evaluation system provides deterministic routing behavior, making it easier to understand and troubleshoot routing decisions.

To learn more about API Gateway header-based routing see the [service documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-routing-mode.html).

To learn more about Serverless architectures see [Serverless Land](https://serverlessland.com/).