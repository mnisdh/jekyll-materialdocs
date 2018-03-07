---
layout: post
title:  "Android Permission"
date:   2017-03-01 09:00:00 +0800
categories: Android
tags: Android Permission
---
### [모든 Permission 종류](https://developer.android.com/reference/android/Manifest.permission.html)
- 안드로이드 기능을 사용시 권한을 획득하여야만 사용할 수 있다
- 설치시만 체크하는 권한과 런타임시에도 체크해야하는 권한이 있있다

```
ACCESS_FINE_LOCATION            위치정보 확인함
ACCESS_MOCK_LOCATION            위치정보 확인함
ACCESS_NETWORK_STATE            네트웍이 연결된것을 확인할수 있게함
INTERNET                        인터넷을 사용함
WRITE_EXTERNAL_STORAGE          외장메모리 사용
CALL_PHONE                     	통화                              
CALL_PRIVILEGED                	통화(긴급전화_포함)               
CAMERA                         	카메라                            
CHANGE_COMPONENT_ENABLED_STATE 	컴포넌트의_실효성_변경            
CHANGE_CONFIGURATION           	컨피그_변경                       
CHANGE_NETWORK_STATE           	통신상태_변경                     
CHANGE_WIFI_STATE              	WiFi상태_변경                     
CONTROL_LOCATION_UPDATES       	위치정보_갱신                     
INTERNET                       	인터넷                            
READ_CALENDAR                  	캘린더_읽어오기                   
READ_CONTACTS                  	주소록_읽어오기                   
RECEIVE_MMS                    	MMS수신                           
RECEIVE_SMS                    	SMS수신                           
SEND_SMS                       	SMS송신                           

SYSTEM_ALERT_WINDOW            	알림_윈도우                       
VIBRATE                        	진동                              
WAKE_LOCK                      	알람                              

WRITE_CALENDAR                 	캘린더_쓰기                       
WRITE_CONTACTS                 	주소록_쓰기                       
WRITE_GSERVICES                	G서비스_쓰기                      
WRITE_OWNER_DATA               	owner_data쓰기                    
WRITE_SETTINGS                 	설정_쓰기
WRITE_SMS                      	SMS쓰기
```


### 사용법

#### androidmanifest.xml

```java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="android.daehoshin.com.permission">

    <!-- 권한설정 -->
    <!-- 실행시간 권한 -->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <!-- 설치 권한 -->
    <uses-permission android:name="android.permission.INTERNET" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name=".BaseActivity"></activity>
    </application>

</manifest>
```


#### BaseActivity

```java
package android.daehoshin.com.permission;

import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Build;
import android.support.annotation.NonNull;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public abstract class BaseActivity extends AppCompatActivity {
    private static final int REQ_CODE = 99;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_base);

        // 앱 버전 체크
        if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) checkPermission();
        else init();
    }

    private void checkPermission(){
        // 1. 권한이 있는지 여부 확인
        if(checkSelfPermission(Manifest.permission.READ_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED
                && checkSelfPermission(Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED){
            // 2.1 요청할 권한을 정의
            String permission[] = {Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.WRITE_EXTERNAL_STORAGE};

            // 2.2 권한 요청
            requestPermissions(permission, REQ_CODE);
        }
        else{
            init();
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        // 3. 권한 승인 여부 체크
        switch (requestCode){
            case REQ_CODE:
                if(grantResults[0] == PackageManager.PERMISSION_GRANTED && grantResults[1] == PackageManager.PERMISSION_GRANTED){
                    init();
                }
                break;
        }
    }

    abstract void init();


}
```
