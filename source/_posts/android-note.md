title: android note
date: 2015-07-30 09:17:19
tags:
---
<!-- toc -->
# 上架App
[Google Play Developer Console](https://play.google.com/apps/publish/)
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

# Question
## Service的動作是否都能做在Activity
