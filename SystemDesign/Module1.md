# Module 1

## Overview

Go step by step through the different components and concepts involved in architecting a web application.

## Module Objectives

1. Understand the concepts, components, and technology trade-offs involved in architecting a web application.
2. Learn various architectural styles such as the client-server, peer to peer decentralized architecture, the fundamentals of data flow in a web application, concepts like scalability, high availability and much more.
3. Master the techniques of picking the right architecture and the technology stack to implement a use case.

## Different Tiers in Software Architecture

1. Introduction
   1. Think of a tier as a logical separation of components in an application or a service.
   2. physical separation at the component level
   3. components
      1. Database
      2. Backend application server
      3. User interface
      4. Messaging
      5. Caching
2. Single Tier Applications
   1. A single-tier application is an application where the user interface, backend business logic & the database all reside in the same machine.
   2. Advantages
      1. no network latency
      2. data is easily & quickly available
      3. data of the user stays in his machine
   3. Disadvantages
      1. Business has no control over the application
      2. no code or features changes can possibly be done until the customer manually updates
      3. vulnerable to being tweaked & reversed engineered
3. Two Tier Application
   1. A Two-tier application involves a client and a server. The client would contain the user interface & the business logic in one machine. And the backend server would be the database running on a different machine. The database server is hosted by the business & has control over it.
   2. Need for 2 tier
      1. to-do list app or a similar planner or a productivity app
      2. fewer network calls
      3. online browser & app-based games
         1. get downloaded on the client just once
         2. network calls only to keep the game state persistent.
4. Three Tier Applications
   1. In a three-tier application, the user interface, application logic & the database all lie on different machines & thus have different tiers. They are physically separated.
5. N tier applications
   1. An N-tier application is an application which has more than three components involved.
   2. components
      1. Cache
      2. Message queues for asynchronous behaviour
      3. Load balancers
      4. Search servers for searching through massive amounts of data
      5. Components involved in processing massive amounts of data
      6. Components running heterogeneous tech commonly known as web services etc.
   3. There is another name for n-tier apps, the “distributed applications”
   4. Need for N-tier
      1. Two software design principles that are key to explaining this are the Single Responsibility Principle & the Separation of Concerns.
      2. Single Responsibility Principle
         1. Single Responsibility Principle simply means giving one, just one responsibility to a component & letting it execute it with perfection
         2. This approach gives us a lot of flexibility & makes management easier.
         3. Dedicated teams & code repositories for every component
         4. Single responsibility principle is a reason why I was never a fan of stored procedures.
         5. Stored procedures enable us to add business logic to the database
         6. A database should not hold business logic, it should only take care of persisting the data
      3. Separation Of Concerns
         1. Separation of concerns kind of means the same thing, be concerned about your work only & stop worrying about the rest of the stuff.
         2. Keeping the components separate makes them reusable.
         3. Different services can use the same database, the messaging server or any component as long as they are not tightly coupled with each other.
      4. Having loosely coupled components is the way to go. The approach makes scaling the service easy in future when things grow beyond a certain level.
   5. Difference Between Layers & Tiers
      1. The difference between layers and tiers is that the layers represent the organization of the code and breaking it into components.
      2. Tiers involve physical separation of components

## Web Architecture

1. What?
   1. Web architecture involves multiple components like database, message queue, cache, user interface & all running in conjunction with each other to form an online service.
2. Client Server Architecture
   1. Client-Server architecture is the fundamental building block of the web.
   2. The architecture works on a request-response model. The client sends the request to the server for information & the server responds with it.
   3. A very small percent of the business websites and applications use the peer to peer architecture, which is different from the client-server.
3. Client
   1. The client holds our user interface.
   2. The user interface is the presentation part of the application
4. Types of Client
   1. Thin Client
      1. Thin Client is the client which holds just the user interface of the application.
      2. It has no business logic of any sort. For every action, the client sends a request to the backend server.
   2. Thick Client
      1. On the contrary, the thick client holds all or some part of the business logic.
      2. These are the two-tier applications.
5. Server
   1. The primary task of a web server is to receive the requests from the client & provide the response after executing the business logic based on the request parameters received from the client.
   2. Kinds
      1. application servers
      2. Proxy server
      3. Mail server
      4. File server
      5. Virtual server
   3. Java, we would pick Apache Tomcat or Jetty
   4. hosting websites, we would pick the Apache HTTP Server.
   5. Server-Side Rendering
      1. Often the developers use a server to render the user interface on the backend & then send the rendered data to the client.
6. Communication Between the Client & the Server
   1. Request-Response Model
      1. The client & the server have a request-response model. 
      2. If there is no request, there is no response. Pretty simple right?
   2. HTTP Protocol
      1. HTTP protocol is a request-response protocol that defines how information is transmitted across the web.
      2. It’s a stateless protocol, every process over HTTP is executed independently & has no knowledge of previous processes.
      3. More on http protocol [Here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
   3. REST API & API Endpoints
      1. Speaking from the context of modern N-tier web applications, every client has to hit a REST end-point to fetch the data from the backend.
      2. The backend application code has a REST-API implemented which acts as an interface to the outside world requests.
7. REST API
   1. REST
      1. REST stands for Representational State Transfer.
      2. It’s a software architectural style for implementing web services
   2. REST API
      1. A REST API is an API implementation that adheres to the REST architectural constraints.
      2. A REST API takes advantage of the HTTP methodologies to establish communication between the client and the server.
      3. The communication between the client and the server is a stateless process.
      4. every time a client interacts with the backend, it has to send the authentication information to it as well.
      5. his entirely decouples the backend & the client code.
   3. Decoupling Clients & the Backend Service
      1. With the availability of the endpoints, the backend service does not have to worry about the client implementation
      2. Developers can have different implementations with separate codebases, for different clients, be it a mobile browser, a desktop browser, a tablet or an API testing tool.
      3. Introducing new types of clients or modifying the client code has no effect on the functionality of the backend service.
      4. This means the clients and the backend service are decoupled.
   4. Application Development Before the REST API
      1. We often tightly coupled the backend code with the client. JSP (Java Server Pages) is one example of it.
8. API Gateway
   1. ![API Gateway](images/APIGateway.jpg)
   2. The REST-API acts as a gateway, as a single entry point into the system.
   3. It encapsulates the business logic.
   4. taking care of the authorization, authentication, sanitizing the input data & other necessary tasks before providing access to the application resources.
9. modes of data transfer
   1.  ![HTTP PULL vs HTTP PUSH](images/HTTPPullPush.jpg)
   2. HTTP PULL
      1. The client sends the request & the server responds with the data.
      2. This is the default mode
      3. The client pulls the data from the server whenever it requires. And it keeps doing it over and over to fetch the updated data.
      4. Every hit on the server costs the business money & adds more load on the server.
      5. What if there is no updated data available on the server, every time the client sends a request?
      6. The client doesn’t know that, so naturally, it would keep sending the requests to the server over and over.
   3. HTTP PUSH
      1. The client sends the request for particular information to the server, just for the first time, & after that the server keeps pushing the new updates to the client whenever they are available.
      2. This is also known as a Callback.
      3. Client phones the server for information. The server responds, Hey!! I don’t have the information right now but I’ll call you back whenever it is available.
      4. A very common example of this is user notifications.
      5. technologies
         1. Ajax Long polling
         2. Web Sockets
         3. HTML5 Event Source
         4. Message Queues
         5. Streaming over HTTP
10. HTTP Pull - Polling with Ajax
    1. AJAX
       1. Asynchronous JavaScript & XML
       2. The name says it all, it is used for adding asynchronous behaviour to the web page.
       3. AJAX uses an XMLHttpRequest object for sending the requests to the server which is built-in the browser
    2. This dynamic technique of requesting information from the server after regular intervals is known as Polling.
11. HTTP PUSH
    1. Time To Live (TTL)
       1. In the regular client-server communication, which is HTTP PULL, there is a Time to Live (TTL) for every request. It could be 30 secs to 60 secs, varies from browser to browser.
       2. If the client doesn’t receive a response from the server within the TTL, the browser kills the connection
       3. Open connections consume resources & there is a limit to the number of open connections a server can handle at one point in time.
       4. Hence, the TTL is used in client-server communication.
    2. Persistent Connection
       1. A persistent connection is a network connection between the client & the server that remains open for further requests & the responses, as opposed to being closed after a single communication.
    3. Heartbeat Interceptors
       1. The connection between the client and the server stays open with the help of Heartbeat Interceptors.
       2. These are just blank request responses between the client and the server to prevent the browser from killing the connection.
    4. Resource Intensive
       1. Persistent connections consume a lot of resources in comparison to the HTTP Pull behaviour.
    5. Technologies
       1. Web Sockets
          1. Is not supported in HTTP/2
          2. A Web Socket connection is ideally preferred when we need a persistent bi-directional low latency data flow from the client to server & back.
          3. Web Sockets tech doesn’t work over HTTP. It runs over TCP.
          4. The server & the client should both support web sockets or else it won’t work.
       2. AJAX – Long Polling
          1. Long Polling lies somewhere between Ajax & Web Sockets.
          2. In this technique instead of immediately returning the response, the server holds the response until it finds an update to be sent to the client
          3. The server doesn’t return an empty response.
          4. If the connection breaks, the client has to re-establish the connection to the server.
          5. Long polling can be used in simple asynchronous data fetch use cases when you do not want to poll the server every now & then.
       3. HTML5 Event Source API & Server Sent Events
          1. Instead of the client polling for data, the server automatically pushes the data to the client whenever the updates are available
          2. The incoming messages from the server are treated as Events.
          3. To implement server-sent events, the backend language should support the technology
          4. On the UI HTML5 Event source API is used to receive the data in-coming from the backend.
          5. The data flow is in one direction only, that is from the server to the client.
          6. SSE is ideal for scenarios such as a real-time feed like that of Twitter, displaying stock quotes on the UI, real-time notifications etc.
          7. Pros
             1. Light weight
             2. HTTP & HTTP/2 compatible
          8. Cons
             1. Proxy is tricky
             2. Stateful
       4. Streaming Over HTTP
          1. Streaming Over HTTP is ideal for cases where we need to stream large data over HTTP by breaking it into smaller chunks
          2. This is possible with HTML5 & a JavaScript Stream API.
          3. The technique is primarily used for streaming multimedia content, like large images, videos etc, over HTTP.
          4. To stream data, both the client & the server agree to conform to some streaming settings.
12. Summary
    1. Long polling has a connection open time slightly longer than the polling mechanism.
    2. Web Sockets have bi-directional data flow
    3. Server sent events facilitate data flow from the server to the client.
    4. Streaming over HTTP facilitates streaming of large objects like multi-media files.
13. Client-Side Vs Server-Side Rendering
    1. Client-Side Rendering
       1. Browser has to render the response on the window in the form of an HTML page.
       2. For this, the browser has several components, such as the:
          1. Browser engine
          2. Rendering engine
          3. JavaScript interpreter
          4. Networking & the UI backend
          5. Data storage etc.
       3. The rendering engine constructs the DOM tree, renders & paints the construction.
    2. Server-Side Rendering
       1. To avoid all this rendering time on the client, developers often render the UI on the server, generate HTML there & directly send the HTML page to the UI.
       2. It ensures faster rendering of the UI, averting the UI loading time in the browser window since the page is already created & the browser doesn’t have to do much assembling & rendering work.
    3. Use Cases For Server-Side & Client-Side Rendering
       1. The server-side rendering approach is perfect for delivering static content, such as WordPress blogs.
       2. It’s also good for SEO as the crawlers can easily read the generated content.
       3. A big downside to this is once the number of concurrent users on the website rises, it puts an unnecessary load on the server.
       4. Client-side rendering works best for modern dynamic Ajax-based websites.
       5. We can use server-side rendering for the home page & for the other static content on our website & use client-side rendering for the dynamic pages.