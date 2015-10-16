title: real time communication, server push
date: 2015-10-08 09:42:39
tags:
toc: true
---

# Concpet
## Message Oriented Middleware (MOM)
Asynchronous Messaging, fire-and-forget, evnet-driven architechure

Systems that rely upon synchronous requests typically have a limited ability to scale because eventually requests will begin to back up, thereby slowing the whole system.

### Refernces
[In which domains are message oriented middleware like AMQP useful?](http://stackoverflow.com/questions/2388539/in-which-domains-are-message-oriented-middleware-like-amqp-useful)
[Message Queue Evaluation Notes](http://wiki.secondlife.com/wiki/Message_Queue_Evaluation_Notes#Criteria)
[Messaging Patterns Overview](http://www.enterpriseintegrationpatterns.com/patterns/messaging/index.html)
## Reactive Programming
### Refernces
[FRP與函數式](https://www.evernote.com/shard/s75/sh/20e03309-c4b7-4a6a-9440-048f43526f90/a46385724a71c34839213c719b360d79)

## websocket
[w3c](http://www.w3.org/TR/websockets/)

### websocket communication by Java (server-side)
[JSR 356, Java API for WebSocket](http://www.oracle.com/technetwork/articles/java/jsr356-1937161.html)
[Java Day pdf](http://javaday.org.ua/2013/images/pdf/Delabassee_Kiev_WebSocket.pdf)
[Securing WebSocket applications on Glassfish](https://blogs.oracle.com/PavelBucek/entry/securing_websocket_applications_on_glassfish)




# Server (message broker, gateway)
[alternatives](https://dzone.com/refcardz/html5-websocket)
- https://www.process-one.net/en/ejabberd/#getejabberd
- http://www.rabbitmq.com/
- http://activemq.apache.org/
- http://kaazing.org/
The Gateway is a network gateway created to provide a single access point for real-time web based protocol elevation that supports **load balancing, clustering, and security management**. It is designed to provide scalable and secure bidirectional event-based communication over the web; **on every platform, browser, and device**.

 - Requirement
   - Java Runtime Environment (JRE) 1.7.0_21 or higher
   - JAVA_HOME must be set

 - Feature
   - cluster -> [參考連結](http://developer.kaazing.com/documentation/5.0/high-availability/u_ha.html)
   - [AWS marketplace](http://developer.kaazing.com/documentation/aws/marketplace/index.html)
   - [About Security with KAAZING Gateway](http://developer.kaazing.com/documentation/5.0/security/c_sec_security.html)
   - [WebSocket Emulation for older browsers](http://kaazing.com/products/kaazing-websocket-gateway/websocket-emulation/)
- http://caucho.com/
- http://www.lightstreamer.com/
 - http://www.slideshare.net/alinone/from-push-technology-to-the-realtime-web
- https://www.ejabberd.im/

[消息队列软件产品大比拼](https://www.evernote.com/shard/s75/sh/3eb6cf33-71db-4412-973d-7d7efac62d47/02330b3286d02dd6558129f4ec914c75)
## jWebsocket
[jWebsocket official site](http://jwebsocket.org/)
[jWebSocket JMS based Cluster](http://jwebsocket.org/documentation/installation-guide/jwebsocket-cluster)

## WebSocket over TLS (GlassFish)

### preview

![](ws-echo-server1.png)
![](ws-echo-server2.png)
![](ws-echo-server3.png)


### server-side

`web.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
...
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Protected resource</web-resource-name>
      <url-pattern>/*</url-pattern>
      <http-method>GET</http-method>
    </web-resource-collection>

    <!-- https -->
    <user-data-constraint>
      <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
  </security-constraint>
</web-app>
```


`EchoEndpoint.java`
```java
package tw.henry.websocket;

import java.io.IOException;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.Set;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.ScheduledFuture;
import java.util.concurrent.TimeUnit;
import java.util.logging.Level;
import java.util.logging.Logger;

import javax.websocket.OnClose;
import javax.websocket.OnMessage;
import javax.websocket.OnOpen;
import javax.websocket.Session;
import javax.websocket.server.ServerEndpoint;


@ServerEndpoint("/echo")
public class EchoEndpoint {
	private static final Logger LOG = Logger.getLogger(EchoEndpoint.class.getName());

	private static Set<Session> allSessions;

	static ScheduledExecutorService timer =
		       Executors.newSingleThreadScheduledExecutor();
	DateTimeFormatter timeFormatter =  
	          DateTimeFormatter.ofPattern("HH:mm:ss");

	ScheduledFuture<?> result;
	@OnMessage
	public String echo(String message) {
	    return message + " (from your server)";
	}

	@OnOpen
	public void connectionOpened(Session session) {
		LOG.log(Level.INFO, "WebSocket opened: "+session.getId());

		allSessions = session.getOpenSessions();

		if (allSessions.size()==1){   
	        result = timer.scheduleAtFixedRate(
	             () -> sendTimeToAll(session),0,10,TimeUnit.SECONDS);    
	    }
	}

	private void sendTimeToAll(Session session){       
	     allSessions = session.getOpenSessions();
	     for (Session sess: allSessions){          
	        try{   
	          sess.getBasicRemote().sendText("Hi, give me some thing to echo (Server time: " +
	                    LocalTime.now().format(timeFormatter)+")");
	          } catch (IOException ioe) {        
	              System.out.println(ioe.getMessage());         
	          }   
	     }  
	}

	@OnClose
	public void connectionClosed() {
		result.cancel(true);
		LOG.log(Level.INFO, "connection closed");
	}
}
```


### client-side: Web
```html
<html>

<head>
  <meta http-equiv="content-type" content="text/html; charset=ISO-8859-1">
</head>

<body>
  <meta charset="utf-8">
  <title>Web Socket JavaScript Echo Client</title>
  <script language="javascript" type="text/javascript">
    var endpointPath = "/echo";
    var wsUri = getRootUri() + endpointPath;
    var websocket;
    /**
     * Get application root uri with ws/wss protocol.
     *
     * @returns {string}
     */
    function getRootUri() {
      var uri = "wss://" + (document.location.hostname == "" ? "localhost" : document.location.hostname) + ":" +
        (document.location.port == "" ? "8181" : document.location.port);

      var pathname = window.location.pathname;

      if (endsWith(pathname, "/index.html")) {
        uri = uri + pathname.substring(0, pathname.length - 11);
      } else if (endsWith(pathname, "/")) {
        uri = uri + pathname.substring(0, pathname.length - 1);
      }

      return uri;
    }

    function endsWith(str, suffix) {
      return str.indexOf(suffix, str.length - suffix.length) !== -1;
    }

    function init() {
      output = document.getElementById("output");
    }

    function send_echo() {
      if (!websocket) {

        websocket = new WebSocket(wsUri);

        websocket.onopen = function(evt) {
          onOpen(evt)
        };
        websocket.onmessage = function(evt) {
          onMessage(evt)
        };
        websocket.onerror = function(evt) {
          onError(evt)
        };
        websocket.onclose = function(evt) {
          onClose(evt);
        }
      }
      // doSend(textID.value);
      sendMessage(textID.value);
    }

    function onOpen(evt) {
      writeToScreen("CONNECTED");
    }

    function onMessage(evt) {
      writeToScreen("RECEIVED: " + evt.data);
    }

    function onClose(evt) {
      writeToScreen("CLOSED: " + evt.code + ": " + evt.reason);
    }

    function onError(evt) {
      writeToScreen('<span style="color: red;">ERROR:</span> ' + evt.data);
    }

    function doSend(message) {
      console.log(websocket);
      writeToScreen("SENT: " + message);
      websocket.send(message);
    }

    function sendMessage(msg) {
      waitForSocketConnection(websocket, function() {
    	    writeToScreen("SENT: " + msg);
        websocket.send(msg);
      });
    };

    function waitForSocketConnection(socket, callback) {
      setTimeout(
        function() {
          if (socket.readyState === WebSocket.OPEN) {
            if (callback !== undefined) {
              callback();
            }
            return;
          } else {
            waitForSocketConnection(socket, callback);
          }
        }, 5);
    };

    function writeToScreen(message) {
      var pre = document.createElement("p");
      pre.style.wordWrap = "break-word";
      pre.innerHTML = message;
      //alert(output);
      output.appendChild(pre);
    }

    window.addEventListener("load", init, false);
  </script>

  <h2 style="text-align: center;">Web Socket Echo Client</h2>

  <div style="text-align: center;">
    <img style=" width: 64px; height: 64px;" alt="" src="HTML5_Logo_512.png">
  </div>
  <br/>

  <div style="text-align: center;">
    <form action="">
      <input onclick="send_echo()" value="Press me" type="button">
      <input id="textID" name="message" label="message" value="Hello Web Sockets !" type="text">
      <br>
    </form>
  </div>
  <div id="output"></div>
</body>

</html>

```

### client-side : Android



### Reference
[Connect and transfer data with secure WebSockets in Android](http://www.juliankrone.com/connect-and-transfer-data-with-secure-websockets-in-android/)





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
- https://www.hydna.com/
- https://www.pubnub.com/
- https://www.intercom.io/
- https://cloud.google.com/pubsub/

[Scaling Secret: Real-time Chat](https://medium.com/@davidbyttow/scaling-secret-real-time-chat-d8589f8f0c9b)

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

# whatsapp
[What is the technology behind the web-based version of WhatsApp?](https://www.quora.com/What-is-the-technology-behind-the-web-based-version-of-WhatsApp)

# 加解密
[POST over HTTPS “secure enough” for sensitive data?](http://security.stackexchange.com/questions/51069/post-over-https-secure-enough-for-sensitive-data)
