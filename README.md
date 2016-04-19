##Name attributes of HTTP protocol makes it difficult to use for real time systems. 

Weird question? - refer to related questions below.

##Explain polling and long-polling strategies, their pros and cons. 
Current attempts to provide real-time web applications largely revolve around polling and other server-side push technologies, the most notable of which is Comet, which delays the completion of an HTTP response to deliver messages to the client. Comet-based push is generally implemented in JavaScript and uses connection strategies such as long-polling or streaming.

####Polling
With polling, the browser sends HTTP requests at regular intervals and immediately receives a response. This technique was the first attempt for the browser to deliver real-time information. Obviously, this is a good solution if the exact interval of message delivery is known, because you can synchronize the client request to occur only when information is available on the server. However, real-time data is often not that predictable, making unnecessary requests inevitable and as a result, many connections are opened and closed needlessly in low-message-rate situations.
####Long-polling
With long-polling, the browser sends a request to the server and the server keeps the request open for a set period. If a notification is received within that period, a response containing the message is sent to the client. If a notification is not received within the set time period, the server sends a response to terminate the open request. It is important to understand, however, that when you have a high message volume, long-polling does not provide any substantial performance improvements over traditional polling. In fact, it could be worse, because the long-polling might spin out of control into an unthrottled, continuous loop of immediate polls.

*sources*<br>
[Websocket.org - HTML5 WebSocket: A Quantum Leap in Scalability for the Web](http://www.websocket.org/quantum.html)<br>

##What is HTTP streaming, SSE (Server sent events)? 
With streaming, the browser sends a complete request, but the server sends and maintains an open response that is continuously updated and kept open indefinitely (or for a set period of time). The response is then updated whenever a message is ready to be sent, but the server never signals to complete the response, thus keeping the connection open to deliver future messages. Streaming includes HTTP headers which increases the file size, increasing delay. This can be considered as a major drawback.

*sources*<br>
[Websocket.org - HTML5 WebSocket: A Quantum Leap in Scalability for the Web](http://www.websocket.org/quantum.html)<br>
[Tutorialspoint - Websockets Duplex Communication](http://www.tutorialspoint.com/websockets/websockets_duplex_communication.htm)<br>

##What is WebSocket protocol, how is it different from HTTP communication, what advantages it has over HTTP?
Ultimately, all of these methods (polling, long-polling and http streaming) involve HTTP request and response headers, which contain lots of additional, unnecessary header data and introduce latency. Full-duplex connectivity requires more than just the downstream connection from server to client. In an effort to simulate full-duplex communication over half-duplex HTTP, many of today's solutions use two connections: one for the downstream and one for the upstream. The maintenance and coordination of these two connections introduces significant overhead in terms of resource consumption and adds lots of complexity. <br>
Simply put, HTTP wasn't designed for real-time, full-duplex communication.

HTML5 Web Sockets represents the next evolution of web communications—a **full-duplex**, **bidirectional** communications channel that operates through a **single socket** over the Web. HTML5 Web Sockets provides a true standard that you can use to build scalable, real-time web applications. In addition, since it provides a socket that is native to the browser, it eliminates many of the problems Comet solutions are prone to. Web Sockets removes the overhead and dramatically reduces complexity.

*sources*<br>
[Websocket.org - HTML5 WebSocket: A Quantum Leap in Scalability for the Web](http://www.websocket.org/quantum.html)<br>
 
##Explain what the WebSocket Protocol brings to the Web-world. 
Normally when a browser visits a web page, an HTTP request is sent to the web server that hosts that page. The web server acknowledges this request and sends back the response. In many cases—for example, for stock prices, news reports, ticket sales, traffic patterns, medical device readings, and so on—the response could be stale by the time the browser renders the page. If you want to get the most up-to-date "real-time" information, you can constantly refresh that page manually, but that's obviously not a great solution.<br>
**Also refer to previous question.**

*sources*<br>
[Websocket.org - HTML5 WebSocket: A Quantum Leap in Scalability for the Web](http://www.websocket.org/quantum.html)<br>

##Explain and demonstrate the process of WebSocket communication - From connecting client to server, through sending messages, to closing connection. 

*insert explanation here...*

![](https://www.pubnub.com/static/images/get-started/websockets_guides.png)

*sources* <br>
[pubnub.com](https://www.pubnub.com/websockets/)
[Githubproject - SimpleChat](https://github.com/hardboilr/SimpleChat)<br>

##What's the advantage of using libraries like Socket.IO, Sock.JS, WS, over pure WebSocket libraries in the backend and standard APIs on frontend? Which problems do they solve? 

(answer based on socket.io)

- Abstraction layer with API's for both server and client<br>
- It allows developers to send and receive data without worrying about cross-browser compatibility. <br>
- Fallbacks to polling with incompatible browsers.

*sources*<br>
[Nodesource.com](https://nodesource.com/blog/understanding-socketio/)<br>

##What is Backend as a Service, Database as a Service, why would you consider using Firebase in your projects?

*sources*<br>
[Githubproject - FirebaseChatExample](https://github.com/hardboilr/FirebaseChatExample)<br> 

##Explain the pros & cons of using a Backend as a Service Provider like Firebase. 

+ + A lot of Realtime functionality is built for you (three-way binding, sockets etc.).
+ + Built in Database (JSON) and hosting.
+ + Built in Scaling 
+ + Built in Security (just configure your rules).
+ + Cross Platform API (for Web, IOS, Android and utilize REST as well)
+ - Firebase service is down -> your service is down etc. (always the case when someone else hosts your service, although they will often be better at hosting than you - uptime, security and so on.
+ - Vendor lock-in (will be a huge headache to migrate to another service)
+ - Probably cheaper to self-host at places like Amazon AWS (building your own backend)

##Explain and demonstrate “three-way data binding” using Firebase and Angular 

In AngularJS our scope model and view stay in sync thanks to the two way data binding (ng-model). When using FireBase as a backend, three way binding is possible. You can bind your model data to a FireBase location (ex. "https://xxx.firebaseio.com/users", so that whenever your models change, those changes are automatically pushed to FireBase. Similarly, whenever the data at the particular FireBase location changes, your local scope model is also updated. This creates a three way data binding. The obvious benefit is that it lets you create cool realtime apps where the data changes frequently and those modifications are broadcast to all the connected users. 

Refer to [Github project - FireSlackSeed](https://github.com/hardboilr/FireSlackSeed) for example.

*sources*<br>
[sitepoint.com](http://www.sitepoint.com/creating-three-way-data-binding-firebase-angularjs/)<br>
[Github project - FireSlackSeed](https://github.com/hardboilr/FireSlackSeed)<br>
[Firebase Official Docs](https://www.firebase.com/docs/web/libraries/angular/guide/synchronized-objects.html#section-three-way-bindings)<br>

##Explain and demonstrate the difference between the simple chat system in your own WebSocket + Node.js backend vs. Firebase. 

*insert stuff here*