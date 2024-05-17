---
title: "Demystifying AWS Lambda: Unveiling the Serverless Powerhouse (Part 1)"
seoTitle: "Demystifying AWS Lambda"
seoDescription: "Unveiling the Serverless Powerhouse - Lambda"
datePublished: Fri May 17 2024 17:54:46 GMT+0000 (Coordinated Universal Time)
cuid: clwazby28000t09mmhs4p3uid
slug: demystifying-aws-lambda-unveiling-the-serverless-powerhouse-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1715968363917/2020ddae-13e5-4be7-99f6-4b48826d20f0.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1715968403783/9a4014fd-0ced-4227-bd44-2717f6360020.png
tags: aws, aws-lambda, lambda-function, aws-certified-solutions-architect-associate

---

AWS Lambda is an event-driven, serverless **compute** service. It allows you to run code without provisioning or managing servers.

### Serverless:

* It abstracts (hides) the infrastructure layer. This ability eliminates the need to manually manage the underlying physical hardware. So you can focus on the code for your applications without spending time building and maintaining the underlying infrastructure.
    
* Advantage comparison of traditional environment and serverless.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715962217673/55168aef-cb65-4cb9-b2f3-5c3b078299d7.png align="center")
    
* services that are part of the AWS serverless platform:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715962317145/288c69a0-16ca-4316-9471-5e36e3c8f1d8.jpeg align="center")
    

### Lambda:

It operates and maintains all of the compute resources, including server and operating system maintenance, capacity provisioning and automatic scaling, code monitoring, and logging.

**Benefits:**

* You can run code for almost any type of application or backend service.
    
* You can **run code** without provisioning or maintaining servers.
    
* It **initiates functions** for you in response to events.
    
* It **scales** automatically.
    
* It provides built-in code **monitoring and logging** via Amazon CloudWatch.
    

**Features:**

* With AWS Lambda, you can run code **without** provisioning or managing servers.
    
* Lambda initiates **events** on your behalf, scales automatically, and provides built-in monitoring and logging.
    
* You can write **code** in your preferred language.
    
* You do **configure** the memory for your function, but not CPU.
    
* You don't work with the OS. AWS provides the operating environment at runtime.
    

### **What is a Lambda Function:**

* The code you run on AWS Lambda is called a ***Lambda*** ***function***.
    
* These are *stateless*, with no affinity to the underlying infrastructure.
    
* Lambda can rapidly launch as many copies of the function as needed to scale to the rate of incoming events.
    

### How AWS Lambda works?

AWS Lambda is an example of an event-driven architecture. Most AWS services generate events and act as an event source for Lambda. Lambda runs custom code (functions) in response to events. Lambda functions are designed to process these events and, once invoked, may initiate other actions or subsequent events. So it is important to understand how events initiate functions to invoke the code within.

**Invocation models for running Lambda functions**

3 general patterns (invocation models). Each invocation model is unique and addresses a different application and developer needs.

1. **Synchronous:**
    
    * When a function is invoked synchronously, Lambda runs the function and waits for a response.
        
    * When the function completes, Lambda returns the response from the function's code with additional data, such as the version of the function that was invoked.
        
    * Synchronous events expect an immediate response from the function invocation.
        
    * There are no built-in retries. You must manage your retry strategy within your application code.
        
    * The following diagram shows clients invoking a Lambda function synchronously.
        
    * Lambda sends the events directly to the function and sends the function response directly back to the invoker.
        
        ![Shows icons of event flow, client, event, function.](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1715968800/8EL0E6UbynNxmV6jYtP_QQ/tincan/674187_1676990596_p1gpq6pq781l3ntaa1fcbps6c0t4_zip/assets/MUkmRcXISC_qu_XB_O80oQc87BztFI4Yn-section2-sycnhronous%20invocation_NOPROCESS_.jpg align="left")
        
    
    The following AWS services invoke Lambda synchronously:
    
    * Amazon API Gateway, Amazon Cognito, AWS CloudFormation, Amazon Alexa, Amazon Lex, Amazon CloudFront
        
    
2. **Asynchronous:**
    
    * When you invoke a function asynchronously, events are queued and the requestor doesn't wait for the function to complete.
        
    * This model is appropriate when the client doesn't need an immediate response.
        
    * With the asynchronous model, you can make use of destinations.
        
    * Use destinations to send records of asynchronous invocations to other services.
        
    
    ![Event flow, client, event, asynch, function.](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1715968800/8EL0E6UbynNxmV6jYtP_QQ/tincan/674187_1676990596_p1gpq6pq781l3ntaa1fcbps6c0t4_zip/assets/WvIyDB-0SzH0-Y9i_Ax8dnp2LoTaAFHsK-section2-asycnhronous%20invocation_NOPROCESS_.jpg align="left")
    
    A destination can send records of asynchronous invocations to other services. You can configure destinations on a function, a version, or an alias, similarly to how you can configure error handling settings. With destinations, you can address errors and successes without needing to write more code. 
    
    ![MgI08vsAfVpQA49__3h6pTpqgr8hD_x7u-section2-destinations_NOPROCESS_.jpg](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1715968800/8EL0E6UbynNxmV6jYtP_QQ/tincan/674187_1676990596_p1gpq6pq781l3ntaa1fcbps6c0t4_zip/assets/MgI08vsAfVpQA49__3h6pTpqgr8hD_x7u-section2-destinations_NOPROCESS_.jpg align="left")
    
    When the function returns a success response or exits without producing an error, Lambda sends a record of the invocation to an EventBridge event bus. When an event fails all processing attempts, Lambda sends an invocation record to an Amazon Simple Queue Service (Amazon SQS) queue.
    
    **AWS Services:** Amazon SNS, Amazon S3 and Amazon EventBridge invokes Lambda asynchronously.
    
3. **Polling:**
    
    * This invocation model is designed to integrate with AWS **streaming and queuing** based services with no code or server management.
        
    * Lambda will poll (or watch) these services, retrieve any matching events, and invoke your functions.
        
    * This invocation model supports the following services: Kinesis, SQS, and DynamoDB Streams.
        
    * With this type of integration, AWS will manage the poller on your behalf and perform synchronous invocations of your function.
        
    * The configuration of services as event triggers is known as event source mapping.
        
        * This process occurs when you configure event sources to launch your Lambda functions and then grant these sources IAM permissions to access the Lambda function.
            
    * Lambda reads events from: **DynamoDB, Kinesis, MQ, Managed Streaming for Apache Kafka (MSK), Self-managed Apache Kafka and SQS**
        
    * With this model, the retry behavior varies depending on the event source and its configuration.
        

**Invocation model error behavior  
**When deciding how to build your functions, consider how each invocation method handles errors.

Synchronous - No retries

Asynchronous - Built in - retries twice

Polling - Depends on the event source

### Lambda execution environment:

![icons showing invocation flow.](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1715968800/8EL0E6UbynNxmV6jYtP_QQ/tincan/674187_1676990596_p1gpq6pq781l3ntaa1fcbps6c0t4_zip/assets/XmiKq-LAplB17t-N_Orb6G1QyzP3m5T08-Lifecycle-image-whole_NOPROCESS_.jpg align="left")

When you create your Lambda function, you specify configuration information, such as the amount of available memory and the maximum invocation time allowed for your function. Lambda uses this information to set up the execution environment.

**Init Phase:**  
In this phase, Lambda creates or unfreezes an execution environment. The Init phase happens either during the first invocation, or before function invocations if you have enabled provisioned concurrency.

The Init phase is split into three sub-phases: 

1. Extension init - starts all extensions
    
2. Runtime init - bootstraps the runtime
    
3. Function init - runs the function's static code
    
    These sub-phases ensure that all extensions and the runtime complete their setup tasks before the function code runs.
    

**Invoke Phase:**

In this phase, Lambda invokes the function handler. After the function runs to completion, Lambda prepares to handle another function invocation.

**Shutdown Phase:**

If the Lambda function does not receive any invocations for a period of time, this phase initiates. In the Shutdown phase, Lambda shuts down the runtime, alerts the extensions to let them stop cleanly, and then removes the environment. Lambda sends a shutdown event to each extension, which tells the extension that the environment is about to be shut down.