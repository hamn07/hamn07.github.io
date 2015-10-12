title: real time communication, server push
date: 2015-10-08 09:42:39
tags:
---
<!-- toc -->
# Concpet
## Message Oriented Middleware (MOM)
Asynchronous Messaging, fire-and-forget, evnet-driven architechure

Systems that rely upon synchronous requests typically have a limited ability to scale because eventually requests will begin to back up, thereby slowing the whole system.

### Refernces
[In which domains are message oriented middleware like AMQP useful?](http://stackoverflow.com/questions/2388539/in-which-domains-are-message-oriented-middleware-like-amqp-useful)

## Reactive Programming
### Refernces
[FRP與函數式](https://www.evernote.com/shard/s75/sh/20e03309-c4b7-4a6a-9440-048f43526f90/a46385724a71c34839213c719b360d79)

## websocket
[w3c](http://www.w3.org/TR/websockets/)

### websocket communication by Java (server-side)
[JSR 356, Java API for WebSocket](http://www.oracle.com/technetwork/articles/java/jsr356-1937161.html)
[Java Day pdf](http://javaday.org.ua/2013/images/pdf/Delabassee_Kiev_WebSocket.pdf)
[Securing WebSocket applications on Glassfish](https://blogs.oracle.com/PavelBucek/entry/securing_websocket_applications_on_glassfish)




# [Server](https://dzone.com/refcardz/html5-websocket) (message broker, gateway)
- https://www.process-one.net/en/ejabberd/#getejabberd
- http://www.rabbitmq.com/
- http://activemq.apache.org/
- http://kaazing.org/
- http://caucho.com/

## [jWebsocket](http://jwebsocket.org/)
[jWebSocket JMS based Cluster](http://jwebsocket.org/documentation/installation-guide/jwebsocket-cluster)

## GlassFish-Eclipse development Env. setup
### Environment

1. JDK 8
2. GlassFish 4 Java EE 7 Full Platform
3. Eclipse (Mars Release) IDE for Java EE Developers


### Setup Steps

1. enter Eclipse preferences `hotkey: cmd+,`, preferences->Server->Runtime Environment->Add...
![](glassfish-eclipse-1.png)

2. no glashfish environment runtime found, click `Download additional server adapters`
![](glassfish-eclipse-2.png)

3. choose `GlassFish Tools`
![](glassfish-eclipse-3.png)

4. restart Eclipse after installaction completes
![](glassfish-eclipse-4.png)

5. repeat step 1.~2., GlassFish runtime should appear, choose GlassFish 4
![](glassfish-eclipse-6.png)

6. locate your glassfish4 path
![](glassfish-eclipse-5.png)

7. use Wizard to create GlassFish Server `hotkey: cmd+n`
![](glassfish-eclipse-7.png)

8. choose GlassFish 4
![](glassfish-eclipse-8.png)

9. setup administrator name and password, finish setup
![](glassfish-eclipse-9.png)

10. Start Server
![](glassfish-eclipse-10.png)

11. visit http://localhost:8080/ to see if GlassFish works properly.
![](glassfish-eclipse-11.png)

### Refernces

[Multiple JDK in Mac OSX 10.10 Yosemite](https://www.evernote.com/shard/s75/sh/b3bab388-37e0-4945-8a3e-eda3fb9e398c/8e4b3a2fb69ab2d662a36db15230201d)

[Eclipse Marketplace GlassFish Tools](https://www.evernote.com/shard/s75/sh/a8635da6-efa0-4eda-a3a7-0a79ba6315d0/f8b95301cf59fed2b8993ad263e9cb72)

[GlassFish Download Page](https://glassfish.java.net/download.html)

[JDK Download Page](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

[Eclipse download Page](https://www.eclipse.org/downloads/)

# Cloud Service (SaaS)
- http://framework.realtime.co/
- https://pusher.com/
- https://www.pubnub.com/
- https://ejabberd-saas.com/
- https://www.mulesoft.com/

# Protocol
- STOMP: Simple (or Streaming) Text Oriented Messaging Protocol
 - it’s not always straightforward to port code between brokers
- XMPP : Extensible Messaging and Presence Protocol
- AQMP : Advanced Message Queuing Protocol
- [MQTT](https://github.com/mqtt/mqtt.github.io/wiki) : Message Queue Telemery Transport
 - Can be applied to IoT, such as connecting an Arduino device to a web service with MQTT.
- JMS : Java Message Service

## Refernces
[Choosing Your Messaging Protocol: AMQP, MQTT, or STOMP
](https://blogs.vmware.com/vfabric/2013/02/choosing-your-messaging-protocol-amqp-mqtt-or-stomp.html)
