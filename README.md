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
- F12 developer tool on chrome
- shift refresh

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

IAM S3:
- Policies (choose or create policy)
- role (choose policy created + basic execution)

![image](https://user-images.githubusercontent.com/104793540/219449521-56005e2d-7145-4dfc-aa37-4599be0472d5.png)
![image](https://user-images.githubusercontent.com/104793540/219449935-75353d58-335d-46b4-932e-ead5c6708d2a.png)

IAM DynamoDB:
- Policies (choose or create policy) > use one of the tables to get ARN format region:accountid
- role (under chat-lambda-data) > permissions > attach policy > select dynamodb policy just created

![image](https://user-images.githubusercontent.com/104793540/219870498-f2fbdb16-a9c8-47ab-9ee6-c05160f99a9e.png)
![image](https://user-images.githubusercontent.com/104793540/219870587-b50bb146-9451-4dfa-9c4d-cd6600b04b6b.png)

IAM Cognito:
- Policies (choose or create policy) > get pool arn for policy from cognito dashboard 
- new role > since accessing user information dont use same role as rest of project > choose policy created + basic execution

![image](https://user-images.githubusercontent.com/104793540/220397268-697a2342-be9f-4d20-85cc-ff3ace44dc1d.png)


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

Lambda (code on demand function)
- **event source** (s3 (file uploaded), cloudwatch (scheduled), api gateway (http request) > **Code** > **Result** (interact with other aws services > return resonse) 
- supports Node.js and Express apps 
- natively supports Java, Go, PowerShell, Node. js, C#, Python, and Ruby code

![image](https://user-images.githubusercontent.com/104793540/219447870-f0cdcfd6-4782-4d98-a0d2-e96aea548949.png)

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

#### Creating DynamoDB tables
- Table 1 conversations (id & list of people)
- Table 2 messages (conversation, timestamp, sender & actual message) 

![image](https://user-images.githubusercontent.com/104793540/219869247-45b2b937-a783-4dff-b12a-a658c27ea974.png)
![image](https://user-images.githubusercontent.com/104793540/219869400-0ec6d67c-e826-45f0-87a0-21d1c025d096.png)
![image](https://user-images.githubusercontent.com/104793540/219869709-ac267926-2c35-422a-8829-a007149a0423.png)

Read a conversation from DynammoDB:
- id, participants, messages, sender, time, message itself 
- add dynamo code to lambda and chek app (v5)

![image](https://user-images.githubusercontent.com/104793540/219879354-d40001e8-f99a-4430-a37e-d0827d42ff38.png)


Read conversation list from DynamoDB:
- add dynamo code to lambda and chek app (v6)

![image](https://user-images.githubusercontent.com/104793540/219884298-40e04391-16ce-4dbb-b54f-7bbe16c252c5.png)


Write new messages to DynamoDB:
- add handling for post commands
- correct test for http method

![image](https://user-images.githubusercontent.com/104793540/219884788-7fc653d2-4150-4510-9c74-5b4cc147cc18.png)

- test with new message and check dynamodb 

![image](https://user-images.githubusercontent.com/104793540/219884959-e942736d-ea2c-4049-867f-f04db2aa7dd7.png)
![image](https://user-images.githubusercontent.com/104793540/219884982-919833ee-eb0e-4017-a77d-6a33d4192e93.png)
![image](https://user-images.githubusercontent.com/104793540/219885000-f9ce4e9e-1ffc-4af3-918a-cd9871d34237.png)


- update site.js & chat.html files in s3 and check chat app to see if it now writes messages 


![image](https://user-images.githubusercontent.com/104793540/219885216-abe949ee-8974-4f61-a445-5b4b571975a2.png)

### Break up monolith (lambda + api gateway)
- having only one lambda function can create problems (leave **proxy mode** behind)

Api Gateway:

- each resource-method combination can be its own function with its own lifecyle 
- each function can have simple, tailored input
- ensuring API compataibility can occur without code 
- Resource and methods > api models > request and response flows 


http basics:
- key peices of request are: method (GET), path, host 
- key peices of response: status code, body

Mehtods:

- **Read:** GET (most common http method of all i.e when i clink link or go on url a GET call is started) and HEAD (sibling of get but only returns headers & status code)
- **Write:** actually change data on the server > POST (create new resource), PUT (create or replace particular resource), PATCH (updating resource by providing a diff)
- **Other:** DELETE, OPTIONS 


![image](https://user-images.githubusercontent.com/104793540/220335884-21d6d64d-64b1-46f0-bcf0-f0b25337257d.png)

status codes:
- 2xx success
- 3xx redirect
- 4xx client error 
- 5xx server error i.e server issues 

Models:

- request data > body (POST,PUT, PATCH)
- reponse data > body  
- json schema (null, boolean, array, object, number, string) 

![image](https://user-images.githubusercontent.com/104793540/220337132-50173534-faeb-470b-a505-3f7c3d1f6913.png)


request flow:

![image](https://user-images.githubusercontent.com/104793540/220337612-a411e86e-5716-4b2a-9761-1d2280adc3b6.png)

#### Deploy API

Lambda Functions:
- Chat-Conversations-GET > added to integration request
- Chat-Messages-GET > added to integration request
- Chat-Messages-POST > added to integration request


![image](https://user-images.githubusercontent.com/104793540/220355379-977bb8fe-0489-4e38-852b-f19007d58efe.png)
![image](https://user-images.githubusercontent.com/104793540/220355552-412893bc-eb29-4cd8-b749-4ee44a8d0f76.png)
![image](https://user-images.githubusercontent.com/104793540/220355684-7549672e-ad00-400b-ba32-731057c179ed.png)

Stages:
- prod > SDK generation > Javascript > unzip & upload to s3
- update s3 files for site.js, chats.html & chat.html
- prod > export > swagger yaml > https://editor.swagger.io/

![image](https://user-images.githubusercontent.com/104793540/220359770-2671951c-16d7-4a47-be60-cc32b617f4fa.png)
![image](https://user-images.githubusercontent.com/104793540/220360229-fc34cc0d-6604-4b4a-8ad1-54ae9d222860.png)


### Cognito for chat app identification

Amazon Cognito > Secure identity and access management for apps. Cognito user pools let you add registration and sign-in to your apps. With Amazon Cognito identity pools, you can provide AWS credentials for access to your cloud resources.

services:
- user pools - Your own usernames, passwords, attributes, etc.
- federated - Use SSO (Google, Facebook, Amazon, etc.)
- sync - Synchronize data across devices

user pools:
- users and groups - List and manage users and/or groups and see details
- attributes - Define what a user looks like
- security:
  - policies - Password length, special characters, etc.
  - mfa and verifications - MFA phone and email verification 
  - advanced - Intelligent security features (outside free teir)

##### List users in api & on site

![image](https://user-images.githubusercontent.com/104793540/220390756-dbc5e2b2-e1d4-43c7-86ed-44f322d3e429.png)

- ensure lambda has access to cognito via IAM
- create lambda function for getting users (use existing role)
- wire up api gateway > create user model > create users resource and GET method > choose right lambda function > edit method response
- deploy users api

![image](https://user-images.githubusercontent.com/104793540/220399832-1a679523-b683-466d-a5b6-acc8540ce51c.png)

- add people.html page to s3
- add users on cognito > create user

![image](https://user-images.githubusercontent.com/104793540/220432373-d204f527-c7ed-4e0d-8cce-3a4646ce569a.png)

##### Debugging serverless apps:
- dicipline 
- start from the front or backend. starting from back:
  - assume cognito works > otherwise non of this would work 
  - next layer is lambda that calls cognito > test lambda function (Chat-Users-GET) > success and return of users just made in outputs
  - next layer after that is api gateway > /users GET > test > success and return of users just made in outputs
  - check prod stage > invoke /users GET > also works 
  - finally check javascript using developer tool > go to api > stages > prod > sdk generation > javascript sdk > upload to s3 in js folder

![image](https://user-images.githubusercontent.com/104793540/220433453-8ee67bb7-40e5-457e-8658-f852f7c780e4.png)
![image](https://user-images.githubusercontent.com/104793540/220433775-e7d8f581-dcf2-4edb-a86a-f35e022ae177.png)
![image](https://user-images.githubusercontent.com/104793540/220434137-4d87eb26-db7a-41b9-934a-f08e04175c65.png)
![image](https://user-images.githubusercontent.com/104793540/220435376-7d120a03-c9a2-4068-ad7b-3f5c48c9ba2b.png)


##### create new conversation 
- Lambda function - Chat-Conversation-POST
- upload layer zip file and add layer to function 
- add conversationid & newconversation models to api gateway
- add post method to conversation 
- method request (newconversation model for the request) and method response (conversationid i get back)
- integration request > mapping templates 
- enable cors on /conversations before redeploying 
- Deploy API > generate new js sdk > upload to s3

##### create signup page

- `npm install --save amazon-cognito-identity-js`
- ` cd node_modules`      `cd amazon-cognito-identity-js`       `cd dist`
- check for amazon-cognito-identity.min.js
- upload to s3 in js folder

![image](https://user-images.githubusercontent.com/104793540/220443888-f53adfd0-c360-498f-bc78-ed335fc0908d.png)
![image](https://user-images.githubusercontent.com/104793540/220614087-b37b9945-f461-4ae4-b8a1-a218c3800722.png)
![image](https://user-images.githubusercontent.com/104793540/220614156-d2e5809e-1095-4099-bd5b-f90bdb344d81.png)

##### create verification page
- upload files to s3

![image](https://user-images.githubusercontent.com/104793540/220615292-6b1676da-8639-4206-9e35-988d5dadc8d4.png)

![image](https://user-images.githubusercontent.com/104793540/220615479-6d2f1a47-cf1e-4fba-ad95-2517d640c583.png)

##### login & logout
![image](https://user-images.githubusercontent.com/104793540/220616542-210c6ca8-c8b3-4576-98f1-6bea5e4c1c4c.png)

##### add cognito authorizer to api gateway 
- Authorizers > create new authorizer > token source = Authorization as already define in CORS integration 

![image](https://user-images.githubusercontent.com/104793540/220617524-46d15ef1-c970-417b-92b5-204454ae6c2e.png)

- get token from console developer tool

![image](https://user-images.githubusercontent.com/104793540/220620443-e4d43513-c070-42f8-8b20-59fa47814499.png)

- after setting up authorizer update mapping templates 
  - conversations GET > method request > authorization > cognito (refresh page if needed) > integration request > mapping template
  - conversations POST > method request > authorization > cognito (refresh page if needed) > integration request > mapping template
  - chat messages GET > method request > authorization > cognito (refresh page if needed) > integration request > mapping template
  - chat messages POST > method request > authorization > cognito (refresh page if needed) > integration request > mapping template
  - users GET > method request > authorization > cognito (refresh page if needed) > integration request > mapping template

- Deploy API
- link signin & authorization

#### Cloudfront CDN


### Extras

- https://andersonguelphjs.github.io/OReilly_JavaScript_The_Good_Parts_May_2008.pdf


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
