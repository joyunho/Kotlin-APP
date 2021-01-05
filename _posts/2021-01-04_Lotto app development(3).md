---
layout: post
title: "Lotto app development(3)"
subtitle: "2021-01-04(이름 검색)"
background: "/img/posts/02.jpg"
date: 2021-01-04 17:03:00 +0900
categories: ["development"]
---

![2021-01-04(1)](https://user-images.githubusercontent.com/76092057/103513961-01b7d400-4eaf-11eb-93f6-d3ccc03bbfe2.PNG){: width:"100%" height:"100%"}

1. 이름으로도 로또 번호를 검색할 수 있게 하며, 테마의 색을 바꿈<br>

***

완성된 레이아웃 XML 코드
=======================

```java
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".NameActivity">

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_begin="20dp"
        app:layout_constraintGuide_percent="0.2" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_begin="20dp"
        app:layout_constraintGuide_percent="0.6" />

    <ImageView
        android:id="@+id/imageView2"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/guideline1"
        app:srcCompat="@drawable/name" />

    <EditText
        android:id="@+id/editText"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginLeft="32dp"
        android:layout_marginEnd="32dp"
        android:layout_marginRight="32dp"
        android:ems="10"
        android:hint="이름을 입력하세요"
        android:inputType="textPersonName"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/guideline2"
        app:layout_constraintVertical_bias="0" />

    <Button
        android:id="@+id/goButton"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginRight="8dp"
        android:text="번호생성"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/guideline3"
        app:layout_constraintStart_toStartOf="@+id/editText"
        app:layout_constraintTop_toBottomOf="@+id/editText"
        app:layout_constraintVertical_bias="0" />

    <Button
        android:id="@+id/backButton"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginRight="8dp"
        android:text="뒤로가기"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="@+id/editText"
        app:layout_constraintStart_toStartOf="@+id/guideline3"
        app:layout_constraintTop_toBottomOf="@+id/editText"
        app:layout_constraintVertical_bias="0" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_begin="20dp"
        app:layout_constraintGuide_percent="0.5" />

</androidx.constraintlayout.widget.ConstraintLayout>

<!-- 테마 변경 코드 -->
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#6200EE</color>
    <color name="colorPrimaryDark">#3700B3</color>
    <color name="colorAccent">#03DAC5</color>

    <!-- 결과화면에서 사용할 컬러 -->
    <color name="colorPrimaryResult">#2196F3</color>
    <color name="colorPrimaryDarkResult">#1976D2</color>
    <color name="colorAccentResult">#FF4081</color>

    <!-- 결과화면에서 사용할 컬러 -->
    <color name="colorPrimaryConstellation">#673AB7</color>
    <color name="colorPrimaryDarkConstellation">#1976D2</color>
    <color name="colorAccentConstellation">#7E57C2</color>
    <color name="colorContentConstellation">#556080</color>
    <color name="colorButtonConstellation">#673AB7</color>

    <!-- 이름 입력화면에서 사용할 컬러 -->
    <color name="colorPrimaryName">#F9A11F</color>
    <color name="colorPrimaryDarkname">#EF6C00</color>
    <color name="colorAccentName">#FFC107</color>
    <color name="colorContentName">#fcd837</color>
    <color name="colorButtonName">#F9A11F</color>

</resources>

<!-- 스타일 변경 코드 -->
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

    <!-- 결과화면 테마 -->
    <style name="AppTheme.Result" parent="AppTheme">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimaryResult</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDarkResult</item>
        <item name="colorAccent">@color/colorAccentResult</item>
    </style>

    <!-- 별자리 입력화면 테마 -->
    <style name="AppTheme.Constellation" parent="AppTheme">
        <item name="colorPrimary">@color/colorPrimaryConstellation</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDarkConstellation</item>
        <item name="colorAccent">@color/colorAccentConstellation</item>
        <!-- 버튼의 컬러 -->
        <item name="colorButtonNormal">@color/colorButtonConstellation</item>
        <!-- 버튼등 텍스트 컬러 -->
        <item name="android:textColor">@android:color/white</item>
    </style>

    <style name="AppTheme.Name" parent="AppTheme">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimaryName</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDarkname</item>
        <item name="colorAccent">@color/colorAccentName</item>
        <!-- 버튼의 컬러 -->
        <item name="colorButtonNormal">@color/colorButtonName</item>
        <!-- 버튼등 텍스트 컬러 -->
        <item name="android:textColor">@android:color/white</item>
    </style>

</resources>

<!-- mainfest 코드 -->
<!--
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>

                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
        -->
        <!-- AppTheme.Constellation 테마지정 -->
        <activity
            android:name=".ConstellationActivity"
            android:theme="@style/AppTheme.Constellation" />
        <!-- AppTheme.Name 테마지정 -->
        <activity
            android:name=".NameActivity"
            android:theme="@style/AppTheme.Name"/>
        <!-- AppTheme.Result 테마지정 -->
        <activity
            android:name=".ResultActivity"
            android:theme="@style/AppTheme.Result"/>
            
```
