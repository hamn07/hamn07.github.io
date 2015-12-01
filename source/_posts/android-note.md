title: 安卓筆記區
date: 2015-07-30 09:17:19
tags:
---
![](http://developer.android.com/intl/zh-cn/images/activity_lifecycle.png)
***
![](http://developer.android.com/images/service_lifecycle.png )
[趙老師的雲端分享資料夾](https://drive.google.com/folderview?id=0B5zn2b2xqOwGfm5yYVd2emZrcnN6YTBvbDhpQTY1OGdxSExFWGczMlFzZV9sMFdGUS1UeTg&usp=sharing#list)
<!-- toc -->
# bluetooth
[official guide](http://developer.android.com/intl/zh-cn/guide/topics/connectivity/bluetooth.html)

```xml
<manifest ... >
  <uses-permission android:name="android.permission.BLUETOOTH" />
  <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
  ...
</manifest>
```
# problem to fix
[Android uploading pictures to server in most efficient way](https://www.evernote.com/shard/s75/sh/ef5c662a-4cb3-486e-b24f-c59191df5f39/cdb742b3e18301296d66d002b36fcb2f)

# dialog
1. ProgressDialog
```java
ProgressDialog dialog = new ProgressDialog(this);
dialog.setProgressStyle(ProgressDialog.STYLE_SPINNER);
dialog.setMessage("downloading...");
dialog.show();
dialog.dismiss();
```

# sensor
- 位移
- 環境
- 位置

## example
```xml
    <!--設定device需有三軸加速感應器才可安裝-->
    <uses-feature
        android:name="android.hardware.sensor.accelerometer"
        android:required="true" />
```


```java
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        mgr = (SensorManager) getSystemService(SENSOR_SERVICE);
        List<Sensor> list = mgr.getSensorList(Sensor.TYPE_ALL);


        for (Sensor sensor:list) {
            Log.i("henry",sensor.getName()+" : "+sensor.getType()+" : "+sensor.getVendor());
        }

        sensor = mgr.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
        if (sensor!=null) {
            isSensorEnable=true;
        }
        /**
         * define
         */
        sensorEventListener = new SensorEventListener() {
            @Override
            public void onSensorChanged(SensorEvent event) {
                float[] values = event.values;

                ((TextView)findViewById(R.id.tv1)).setText("x : "+values[0]);
                ((TextView)findViewById(R.id.tv2)).setText("y : "+values[1]);
                ((TextView)findViewById(R.id.tv3)).setText("z : "+values[2]);

                MyView mv = (MyView) findViewById(R.id.mv);

            }

            @Override
            public void onAccuracyChanged(Sensor sensor, int accuracy) {
            }
        };
    }

    @Override
    protected void onResume() {
        super.onResume();
        if (isSensorEnable) {
            mgr.registerListener(sensorEventListener, sensor, SensorManager.SENSOR_DELAY_UI);
        }
    }

    @Override
    protected void onStop() {
        super.onStop();
        if (isSensorEnable) {
            mgr.unregisterListener(sensorEventListener, sensor);
        }
    }
```

# media player
![](http://developer.android.com/intl/zh-cn/images/mediaplayer_state_diagram.gif)

# volley
## POST image file
[stackoverflow](http://stackoverflow.com/questions/29430599/upload-an-image-using-google-volley)

# HttpURLConnection
## POST image file
[Android HttpURLConnection 上傳檔案 (multipart/form-data)](http://blog.kenyang.net/2011/12/android-httpurlconnection-multipartform.html)

# AsyncTask
```java
class MyAsyncTask extends AsyncTask<String, Integer, Boolean> {
    /**
     * Creates a new asynchronous task. This constructor must be invoked on the UI thread.
     */
    public MyAsyncTask() {
        super();
    }


    /**
     * Runs on the UI thread before {@link #doInBackground}.
     *
     * @see #onPostExecute
     * @see #doInBackground
     */
    @Override
    protected void onPreExecute() {
        super.onPreExecute();
        Log.i("henry", "onPreExecute");

    }

    /**
     * Override this method to perform a computation on a background thread. The
     * specified parameters are the parameters passed to {@link #execute}
     * by the caller of this task.
     * <p/>
     * This method can call {@link #publishProgress} to publish updates
     * on the UI thread.
     *
     * @param names The parameters of the task.
     * @return A result, defined by the subclass of this task.
     * @see #onPreExecute()
     * @see #onPostExecute
     * @see #publishProgress
     */
    @Override
    protected Boolean doInBackground(String... names) {

        for (String name:names){
            intCounter++;
            Log.i("henry", "doInBackground");

            publishProgress(intCounter,intCounter*10,intCounter*100);

            if (isCancelled()) return false;

            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
        return true;
    }

    /**
     * Runs on the UI thread after {@link #publishProgress} is invoked.
     * The specified values are the values passed to {@link #publishProgress}.
     *
     * @param values The values indicating progress.
     * @see #publishProgress
     * @see #doInBackground
     */
    @Override
    protected void onProgressUpdate(Integer... values) {
        super.onProgressUpdate(values);
        Log.i("henry", "onProgressUpdate");
        tv1.setText("OK"+values[0]);
        tv2.setText("OK"+values[1]);
        tv3.setText("OK"+values[2]);


    }

    /**
     * <p>Runs on the UI thread after {@link #doInBackground}. The
     * specified result is the value returned by {@link #doInBackground}.</p>
     * <p/>
     * <p>This method won't be invoked if the task was cancelled.</p>
     *
     * @param aVoid The result of the operation computed by {@link #doInBackground}.
     * @see #onPreExecute
     * @see #doInBackground
     * @see #onCancelled(Object)
     */
    @Override
    protected void onPostExecute(Boolean aVoid) {
        super.onPostExecute(aVoid);
        Log.i("henry", "onPostExecute");
        tv4.setText(aVoid?"Finished":"Cancelled");

    }



    /**
     * <p>Runs on the UI thread after {@link #cancel(boolean)} is invoked and
     * {@link #doInBackground(Object[])} has finished.</p>
     * <p/>
     * <p>The default implementation simply invokes {@link #onCancelled()} and
     * ignores the result. If you write your own implementation, do not call
     * <code>super.onCancelled(result)</code>.</p>
     *
     * @param aVoid The result, if any, computed in
     *              {@link #doInBackground(Object[])}, can be null
     * @see #cancel(boolean)
     * @see #isCancelled()
     */
    @Override
    protected void onCancelled(Boolean aVoid) {
        super.onCancelled(aVoid);
        Log.i("henry", "onCancelled");
        tv4.setText(aVoid?"Finished":"Cancelled");
    }

    /**
     * <p>Applications should preferably override {@link #onCancelled(Object)}.
     * This method is invoked by the default implementation of
     * {@link #onCancelled(Object)}.</p>
     * <p/>
     * <p>Runs on the UI thread after {@link #cancel(boolean)} is invoked and
     * {@link #doInBackground(Object[])} has finished.</p>
     *
     * @see #onCancelled(Object)
     * @see #cancel(boolean)
     * @see #isCancelled()
     */
    @Override
    protected void onCancelled() {
        super.onCancelled();
        Log.i("henry", "onCancelled2");

    }


}
```

```java
task = new MyAsyncTask();
task.execute("test1",
             "test2",
             "test2",
             "test2",
             "test2",
             "test2",
             "test2",
             "test3");
```

# 上架App
[Google Play Developer Console](https://play.google.com/apps/publish/)
export signed package
keystore







# Providing Resource
[official](http://developer.android.com/intl/zh-cn/guide/topics/resources/providing-resources.html)
`res/layout-land`當device拿橫時，就會套用到此版面
`res/values-zh-rTW`當語系改為中文台灣時，就會套用此values設定

# Notification
[official](http://developer.android.com/intl/zh-cn/guide/topics/ui/notifiers/notifications.html)

```java
        mgr = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);

        // instantiate PendingIntent
        TaskStackBuilder taskStackBuilder = TaskStackBuilder.create(this);
        taskStackBuilder.addParentStack(NoticePageActivity.class);
        taskStackBuilder.addNextIntent(new Intent(this,NoticePageActivity.class));
        PendingIntent pendingIntent = taskStackBuilder.getPendingIntent(124,PendingIntent.FLAG_UPDATE_CURRENT);

        // instantiate Notification.Builder
        Notification.Builder builder = new Notification.Builder(this);
        builder.setTicker("super important");
        builder.setAutoCancel(true);
        builder.setSmallIcon(android.R.drawable.sym_def_app_icon);
        builder.setLargeIcon(BitmapFactory.decodeResource(getResources(), android.R.drawable.sym_def_app_icon));
        builder.setSound(Uri.fromFile(new File(Environment.getExternalStorageDirectory(),"sound.wav")));
        builder.setContentInfo("info");
        builder.setContentText("text");
        builder.setContentTitle("title");
        builder.setContentIntent(pendingIntent);


        // API Level 11+
        //Notification notification = builder.getNotification();

        // API Level 16+ (4.1.2+)
        Notification notification = builder.build();
        // send notification
        mgr.notify(0,notification);

```




# java
- garbage collection
> 物件沒有被reference時，`System.gc();`會要求系統做gc，但若系統沒空，還是要等到它有空才會做。

# convetion
[Official Code Style Guidelines for Contributors](http://source.android.com/source/code-style.html)

> lint
在計算機科學中，lint是一種工具程序的名稱，它用來標記源代碼中，某些可疑的、不具結構性的段落。它是一種靜態程序分析工具，最早適用於C語言，在UNIX平台上開發出來。後來它成為通用術語，可用於描述在任何一種電腦編程語言中，用來標記源代碼中有疑義段落的工具。


# Question
- Content Provider的使用時機
- Fragment的使用時機
- FrameLayout的使用時機

- Service的動作是否都能做在Activity
跟UI無關的動作都放在Service

- 啥是Context
Activity/Service..等類別

- QA
  1. coding完用JUnit單元測試，[參考](http://140.127.82.166/retrieve/18991/91.pdf)
  2. brad客製化QA測試工具做整體測試

- 公司VersionControlSystem, gitignore
> 內部git, vpn

- API https


- 程式架構文件-> PGM: Phase Gate Model
  1. 流程圖 -> brad
  2. 演算法 -> all
  3. coding -> member
  4. code review -> all


# Java

[brad@brad.tw](mailto://brad@brad.tw)

**Apache Cordova** is a platform for building native mobile applications using HTML, CSS and JavaScript
[官網](https://cordova.apache.org/)

```java
  byte b; // [a-zA-Z$_][a-zA-Z0-9$_]
  byte 成績=127; //8個位元組，-127~127，常用在圖形及網路streaming
  System.out.println(成績);
```

Instances of `StringBuilder` are not safe for use by multiple threads. If such synchronization is required then it is recommended that `StringBuffer` be used.

**FileInputStream**:  一次讀取一個byte，適用於讀取影片、圖片…等檔案
**FileReader**: 一次讀取一個character，適用於讀取文件
**BufferReader**: 一次讀取一行`readline()`，適用於讀取文件，需串接`InputStreamReader`，再由`InputStreamReader`串接`FileInputStream`
**FileOutputStream**:
- 最後要close前，要強制將buffer裡的資料寫入disk---->`flush()`

DataInputStream: 可存基本型態(primitive Java data types)
ObjectInputStream: 可存Object，前提是此Object需`implements Serializable`，另可再此Object屬性加上`transient`表示此屬性不可序列化




存取權

- public: 全世界
- protected:
	- 同package
	- 子類別
- 沒寫: 同package
- private: 本類別

## java.net
> InetAddress
UDP:
- fast
- unreliable
- socket: 接口, `DatagramSocket`
- packet: 封包, `DatagramPacket`

```java
  //sender
  byte[] buf = "hello, I'm Henry".getBytes();
  DatagramSocket socket = new DatagramSocket();
  DatagramPacket packet = new DatagramPacket(buf, buf.length, InetAddress.getByName("10.2.24.156"), 9999);
  socket.send(packet);
  socket.close();
```

```java
  //reciever
  byte[] buf = new byte[4096];
  DatagramSocket socket = new DatagramSocket(8888);
  DatagramPacket packet = new DatagramPacket(buf, buf.length);
  socket.receive(packet);
  socket.close();
```

  TCP:
  server socket: `ServerSocket`
  client socket: `Socket`

```java
  // reciever
  ServerSocket server = new ServerSocket(8888);
  Socket socket = server.accept();
  InputStream is = socket.getInputStream();

  InputStreamReader isr = new InputStreamReader(is);
  int temp;
  while ( (temp = isr.read())!=-1)
  {
  	System.out.print((char)temp);
  }

  is.close();
  socket.close();
  server.close();
```

```java
  // sender
  Socket socket = new Socket(ip, 8888);
  OutputStream out = socket.getOutputStream();
  out.write("Hi, I'm Henry!!".getBytes());
  out.flush();
  out.close();
  socket.close();
```

## 執行緒Thread
  - 有生命週期之物件
  - 寫法一`extends Thread`

```java

  public class ThreadObject {

  	public static void main(String[] args) {
  		ServerThreads st1 = new ServerThreads("bella");
  		ServerThreads st2 = new ServerThreads("vivian");
  		st1.start();
  		st2.start();
  		System.out.println("penny");
  		try {
  			Thread.sleep(1000);
  		} catch (InterruptedException e) {
  			// TODO Auto-generated catch block
  			e.printStackTrace();
  		}
  		System.out.println("henry");
  	    // trigger InterruptedException例外
  		st1.interrupt();
  	}

  }

  class ServerThreads extends Thread{
  	private String name;
  	public ServerThreads(String s) {
  		name = s;
  	}

  	@Override
  	public void run() {
  		for (int i = 0; i < 20; i++) {
  			try {
  				Thread.sleep(200);
  			} catch (InterruptedException e) {
  			// trigger by st1.interrupt();
  			    break;
  			}
  			System.out.println(name+":"+i);
  		}
  	}
  }
```
  
- 寫法二`implements Runnable`

```java

  public class ThreadObject {

  	public static void main(String[] args) {

  		ServerRunnable sr1 = new ServerRunnable("bella");
  		Thread t1 = new Thread(sr1);
  		t1.start();
  	}

  }
  class ServerRunnable implements Runnable{
  	private String name;
  	public ServerRunnable(String s) {
  		name = s;
  	}

  	@Override
  	public void run() {
  		for (int i = 0; i < 20; i++) {
  			try {
  				Thread.sleep(200);
  			} catch (InterruptedException e) {
  			}
  			System.out.println(name+":"+i);
  		}
  	}
  }
```

## Collection

- [what is the sense of final ArrayList?](https://www.evernote.com/shard/s75/sh/29c4aebe-c386-4275-a320-94fa28e3b32f/5552b7359ba91b9e8a00e0989df94d62)
- [HashMap with multiple values under the same key](https://www.evernote.com/shard/s75/sh/f6f4a967-57d5-4139-82c2-6120f1dc4df8/523b027d19c67ec23c6afd48f63c9b72)

## IO

- [Java 7 新的 try-with-resources 语句，自动资源释放](https://www.evernote.com/shard/s75/sh/95db27f4-be6d-4e21-ab5c-8e6e50f45aa2/d778d182765dc1ef92b79988df04fe79)


## Database

- PreparedStatement與Statement最大的差異在於SQL已預載入，因此執行時僅需bind variable即可，所以SQL是bind不同var頻繁執行時，使用PS會比較有效率；但若是不重覆執行頻繁更換SQL的用法時，效能基本上就跟S差不多。

## Annotation

- 將metadata, data, methods都放在程式裡, 易於分析/解讀.

## CDI

- 當沒有@ApplicationScoped, 會報錯Unsatisfied dependencies for type xxxxx with qualifiers @Default

```bash
java.lang.IllegalStateException: ContainerBase.addChild: start: org.apache.catalina.LifecycleException: org.apache.catalina.LifecycleException: org.jboss.weld.exceptions.DeploymentException: WELD-001408: Unsatisfied dependencies for type CdiServerJava with qualifiers @Default
  at injection point [BackedAnnotatedField] @Inject private tw.henry.test.JaxRsService.server
  at tw.henry.test.JaxRsService.server(JaxRsService.java:0)
```
[參考](http://stackoverflow.com/questions/27706091/unsatisfied-dependencies-for-type-x-with-qualifiers-default)


- 當有兩個以上的@Default, 會報錯Ambiguous dependencies

```bash
org.jboss.weld.exceptions.DeploymentException: WELD-001409: Ambiguous dependencies for type CdiServerIF with qualifiers @Default
  at injection point [BackedAnnotatedField] @Inject private tw.henry.test.JaxRsService.server
  at tw.henry.test.JaxRsService.server(JaxRsService.java:0)
  Possible dependencies:
  - Managed Bean [class tw.henry.test.CdiServerJava] with qualifiers [@Any @Default],
  - Managed Bean [class tw.henry.test.CdiServerPhp] with qualifiers [@Any @Default]
```

- 管理物件生命週期, e.g. JDBC resource, client 無需開關
- 没有 Scope 注解的情况下，default scope 是@Dependent, 而@Dependent Scope 中的 Bean 的生命周期取决于被注入的 Bean 的生命周期