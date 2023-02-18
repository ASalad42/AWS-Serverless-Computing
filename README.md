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




## Serverless Chat App Project:
Aim:
- Creating a chat web app using AWS - Lambda, DynamoDB, API Gateway, S3, Cognito, CloudFront, and more.


![image](https://user-images.githubusercontent.com/104793540/219374111-17d71aa4-e05a-4374-be5e-718143536ffa.png)


- user comes to site and loads static HTML, CSS, and JS
- static part of page are HTML and dynamic parts are added by JS
- JS retreieve dynamic data from API
- JS writes data to the API
- JS handles some aspects of navigation 

Remember IAM between:
- Lambda & s3
- Lambda & DynamoDB
- Lambda & Cognito

IAM:
- Policies (choose or create policy)
- role (choose policy created + basic execution)

![image](https://user-images.githubusercontent.com/104793540/219449521-56005e2d-7145-4dfc-aa37-4599be0472d5.png)
![image](https://user-images.githubusercontent.com/104793540/219449935-75353d58-335d-46b4-932e-ead5c6708d2a.png)




### Static chat app with S3
- upload site folder to s3 (ACL enabled as i want app public)
- check permissions > then property for static website hosting

![image](https://user-images.githubusercontent.com/104793540/219378188-12aaabfd-99d2-409e-bafe-6b79772409c3.png)

- Access policy definition > under permissions bucket policy 

![image](https://user-images.githubusercontent.com/104793540/219380053-8633177b-2658-430d-9f47-c9bcaae69378.png)
![image](https://user-images.githubusercontent.com/104793540/219380088-ce446e6a-141f-422e-87db-18e75d8f3c17.png)

Site bare bones:
- CSS (look and feel of the site i.e font and styles)
- JavaScript JS (bootstrap js file, jquery popular libarary and recommened if ever running dynamic website, config.js store values custom to app such as api endpoints and userpool names, site.js ) 
- HTML (rendering site- brings in css and js)


#### JavaScript 
JavaScript is the world's most popular programming language. JavaScript is the programming language of the Web. Made to run in the browser and the DOM (Document Object Model) can only be manipulated in a single thread.


Syntax:
- == equivalent values
- === equal values of the same type
- null - an object of type null (nothing)
- undefined - a value of type undefined (havent defined yet)

```
var object = {
  p1:1,
  p2:2,
  'this is quoted':'hello, world'
  };
  
  object.p1 is the same as object['p1'] 
  i.e dot ref is same as array ref

```

JQuery:

jQuery is a JavaScript Library. jQuery greatly simplifies JavaScript programming.
- $ is JQuery library 
- http call with:
- $.get()
- $.post()
- class selector, ID selector, tag selector

Useful ref:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference
- https://api.jquery.com/
- https://www.w3schools.com/jquery/
- https://www.w3schools.com/js/default.asp

JS Parallesim:
- JS is single threaded (all my code runs on a single thread) but browsers and Node.js manage other threads like http calls for me. 
- callbacks: define a function that gets called whenever value becomes available (anything that requries async call will take a callback in order to return value or error)

### Creating API

#### Lambda
- create function > correct env (node.js x12)+ existing execution role
- add source code to index.js
- configure test event and run test > success

Triggers:
- API, s3, cognito, DynamoDB, cloudfront, Cloudwatch events, SNS

#### API Gateway in front of Lambda function
Develop a REST API where you gain complete control over the request and response along with API management capabilities.

- proxy mode 
- mapping mode

Proxy mode:
- create REST api > edge optimised endpoint type
- create proxy resource > choose chat lambda function 
- test with get method > go back to lambda and see what has changed:

![image](https://user-images.githubusercontent.com/104793540/219459529-d0de211a-db94-4cf6-b5c4-85bd589c4b17.png)


#### Setup CORS (Cross-origin resource sharing)
- api > on proxy select actions > enable cors (4xx,5xx)
- deploy api
- tighten down cors to my s3 bucket only

![image](https://user-images.githubusercontent.com/104793540/219684125-5b536eea-dd5e-49c0-87dd-3bd9695a66c9.png)

### DynamoDB for chat app storage
DynamoDB is a fully managed, key-value, and document database that delivers single-digit-millisecond performance at any scale.

- fast and flexible NoSQL database service for any scale
- flexible data model and reliable performance make DynamoDB a great fit for mobile, web, gaming, advertising technology, Internet of Things, and other applications.

key-value storage system:
- tables (hash key - sort key - data)
- types of attributes 

![image](https://user-images.githubusercontent.com/104793540/219868223-9993cae7-09fe-4609-9260-fe786ef00ca2.png)

- retrieving items 

![image](https://user-images.githubusercontent.com/104793540/219868373-05f85a91-d5d0-438c-b498-43cbe45d6077.png)

- DynamoDB vs S3 (key-value store vs key-blob store)
- consist reads with DDB

Creating DynamoDB tables:
- Table 1 conversations (id & list of people)
- Table 2 messages (conversation, timestamp, sender & actual message) 

![image](https://user-images.githubusercontent.com/104793540/219869247-45b2b937-a783-4dff-b12a-a658c27ea974.png)

### Cognito for chat app identification

### Optimisation & Production of chat app (incl. Cloudfront CDN) 



## Compare yourself App

Aim:
- web app (single page application) connected to backend (store and fetch data from db)


- API > new path via resource > Enable API Gateway CORS
- post request > serve data > post method > integration type: Lambda Function


Lambda (code on demand function)
- **event source** (s3 (file uploaded), cloudwatch (scheduled), api gateway (http request) > **Code** > **Result** (interact with other aws services > return resonse) 
- supports Node.js and Express apps 
- natively supports Java, Go, PowerShell, Node. js, C#, Python, and Ruby code

![image](https://user-images.githubusercontent.com/104793540/219447870-f0cdcfd6-4782-4d98-a0d2-e96aea548949.png)

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
