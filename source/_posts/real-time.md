title: real time communication, server push
date: 2015-10-08 09:42:39
tags:
---
<!-- toc -->
# 觀念
## Message Oriented Middleware (MOM)
Asynchronous Messaging, fire-and-forget, evnet-driven architechure

Systems that rely upon synchronous requests typically have a limited ability to scale because eventually requests will begin to back up, thereby slowing the whole system.


> 參考文獻

[In which domains are message oriented middleware like AMQP useful?](http://stackoverflow.com/questions/2388539/in-which-domains-are-message-oriented-middleware-like-amqp-useful)

# Cloud Service (SaaS)
- http://framework.realtime.co/
- https://pusher.com/
- https://www.pubnub.com/
- https://ejabberd-saas.com/

# Server (message broker, gateway)
- https://www.process-one.net/en/ejabberd/#getejabberd
- http://www.rabbitmq.com/
- http://activemq.apache.org/
- http://kaazing.org/
- http://jwebsocket.org/

# GlassFish開發環境建置
`在Eclipse主視窗按下cmd+,叫出preference`
`點擊Add...`
![](glassfish-eclipse-1.png)


`點擊Download additional server adapters`
![](glassfish-eclipse-2.png)


![](glassfish-eclipse-3.png)
![](glassfish-eclipse-4.png)
`重覆上述步驟，在這邊選取GlassFish 4`
![](glassfish-eclipse-6.png)
`輸入GlassFish安裝路徑`
![](glassfish-eclipse-5.png)
`回到Eclipse主視窗按下cmd+N，使用Wizard來建立Server`
![](glassfish-eclipse-7.png)
![](glassfish-eclipse-8.png)
![](glassfish-eclipse-9.png)
![](glassfish-eclipse-10.png)
![](glassfish-eclipse-11.png)
