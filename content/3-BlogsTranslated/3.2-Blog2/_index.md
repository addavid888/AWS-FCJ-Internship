---
title: "Introducing an agentic coding experience in Visual Studio and JetBrains IDEs"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

*by Artur Rodrigues and Neeraj Handa on 05 JUN 2025*

Developers spend countless hours on repetitive tasks like debugging code, writing unit tests, and validating build processes – time that could be better spent on innovation and problem-solving. To address these challenges, Amazon Q Developer has expanded its intelligent coding assistant capabilities to Visual Studio and JetBrains Integrated development environments (IDEs). This new agentic experience works proactively on your behalf, automatically analyzing your workspace, generating code fixes, and executing commands to streamline your development workflow.

In this blog post, we’ll explore how Amazon Q Developer automates unit test creation and execution to validate code changes, streamlines build processes by identifying and resolving common issues.

In May 2025, our colleague Brian Beach wrote about the [new agentic coding experience in Amazon Q Developer for VS Code](https://aws.amazon.com/blogs/devops/amazon-q-developer-agentic-coding-experience/). By extending the agentic experience to Visual Studio and JetBrains IDEs, Amazon Q Developer now brings intelligent automation to even more developers.

**Benefits for Developers**

Amazon Q Developer transforms the way developers work by seamlessly integrating AI assistance into their daily workflow without switching contexts or leaving their preferred development environment. Using features like [@workspace](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/workspace-context.html) and [@files](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/ide-chat-context.html#context-explicit), you can get highly relevant recommendations in your IDE. With Q Developer’s ability to take actions like generating code diffs and running commands, you can automate repetitive coding tasks, implement complex features faster, and troubleshoot issues without breaking your flow. With [support for multiple languages including English, Mandarin, Japanese, and Spanish](https://aws.amazon.com/blogs/devops/amazon-q-developer-global-capabilities/), Amazon Q Developer makes advanced AI assistance accessible to development teams worldwide, fostering inclusive collaboration across global organizations.

**Maximizing Development Efficiency with Amazon Q Developer**

Amazon Q Developer revolutionizes your development workflow by offering a comprehensive set of capabilities within your IDE. Let’s explore how this powerful tool leverages context to enhance your coding experience by using context features, codebase’s folders and rules.

You can explicitly guide Q Developer by defining specific files or folders in the prompt context. Don’t know where to find particular information? No problem! Q Developer can efficiently navigate through your codebase using @workspaces to gather relevant code snippets from multiple files. This is particularly important when you want to create documentation that spans multiple files or when you need to fix a bug and have no idea where you should start.

The agentic chat feature automatically derives context from the codebase’s folders and executes commands on your behalf. It has the same intelligent reasoning capability used in the Q Developer CLI, which has already won the hearts of many developers.

Context management extends to configuration through the .amazonq/rules/ directory. Within this directory, you can define [rules](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/context-project-rules.html) for coding standards, testing requirements, security protocols, and documentation practices. Some customers have already created a rule that defines how Q Developer commits changes. This rule provides a template for a Git commit that details the message and for the agentic actions that modify files. It makes it much easier to identify and review the contributions of the Q Developer to your codebase.

**Quick Tour of the Agentic Experience**

Let us walk you through two use cases. In our example, we will use the Visual Studio IDE. Similar agentic capabilities are now supported in [JetBrains IDEs](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE.html#supported-ides-features) as well. We invite you to follow along by cloning the [Bob’s Used Books sample repo](https://github.com/aws-samples/bobs-used-bookstore-sample) and opening it in Visual Studio 2022. Don’t forget to add or update the [Amazon Q Developer extension](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.AWSToolkitforVisualStudio2022).

***Creating unit tests***

The **Bookstore.Domain** project contains domain objects such as **Book** and **ShoppingCart**.

Figure 1: Domain objects in Bookstore.Domain

We have a separate project called Bookstore.Domain.Tests that contains tests for the Book class.

Figure 2: Tests for Book class

We want to add unit tests for the **ShoppingCart** class. Let’s ask Amazon Q Developer to create unit tests for **ShoppingCart**. We also want Amazon Q Developer to follow the existing pattern of creating test classes in a separate test project.

By default, the agentic experience is on. If you are in the planning phase of the Software Development Lifecycle (SDLC) and prefer to use a traditional back-and-forth chat, you can turn the agentic experience. To toggle the agentic experience on and off, choose the angle bracket pair in the bottom left corner of your Q Developer chat window.

Then, we ask Q Developer *“Can you create a test for @ShoppingCart.cs? Look at existing test and use the same libraries”*. First, notice that we are giving a command instead of just asking a question. Second, we are referencing the file ShoppingCart.cs explicitly to provide Q Developer the appropriate context. In the following image, you can see that Q Developer is acting on our behalf. In agentic coding mode, Q Developer can take actions and run commands. In our example, it is reading files, writing to files, and running commands with your permission.

Figure 3: Prompt to create new tests

Using commands, Q Developer was able to analyze our solution structure, understand that we have a project called **Bookstore.Domain.Tests**, and create a new file containing unit tests for **ShoppingCart**.

We can verify that there is a new file called **ShoppingCartTests** in the **Bookstore.Domain.Tests** project, which is aligned with our existing test creation strategy.

In Visual Studio, we can now run the unit tests and verify that they pass.

Figure 6: Successful test run of new tests

**Resolving build errors**

In the following example, we will demonstrate the power of the agentic coding experience by using Q Developer to build our application and resolve build errors.

In our example, we have deliberately misspelled one of the methods in the **IShoppingCartRepository** interface. The **AddAsync** method is now incorrectly spelled **AddAsyn**.

Figure 7: Spelling mistake in a method name

When we try to build the **Bookstore.Domain** project, we get a build error as expected. Let’s ask Q Developer to fix the error. Without the agentic coding experience, we would have to copy the text of the build error into the chat window and ask Q Developer to provide recommendations. Then we would have to act on its recommendations by manually making changes and trying to build. This is one of many examples of the power of the agentic chat, which runs commands and uses the command’s output to enrich the context of the prompt to take actions.

With the agentic coding experience, we just ask Q Developer *“Can you fix the error I am getting while building the solution? Please build and check it”*. In the following image, you will see how Q Developer runs the .NET build commands to get build errors and read the relevant files.

Figure 8: Building the solution

After it reads the files, it finds the spelling mistake and fixes it automatically. As shown in the following image, it then builds the solution to verify that its fix worked.

Figure 9: Fixing the spelling mistake

In the following image, Amazon Q Developer provides a summary of the error, the actions it took to build it. It even helps me with some recommendations to fix the warnings it got while running the build.

Figure 10: Summary of changes and suggestions

**Conclusion**

The addition of Amazon Q Developer’s agentic experience in Microsoft Visual Studio and JetBrains IDEs takes Amazon Q Developer beyond traditional chat-based interactions to intelligent, action-oriented assistance. The ability to automatically read files, generate code diffs, run shell commands, and validate changes demonstrates a level of autonomy that can significantly accelerate development tasks while maintaining code quality. The examples we’ve explored, from automated test creation to build error resolution, showcase how the agentic experience can streamline common development tasks that traditionally required multiple manual steps. This new capability, combined with multi-language support and customizable development standards, makes Amazon Q Developer a powerful ally in modern software development workflows. As development teams continue to seek ways to improve productivity without compromising code quality, Amazon Q Developer’s agentic experience represents a meaningful step forward in IDE-integrated AI assistance. Whether you’re writing tests, fixing bugs, or optimizing code, the ability to have an AI assistant that can not only suggest solutions but also implement them while maintaining context awareness is a game-changing addition to the developer’s toolkit.








Data lakes can help hospitals and healthcare facilities turn data into business insights, maintain business continuity, and protect patient privacy. A **data lake** is a centralized, managed, and secure repository to store all your data, both in its raw and processed forms for analysis. Data lakes allow you to break down data silos and combine different types of analytics to gain insights and make better business decisions.

This blog post is part of a larger series on getting started with setting up a healthcare data lake. In my final post of the series, *“Getting Started with Healthcare Data Lakes: Diving into Amazon Cognito”*, I focused on the specifics of using Amazon Cognito and Attribute Based Access Control (ABAC) to authenticate and authorize users in the healthcare data lake solution. In this blog, I detail how the solution evolved at a foundational level, including the design decisions I made and the additional features used. You can access the code samples for the solution in this Git repo for reference.

---

## Architecture Guidance

The main change since the last presentation of the overall architecture is the decomposition of a single service into a set of smaller services to improve maintainability and flexibility. Integrating a large volume of diverse healthcare data often requires specialized connectors for each format; by keeping them encapsulated separately as microservices, we can add, remove, and modify each connector without affecting the others. The microservices are loosely coupled via publish/subscribe messaging centered in what I call the “pub/sub hub.”

This solution represents what I would consider another reasonable sprint iteration from my last post. The scope is still limited to the ingestion and basic parsing of **HL7v2 messages** formatted in **Encoding Rules 7 (ER7)** through a REST interface.

**The solution architecture is now as follows:**

> *Figure 1. Overall architecture; colored boxes represent distinct services.*

---

While the term *microservices* has some inherent ambiguity, certain traits are common:  
- Small, autonomous, loosely coupled  
- Reusable, communicating through well-defined interfaces  
- Specialized to do one thing well  
- Often implemented in an **event-driven architecture**

When determining where to draw boundaries between microservices, consider:  
- **Intrinsic**: technology used, performance, reliability, scalability  
- **Extrinsic**: dependent functionality, rate of change, reusability  
- **Human**: team ownership, managing *cognitive load*

---

## Technology Choices and Communication Scope

| Communication scope                       | Technologies / patterns to consider                                                        |
| ----------------------------------------- | ------------------------------------------------------------------------------------------ |
| Within a single microservice              | Amazon Simple Queue Service (Amazon SQS), AWS Step Functions                               |
| Between microservices in a single service | AWS CloudFormation cross-stack references, Amazon Simple Notification Service (Amazon SNS) |
| Between services                          | Amazon EventBridge, AWS Cloud Map, Amazon API Gateway                                      |

---

## The Pub/Sub Hub

Using a **hub-and-spoke** architecture (or message broker) works well with a small number of tightly related microservices.  
- Each microservice depends only on the *hub*  
- Inter-microservice connections are limited to the contents of the published message  
- Reduces the number of synchronous calls since pub/sub is a one-way asynchronous *push*

Drawback: **coordination and monitoring** are needed to avoid microservices processing the wrong message.

---

## Core Microservice

Provides foundational data and communication layer, including:  
- **Amazon S3** bucket for data  
- **Amazon DynamoDB** for data catalog  
- **AWS Lambda** to write messages into the data lake and catalog  
- **Amazon SNS** topic as the *hub*  
- **Amazon S3** bucket for artifacts such as Lambda code

> Only allow indirect write access to the data lake through a Lambda function → ensures consistency.

---

## Front Door Microservice

- Provides an API Gateway for external REST interaction  
- Authentication & authorization based on **OIDC** via **Amazon Cognito**  
- Self-managed *deduplication* mechanism using DynamoDB instead of SNS FIFO because:  
  1. SNS deduplication TTL is only 5 minutes  
  2. SNS FIFO requires SQS FIFO  
  3. Ability to proactively notify the sender that the message is a duplicate  

---

## Staging ER7 Microservice

- Lambda “trigger” subscribed to the pub/sub hub, filtering messages by attribute  
- Step Functions Express Workflow to convert ER7 → JSON  
- Two Lambdas:  
  1. Fix ER7 formatting (newline, carriage return)  
  2. Parsing logic  
- Result or error is pushed back into the pub/sub hub  

---

## New Features in the Solution

### 1. AWS CloudFormation Cross-Stack References
Example *outputs* in the core microservice:
```yaml
Outputs:
  Bucket:
    Value: !Ref Bucket
    Export:
      Name: !Sub ${AWS::StackName}-Bucket
  ArtifactBucket:
    Value: !Ref ArtifactBucket
    Export:
      Name: !Sub ${AWS::StackName}-ArtifactBucket
  Topic:
    Value: !Ref Topic
    Export:
      Name: !Sub ${AWS::StackName}-Topic
  Catalog:
    Value: !Ref Catalog
    Export:
      Name: !Sub ${AWS::StackName}-Catalog
  CatalogArn:
    Value: !GetAtt Catalog.Arn
    Export:
      Name: !Sub ${AWS::StackName}-CatalogArn
