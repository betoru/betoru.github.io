---
layout: post
date: 2020-05-07 13:25:00 +0900
title: 'Android: Kotlin Splash'
category:
  - Kotlin
tags:
  - Kotlin
  - android
  - splash
img: kotlin.png # Add image post (optional)  
---

## Splash
> App 을 실행하여 처음 보여주는 인트로 화면, 주로 데이터를 로드하는 시간동안 노출하며 앱 버전, 업데이트 여부 등을 체크하는 동안 노출한다.


#### AndroidManifest.xml
splash는 앱 실행시 노출되므로 adroidmanifest 의 LAUNCHER를 설정해준다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.first.eplatztesttmpl">
    <uses-permission android:name="android.permission.INTERNET" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:debuggable="true"
        android:theme="@style/AppTheme"
        tools:ignore="HardcodedDebugMode">
        <activity android:name=".CalendarViewActivity"></activity>
        <!-- Splash Activity -->
        <activity
            android:name=".SplashActivity"
            android:theme="@style/SplashTheme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity> <!-- Splash Activity -->
        <activity
            android:name=".MainActivity"
            android:theme="@style/AppTheme.NoActionBar" />
    </application>

</manifest>
```

#### SplashActivity.kt
스플래시 코틀린 클래스 : 앱이 실행되면 코틀린 클래스가 실행되며, 딜레이 시간을 설정하여 끝났을 때 MainActivity가 실행되도록 한다.

```javascript
class SplashActivity : AppCompatActivity() {

    val SPLASH_VIEW_TIME : Long = 3000 // 3초간 스플래시 화면 노출(ms)

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        //setting start activity after delay
        Handler().postDelayed({
            startActivity(Intent(this,MainActivity::class.java))
        },SPLASH_VIEW_TIME)

        setContentView(R.layout.activity_main)
    }
}
```
