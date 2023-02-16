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
- CORS Cross Origin Resource Sharing 

### Core serverless services

![image](https://user-images.githubusercontent.com/104793540/217071968-dba3fbde-f6f1-4e09-b489-ef74812f742c.png)

### Business logic with Lambda and API Gateway
A REST API (also known as RESTful API) is an application programming interface (API or web API) that conforms to the constraints of REST architectural style and allows for interaction with RESTful web services.

#### API
- If you want to interact with a computer or system to retrieve information or perform a function, an API **helps you communicate what you want to that system so it can understand and fulfill the request.**
- mediator between the users or clients and the resources or web services they want to get
- Establishes the content required from the consumer (the call) and the content required by the producer (the response).

For exmaple: 
- clients send request to some API because they need some backend to do something for them i.e:
  - execute some code
  - store something in a database
  - retrieve something from a database 


#### REST
- set of architectural constraints that API developers can implement in a variety of ways.
- When a **client request** is made via a RESTful API, it transfers a **representation** of the state of the resource to the requester or endpoint.
- **REST stands for representational state transfer**
- representation, is delivered in one of several formats via HTTP: JSON (Javascript Object Notation), HTML, XLT, Python, PHP, or plain text. 
- JSON is the most generally popular file format to use because, despite its name, it’s language-agnostic, as well as readable by both humans and machines. 


#### Creating an API Gateway & AWS Lambda (on-demand computing)
Application > REST API > Action (run lambda code)

- API Gateway > create REST API > new api > name first-api > create
- Actions > resources > create (cant call yet so do methods next)
- Actions > methods > GET (request) > mock. first end point created 
- integration > body mapping > application/json 
- Actions > deploy API > dev stage > https://t68wzxxbfd.execute-api.eu-west-1.amazonaws.com/dev/first-api-test
- Bring resources live with deploy action

![image](https://user-images.githubusercontent.com/104793540/217248465-9469c680-fc35-47ec-b7e5-fb09c340a8ac.png)

API Keys:
- Actions > create API keys (good for usage plans and with other developers)

**Endpoint:**
- Endpoint = resource (path which request is sent) + method (type of request)

**cycle: flow of data in API**
- method request: incoming requests have certain shape/data (has schema needed been met)(**gatekeeper**)
- integration request: mapping incoming data to trigger endpoint (extract incoming data to pass onto action)
- integration response: configures the response to be sent back
- method response: defines shape of response/data sent back to user 


##### Compare yourself App

Aim:
- web app (single page application) connected to backend (store and fetch data from db)


- API > new path via resource > Enable API Gateway CORS
- post request > serve data > post method > integration type: Lambda Function


Lambda (code on demand function)
- **event source** (s3 (file uploaded), cloudwatch (scheduled), api gateway (http request) > **Code** > **Result** (interact with other aws services > return resonse) 
- supports Node.js and Express apps 
- natively supports Java, Go, PowerShell, Node. js, C#, Python, and Ruby code

Handler i.e index.handler:
- looks for **index file** 
- in that file look at **export objects** and find the handler **function** stored in the **handler property** (export handler)

back to API:
- find recently created lambda function and connect 
- test

![image](https://user-images.githubusercontent.com/104793540/217831089-c9cfb94f-1e7e-46a5-8882-e8000cf31ecb.png)

Accessing the API from the web:
- deploy api (check stages for snapshot)
- (ctrl shift c for developer mode - check errors in console > fix CORS error to do with Access-Control-Allow-Origin
- add in method reponse first under header mapping > then add value for header in integration response > deploy 

Accessing the API from the Web - The Right Way:



Forwarding Requests with Proxy Integration:

Accessing Lambda Logs:
 
Mapping and Models:
 
 
 




### Data Storage with DynamoDB

#### Using DynamoDB with Lambda

#### Creating a Table in DynamoDB

#### Accessing DynamoDB from Lambda

#### Putting Items into a DynamoDB Table from Lambda

#### Using API Gateway (Request) Data for Item Creation



### Authentication with Cognito 

### Content delivery & hosting with S3, Cloudfront, and Route53


## Serverless Chat App Project:

![image](https://user-images.githubusercontent.com/104793540/219374111-17d71aa4-e05a-4374-be5e-718143536ffa.png)

- user comes to site and loads static HTML, CSS, and JS
- static part of page are HTML and dynamic parts are added by JS
- JS retreieve dynamic data from API
- JS writes data to the API
- JS handles some aspects of navigation 




### Extras
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
