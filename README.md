# gRPC-Spring-Boot-Integration

Need For gRPC:
Microservices are the popular way to design distributed systems. A big monolith application is broken down into multiple independent Microservices. These Microservices have few advantages compared to traditional monolith applications – like easy to deploy, scale, reuse etc. Microservices do not come alone. There will be always more than 1 service. These Microservices communicate with each other mostly with REST using HTTP/1.1 protocol by exchanging JSON.

For example: If an user tries to send a request to order-service to order a product, order-service might internally send multiple requests to other services to fulfill the request. One request from user might trigger multiple internal requests among microservices in an application design.



REST is simple and very easy to use. REST is great for browser. Easy to test our APIs. Developers love this. So we always use REST style for our inter-microservices communication. However it has following issues.

HTTP/1.1 is textual & Heavy. Microservices exchange information by using huge JSON payload.
HTTP is stateless. So additional information is sent via headers which are not compressed.
HTTP/1.1 is unary – that is – you send a request and get a response. You can not send another request until you receive the response.
HTTP request requires a 3 way message exchange to set up a TCP connection first which is time consuming.
This all can affect the overall performance of our Microservices. REST is good between browser and back-end. But we need something better than REST for inter microservices communication to avoid above mentioned issues.

RPC:
RPC, Remote Procedure Call, is an old mechanism in distributed computing, to execute certain procedure in a remote machine without having to understand the network details. Processes in the same system/different systems which are not sharing the same address space can use RPC for their communication. The call will be made as we would normally invoke a local method call. It follows the client-server model. A client sends a request to the server by invoking a method on the remote server and exchanges messages. RPC provides a well defined interface and type safety.



gRPC:
gRPC is a RPC implementation / framework from Google for inter-microservices communication. Google has been using this for more than 15 years (internal name is Stubby). It is battle tested for more than a decade. Google site shows they have been processing 10 BILLIONS requests / second using gRPC.

gRPC is faster than REST (Checkout this gRPC vs REST Performance Comparison). We achieve this performance gain by switching to gRPC because of these 2 important reasons along with other in-built tools.

HTTP/2
Protocol Buffers (Check this out – Protobuf / Protocol Buffers – A Simple Introduction)
gRPC by default uses HTTP/2 for transport and Protocol Buffers for message exchange instead of JSON whereas most of the current microservices architectural style is REST with JSON on top of HTTP/1.1

HTTP/1.1 vs HTTP/2
HTTP/1.1	HTTP/2
Textual format	Binary format
Headers are plain text. Not compressed	Compressed headers
Single request and response with 1 single TCP connection.	Same TCP connection can be reused for multiplexing.
Server streaming
Client streaming
Bi-directional streaming
Protocol Buffers vs JSON
JSON	Protocol Buffers
No strict schema definition / No strict type	Strict schema definition & Type safety
Textual	Binary
Test format makes serialization / deserialization slower & CPU/Memory intensive	Binary format makes serialization/deserialization faster
Manual work to create the classes to serialize & deserialize	Auto generated for most of the programming languages
By combining the above HTTP/2 and Protocol Buffers,  gRPC becomes a better choice for inter-microservices communication.

REST	gRPC
JSON	Protocol Buffers
HTTP/1.1	HTTP/2
Single Request & Response	Single Request / Response
Client Streaming
Server Streaming
Bi-Directional Streaming
gRPC Course:
I learnt gRPC + Protobuf in a hard way. But you can learn them quickly on Udemy. Yes, I have created a separate step by step course on Protobuf + gRPC along with Spring Boot integration for the next generation Microservice development. Click here for the special link.




gRPC API Types:
REST by default is unary. We send a request and get the response. But gRPC supports streaming requests and responses along with unary APIs.

Unary: This is a regular blocking request and response call.


Client Streaming: Client keeps on sending a request to the server by using a single TCP connection. The server might accept all the messages and sends a single response back.
Use case: File upload functionality


Server Streaming: Server sends multiple messages to the client via single TCP connection.
Use case:  Pagination or Server pushes periodic updates to the client asynchronously.


Bi-Directional Streaming: Client and Server can keep on sharing messages via single TCP connection.
Use case: Chat application or GPS or Client & server have to work together in an interactive way to complete a task


