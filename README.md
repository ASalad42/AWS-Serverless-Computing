# AWS Serverless Computing

## API Gateway, AWS Lambda & DynamoDB

### Severless Development 

Issues with traditional web hosting Apps:
- keep OS and software updated 
- over or under provisioning 
- servers online even if not required 

Serverless benefits:
- Runs on demand (unlimited cap, only pay for code executions)
- scales automatically 
- runs on managed AWS infrastructure 
- great for SPA + API apps (limited support for Fullstack apps)

Useful:

- SPA single page application 

### Core serverless services

![image](https://user-images.githubusercontent.com/104793540/217071968-dba3fbde-f6f1-4e09-b489-ef74812f742c.png)

### Business logic with Lambda and API Gateway
A REST API (also known as RESTful API) is an application programming interface (API or web API) that conforms to the constraints of REST architectural style and allows for interaction with RESTful web services.

#### API
- If you want to interact with a computer or system to retrieve information or perform a function, an API **helps you communicate what you want to that system so it can understand and fulfill the request.**
- mediator between the users or clients and the resources or web services they want to get
- Establishes the content required from the consumer (the call) and the content required by the producer (the response).

#### REST
- set of architectural constraints that API developers can implement in a variety of ways.
- When a client request is made via a RESTful API, it transfers a **representation** of the state of the resource to the requester or endpoint.
- representation, is delivered in one of several formats via HTTP: JSON (Javascript Object Notation), HTML, XLT, Python, PHP, or plain text. 
- JSON is the most generally popular file format to use because, despite its name, it’s language-agnostic, as well as readable by both humans and machines. 


#### Creating and API Gateway & AWS Lambda


### Data Storage with DynamoDB

### Authentication with Cognito 

### Content delivery & hosting with S3, Cloudfront, and Route53




#### AWS Serverless + Express Apps

- https://aws.amazon.com/blogs/compute/going-serverless-migrating-an-express-application-to-amazon-api-gateway-and-aws-lambda/
- https://github.com/vendia/serverless-express

#### Serverless Framework
- https://www.serverless.com/framework/docs/getting-started
- https://github.com/serverless/serverless

#### Serverless Application Model (SAM)
- https://github.com/aws/serverless-application-model
- https://github.com/aws/serverless-application-model/blob/master/HOWTO.md
- https://docs.aws.amazon.com/lambda/latest/dg/deploying-lambda-apps.html
