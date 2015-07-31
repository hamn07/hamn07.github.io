title: android note
date: 2015-07-30 09:17:19
tags:
---
![](http://developer.android.com/intl/zh-cn/images/activity_lifecycle.png)
***
![](http://developer.android.com/images/service_lifecycle.png )
[趙老師的雲端分享資料夾](https://drive.google.com/folderview?id=0B5zn2b2xqOwGfm5yYVd2emZrcnN6YTBvbDhpQTY1OGdxSExFWGczMlFzZV9sMFdGUS1UeTg&usp=sharing#list)
<!-- toc -->
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
# volley
## POST image file
[stackoverflow](http://stackoverflow.com/questions/29430599/upload-an-image-using-google-volley)

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

# Question
- Service的動作是否都能做在Activity
- 啥是Context
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
