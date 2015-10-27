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

### RFC 6455
[ieft official](https://tools.ietf.org/html/rfc6455)

#### 5.2 Base Framing Protocol

Let's examin our framing logic base by rfc6455 framing protocol as below.



```php
$msg = 'hi';

echo bstr2bin(frame($msg));

function frame($s) {
  // our framing logic
  $a = str_split($s, 125);
  if (count($a) == 1) {
    return "\x81".chr(strlen($a[0])).$a[0];
  }

  $ns = "";
  foreach ($a as $o) {
    $ns .= "\x81".chr(strlen($o)).$o;
  }
  return $ns;
}

function bstr2bin($input)
// Binary representation of a binary-string
{
  if (!is_string($input)) return null; // Sanity check

  // Unpack as a hexadecimal string
  $value = unpack("H*", $input);

  // Output binary representation
  return base_convert($value[1], 16, 2);
}
```

while sent hi as message, the output would be `10000001000000100110100001101001` in binary. Let's fill in base frame protocol table as below.


```bash
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-------+-+-------------+-------------------------------+
|F|R|R|R| opcode|M| Payload len |         payload Data (hi)     |
|I|S|S|S|  (4)  |A|     (7)     |             (16)              |
|N|V|V|V|       |S|             |                               |
| |1|2|3|       |K|             |                               |
+-+-+-+-+-------+-+-------------+-------------------------------+
|1|0|0|0|0 0 0 1|0|0 0 0 0 0 1 0|0 1 1 0 1 0 0 0 0 1 1 0 1 0 0 1|
+-+-+-+-+-------+-+-------------+-------------------------------+
```

\x81 are 2 hex; 10000001 in binary.

FIN=1 denotes a final frame
> FIN:  1 bit
>
> Indicates that this is the final fragment in a message.  The first
> fragment MAY also be the final fragment.



RSV1=0
RSV2=0
RSV3=0

RSV1~3 are set to 0, denotes we don't use any extension.
> RSV1, RSV2, RSV3:  1 bit each
>
> MUST be 0 unless an extension is negotiated that defines meanings for non-zero values.  If a nonzero value is received and none of the negotiated extensions defines the meaning of such a nonzero value, the receiving endpoint MUST \_Fail the WebSocket Connection_.


opcode=0001 denotes a text frame
> Opcode:  4 bits
>
> Defines the interpretation of the "Payload data".  If an unknown opcode is received, the receiving endpoint MUST \_Fail the WebSocket Connection_.  The following values are defined.
>
>      *  %x0 denotes a continuation frame
>
>      *  %x1 denotes a text frame
>
>      *  %x2 denotes a binary frame
>
>      *  %x3-7 are reserved for further non-control frames
>
>      *  %x8 denotes a connection close
>
>      *  %x9 denotes a ping
>
>      *  %xA denotes a pong
>
>      *  %xB-F are reserved for further control frames

`chr(strlen($a[0]))` returns a specific charater according to frame length, since we limit frame length to 125, first binary would be 0.

Mask=0 denotes no mask
> Mask:  1 bit
>
>   Defines whether the "Payload data" is masked.  If set to 1, a
>   masking key is present in masking-key, and this is used to unmask
>   the "Payload data" as per Section 5.3.  All frames sent from
>   client to server have this bit set to 1.

Payload length= 0000010
in this example, 'hi' is a 2 charater data, '0000010' in binary.
> Payload length:  7 bits, 7+16 bits, or 7+64 bits
>
>   The length of the "Payload data", in bytes: if 0-125, that is the
>   payload length.  If 126, the following 2 bytes interpreted as a
>   16-bit unsigned integer are the payload length.  If 127, the
>   following 8 bytes interpreted as a 64-bit unsigned integer (the
>   most significant bit MUST be 0) are the payload length.  Multibyte
>   length quantities are expressed in network byte order.  Note that
>   in all cases, the minimal number of bytes MUST be used to encode
>   the length, for example, the length of a 124-byte-long string
>   can't be encoded as the sequence 126, 0, 124.  The payload length
>   is the length of the "Extension data" + the length of the
>   "Application data".  The length of the "Extension data" may be
>   zero, in which case the payload length is the length of the
>   "Application data".

Payload Data=0110100001101001
since we limit our frame length to 125, the remaining bytes are payload.
01101000 is 'h' in binary
01101001 is 'i' in binary
> Application data:  y bytes
>
> Arbitrary "Application data", taking up the remainder of the frame
> after any "Extension data".  The length of the "Application data"
> is equal to the payload length minus the length of the "Extension
> data".


Note: Further discussion would be needed while migration to another platform language which already implements WebSocket (like Java).


### Refernces
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
- [apache karaf](http://karaf.apache.org/)
Apache Karaf is a small OSGi based runtime which provides a lightweight container onto which various components and applications can be deployed.
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

## GlassFish implements WebSocket over TLS

> This example demostrate a echo server peroidically return server time via websocket connection.


### preview

![](ws-echo-server1.png)
![](ws-echo-server2.png)
![](ws-echo-server3.png)


### server configuration

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

### server-side

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

```java
import android.os.Build;
import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.util.Log;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;

import org.java_websocket.client.DefaultSSLWebSocketClientFactory;
import org.java_websocket.client.WebSocketClient;
import org.java_websocket.drafts.Draft_17;
import org.java_websocket.handshake.ServerHandshake;

import java.net.URI;
import java.net.URISyntaxException;

import javax.net.ssl.SSLContext;
import javax.net.ssl.TrustManager;
import javax.net.ssl.X509TrustManager;


public class MainActivity extends AppCompatActivity {
    private WebSocketClient mWebSocketClient;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        try {

 //           connectWebSocket(new URI("ws://10.0.3.2:8080/tm.EchoServer/echo"),false);
//           connectWebSocket(new URI("wss://10.0.3.2:8181/tm.EchoServer/echo"),true);
//           connectWebSocket(new URI("ws://10.0.1.147:8080/tm.EchoServer/echo"),false);
           connectWebSocket(new URI("wss://10.0.1.147:8181/tm.EchoServer/echo"),true);

        } catch (URISyntaxException e) {
            e.printStackTrace();
        }
    }

    private void connectWebSocket(URI uri, boolean overTLS) {


        mWebSocketClient = new WebSocketClient(uri, new Draft_17()) {
            @Override
            public void onOpen(ServerHandshake serverHandshake) {
                Log.i("Websocket", "Opened");
                mWebSocketClient.send("Hello from " + Build.MANUFACTURER + " " + Build.MODEL);
            }

            @Override
            public void onMessage(String s) {
                final String message = s;
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        TextView textView = (TextView)findViewById(R.id.messages);
                        textView.setText(textView.getText() + "\n" + message);
                    }
                });
            }

            @Override
            public void onClose(int i, String s, boolean b) {
                Log.i("Websocket", "Closed " + s);
            }

            @Override
            public void onError(Exception e) {
                Log.i("Websocket", "Error " + e.getMessage());
            }
        };

        if (overTLS) {
            /***************************************************************************/
            //This part is needed in case you are going to use self-signed certificates
            TrustManager[] trustAllCerts = new TrustManager[]{new X509TrustManager() {
                @Override
                public void checkClientTrusted(java.security.cert.X509Certificate[] chain, String authType) throws java.security.cert.CertificateException {

                }

                @Override
                public void checkServerTrusted(java.security.cert.X509Certificate[] chain, String authType) throws java.security.cert.CertificateException {

                }

                public java.security.cert.X509Certificate[] getAcceptedIssuers() {
                    return new java.security.cert.X509Certificate[]{};
                }

            }};
            /**************************************************************************/
            try {
                SSLContext sc = SSLContext.getInstance("TLS");
                sc.init(null, trustAllCerts, new java.security.SecureRandom());

                //Otherwise the line below is all that is needed.
                //sc.init(null, null, null);
                mWebSocketClient.setWebSocketFactory(new DefaultSSLWebSocketClientFactory(sc));
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

        mWebSocketClient.connect();
    }

    public void sendMessage(View view) {
        EditText editText = (EditText)findViewById(R.id.message);
        mWebSocketClient.send(editText.getText().toString());
        editText.setText("");
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        mWebSocketClient.close();

    }
}

```

### Reference
[Connect and transfer data with secure WebSockets in Android](http://www.juliankrone.com/connect-and-transfer-data-with-secure-websockets-in-android/)





## GlassFish-Eclipse development Env. setup
### Environment

1. JDK 8
```bash
$ java -version
java version "1.8.0_45"
Java(TM) SE Runtime Environment (build 1.8.0_45-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.45-b02, mixed mode)
```
2. GlassFish 4 Java EE 7 Full Platform
![](capture-20151016-154243.png)
3. Eclipse (Mars Release) IDE for Java EE Developers


### Setup Steps

1. goto Eclipse preferences `hotkey: cmd+,`, preferences->Server->Runtime Environment->Add...
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
By using standard protocol instead of proprietary one, we could leverage lots of client and server implementations to quickly build our app.
- STOMP: Simple (or Streaming) Text Oriented Messaging Protocol
 - it’s not always straightforward to port code between brokers
- XMPP : Extensible Messaging and Presence Protocol
  - http://igniterealtime.org/
- AQMP : Advanced Message Queuing Protocol
  - Except puducer,broker,consumer(like JMS), AQMP introduce new component 'exchange'
- [MQTT](https://github.com/mqtt/mqtt.github.io/wiki) : Message Queue Telemery Transport
 - Can be applied to IoT, such as connecting an Arduino device to a web service with MQTT.
- JMS : Java Message Service
- Protocol Buffers

## Refernces
[Message Queue Evaluation Notes](http://wiki.secondlife.com/wiki/Message_Queue_Evaluation_Notes)
[Choosing Your Messaging Protocol: AMQP, MQTT, or STOMP
](https://blogs.vmware.com/vfabric/2013/02/choosing-your-messaging-protocol-amqp-mqtt-or-stomp.html)

# whatsapp
[The WhatsApp Architecture Facebook Bought For $19 Billion - High Scalability -](https://www.evernote.com/shard/s75/sh/caec8dac-1026-4603-bab4-d241c9e1e1e3/bea5136188b0948f22aea9f65e5652e4)
[INSIDE ERLANG, THE RARE PROGRAMMING LANGUAGE BEHIND WHATSAPP'S SUCCESS](https://www.evernote.com/shard/s75/sh/5a371dae-b43c-4229-8717-4d5bb1d031a5/a43f440b05685b66b342bd7c0ad061f9)
[What is the technology behind the web-based version of WhatsApp?](https://www.quora.com/What-is-the-technology-behind-the-web-based-version-of-WhatsApp)
- chat history is only stored on phone, none on server. Thus, to use the web client your smartphone has to be connected to the internet.
- What protocol is used in Whatsapp app? SSL socket to the WhatsApp server pools.
- Erlang/FreeBSD-based server infrastructure
  - Server systems that do the backend message routing are done in Erlang.
    - Ericsson engineer Joe Armstrong developed Erlang with the logic of telecommunications in mind: millions of parallel conversations happening at the same time, with almost zero tolerance for downtime.
    - Erlang allows for bug fixes and updates without downtime.
    - Erlang is very good at efficiently executing commands across processors within a single machine.
  - Great achievement is that the number of active users is managed with a really small server footprint. Team consensus is that it is largely because of Erlang.
  - Interesting to note Facebook Chat was written in Erlang in 2009, but they went away from it because it was hard to find qualified programmers.
- WhatsApp server has started from ejabberd
  - Ejabberd is a famous open source Jabber server written in Erlang.
  - Originally chosen because its open, had great reviews by developers, ease of start and the promise of Erlang’s long term suitability for large communication system.
  - The next few years were spent re-writing and modifying quite a few parts of ejabberd, including switching from XMPP to internally developed protocol, restructuring the code base and redesigning some core components, and making lots of important modifications to Erlang VM to optimize server performance.
- A primary gauge of system health is message queue length. The message queue length of all the processes on a node is constantly monitored and an alert is sent out if they accumulate backlog beyond a preset threshold. If one or more processes falls behind that is alerted on, which gives a pointer to the next bottleneck to attack.
- Multimedia messages are sent by uploading the image, audio or video to be sent to an HTTP server and then sending a link to the content along with its Base64 encoded thumbnail (if applicable).
## Erlang
- The basic unit of concurrency in Erlang is the process.
- An Erlang process is a little virtual machine that can evaluate a single Erlang function; it should not be confused with an operating system process.
- cannot rebind variable.


# encryption
## Concept
[What is SSL?](http://info.ssl.com/article.aspx?id=10241)
## certificate transparency
[免費申請 StartSSL™ 個人數位簽章與網站 SSL 憑證完全攻略](https://www.evernote.com/shard/s75/sh/7ad82494-f38b-40f6-a14f-ad78370c2f8f/b7b87d174d5d7337d4f8e1bd5140fc07)
[Symantec員工誤發Google憑證被開除](http://www.ithome.com.tw/news/98897)
## the necessity to encrypt-decrypt again
[POST over HTTPS “secure enough” for sensitive data?](http://security.stackexchange.com/questions/51069/post-over-https-secure-enough-for-sensitive-data)
## alternatives
[digicert](https://www.digicert.com/), used by facebook / whatsapp
