---
title: MiCode Note Android Studio 环境搭建
date: 2025-03-17 09:10:09
tags: Android
---

# Android Studio 下载安装
<iframe src="//player.bilibili.com/player.html?isOutside=true&aid=113375174459879&bvid=BVBV1YLXMYJEiJ&cid=26479496308&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
[Android Studio官网下载](https://developer.android.com/studio)
配置网络环境

# 下载Notes源代码
```bash
cd ~/Documents
mkdir project
cd project
git clone https://github.com/MiCode/Notes
```

# 创建Android项目
按图完成项目创建，并等待右下角项目创建进度完成。
![create](create.png)

```bash
cp -r ./Notes/src/net/micode/notes/* ./MiNote/app/src/main/java/net/micode/notes/
cp -r ./Notes/res/* ./MiNote/app/src/main/res/
```

# 修改Manifest.xml
![manifest](manifest.png)
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
 
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="com.android.launcher.permission.INSTALL_SHORTCUT" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.READ_CONTACTS" />
    <uses-permission android:name="android.permission.MANAGE_ACCOUNTS" />
    <uses-permission android:name="android.permission.AUTHENTICATE_ACCOUNTS" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
    <uses-permission android:name="android.permission.USE_CREDENTIALS" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
 
    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MiNote"
        tools:targetApi="31">
 
        <activity
            android:name=".ui.NotesListActivity"
            android:configChanges="keyboardHidden|orientation|screenSize"
            android:label="@string/app_name"
            android:launchMode="singleTop"
            android:theme="@style/NoteTheme"
            android:uiOptions="splitActionBarWhenNarrow"
            android:windowSoftInputMode="adjustPan"
            android:exported="true">
 
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
 
        <activity
            android:name=".ui.NoteEditActivity"
            android:configChanges="keyboardHidden|orientation|screenSize"
            android:launchMode="singleTop"
            android:theme="@style/NoteTheme"
            android:exported="true">
 
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="vnd.android.cursor.item/text_note" />
                <data android:mimeType="vnd.android.cursor.item/call_note" />
            </intent-filter>
 
            <intent-filter>
                <action android:name="android.intent.action.INSERT_OR_EDIT" />
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="vnd.android.cursor.item/text_note" />
                <data android:mimeType="vnd.android.cursor.item/call_note" />
            </intent-filter>
 
            <intent-filter>
                <action android:name="android.intent.action.SEARCH" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
 
            <meta-data
                android:name="android.app.searchable"
                android:resource="@xml/searchable" />
        </activity>
 
 
        <provider
            android:name="net.micode.notes.data.NotesProvider"
            android:authorities="micode_notes"
            android:multiprocess="true" />
 
        <receiver
            android:name=".widget.NoteWidgetProvider_2x"
            android:label="@string/app_widget2x2"
            android:exported="true">
            <intent-filter>
                <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
                <action android:name="android.appwidget.action.APPWIDGET_DELETED" />
                <action android:name="android.intent.action.PRIVACY_MODE_CHANGED" />
            </intent-filter>
 
            <meta-data
                android:name="android.appwidget.provider"
                android:resource="@xml/widget_2x_info" />
        </receiver>
        <receiver
            android:name=".widget.NoteWidgetProvider_4x"
            android:label="@string/app_widget4x4"
            android:exported="true">
 
            <intent-filter>
                <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
                <action android:name="android.appwidget.action.APPWIDGET_DELETED" />
                <action android:name="android.intent.action.PRIVACY_MODE_CHANGED" />
            </intent-filter>
 
            <meta-data
                android:name="android.appwidget.provider"
                android:resource="@xml/widget_4x_info" />
        </receiver>
 
        <receiver android:name=".ui.AlarmInitReceiver"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
            </intent-filter>
        </receiver>
 
        <receiver
            android:name="net.micode.notes.ui.AlarmReceiver"
            android:process=":remote" >
        </receiver>
 
        <activity
            android:name=".ui.AlarmAlertActivity"
            android:label="@string/app_name"
            android:launchMode="singleInstance"
            android:theme="@android:style/Theme.Holo.Wallpaper.NoTitleBar" >
        </activity>
 
        <activity
            android:name="net.micode.notes.ui.NotesPreferenceActivity"
            android:label="@string/preferences_title"
            android:launchMode="singleTop"
            android:theme="@android:style/Theme.Holo.Light" >
        </activity>
 
        <service
            android:name="net.micode.notes.gtask.remote.GTaskSyncService"
            android:exported="false" >
        </service>
 
        <meta-data
            android:name="android.app.default_searchable"
            android:value=".ui.NoteEditActivity" />
 
        <!--        <activity-->
        <!--            android:name=".MainActivity"-->
        <!--            android:exported="true">-->
        <!--            <intent-filter>-->
        <!--                <action android:name="android.intent.action.MAIN" />-->
 
        <!--                <category android:name="android.intent.category.LAUNCHER" />-->
        <!--            </intent-filter>-->
        <!--        </activity>-->
 
    </application>
 
</manifest>
```

# 下载依赖
```bash
cd ~/Documents/project/MiNote
wget https://dlcdn.apache.org//httpcomponents/httpclient/binary/httpcomponents-client-4.5.14-bin.zip
unzip httpcomponents-client-4.5.14-bin.zip -d app/libs
cd app/libs
rm -rf javadoc/ LICENSE.txt NOTICE.txt RELEASE_NOTES.txt
cp ./lib/* .
rm -rf lib
```

# 添加依赖
![gradle](gradle.png)
```gradle
    implementation(fileTree(mapOf(
        "dir" to "libs",
        "include" to listOf("*.aar", "*.jar"),
        "exclude" to emptyList<String>()
    )))
```
# 修改过时函数showNotification
![fun-replace](fun-replace.png)
```java
private void showNotification(int tickerId, String content) {
        PendingIntent pendingIntent;
        if (tickerId != R.string.ticker_success) {
            pendingIntent = PendingIntent.getActivity(mContext, 0, new Intent(mContext,
                    NotesPreferenceActivity.class), PendingIntent.FLAG_IMMUTABLE);
        } else {
            pendingIntent = PendingIntent.getActivity(mContext, 0, new Intent(mContext,
                    NotesListActivity.class), PendingIntent.FLAG_IMMUTABLE);
        }
        Notification.Builder builder = new Notification.Builder(mContext)
                .setAutoCancel(true)
                .setContentTitle(mContext.getString(R.string.app_name))
                .setContentText(content)
                .setContentIntent(pendingIntent)
                .setWhen(System.currentTimeMillis())
                .setOngoing(true);
        Notification notification=builder.getNotification();
        mNotifiManager.notify(GTASK_SYNC_NOTIFICATION_ID, notification);
    }
```

# 转换switch为if-else (共4处)
![switch-replace](switch-replace.png)

# 修改重复引入依赖
```gradle
    // implementation(fileTree(mapOf(
    //     "dir" to "libs",
    //     "include" to listOf("*.aar", "*.jar"),
    //     "exclude" to emptyList<String>()
    // )))
    implementation(files("libs/httpclient-osgi-4.5.14.jar"))
    implementation(files("libs/httpclient-win-4.5.14.jar"))
    implementation(files("libs/httpcore-4.4.16.jar"))
```

在build.gradle(Module:app)的android字段里面，加上这段代码，排除掉冲突的系统依赖包
```gradle
packaging {
        resources.excludes.add("META-INF/DEPENDENCIES");
        resources.excludes.add("META-INF/NOTICE");
        resources.excludes.add("META-INF/LICENSE");
        resources.excludes.add("META-INF/LICENSE.txt");
        resources.excludes.add("META-INF/NOTICE.txt");
    }
```
# 创建虚拟机
![avd](avd1.png)
![avd](avd2.png)
![avd](avd3.png)

# 运行成功
![result](result.png)