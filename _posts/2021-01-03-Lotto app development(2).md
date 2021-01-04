---
layout: post
title: "Lotto app development(2)"
subtitle: "2021-01-03(별자리 검색)"
background: "/img/posts/02.jpg"
date: 2021-01-03 16:12:00 +0900
categories: ["development"]
---

![2021-01-03(1)](https://user-images.githubusercontent.com/76092057/103477354-79c7c080-4e01-11eb-8fc2-3a35b1ae1144.PNG){: width:"100%" height:"100%"}

1. DatePicker를 이용하여 날짜를 선택할 수 있게 하게 하고,
   그에 맞게 별자리가 나오도록 수정할 예정!<br>

***

완성된 레이아웃 XML 코드
=======================

```java
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".ConstellationActivity">

    <Button
        android:id="@+id/goResultButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        android:layout_margin="16dp"
        android:layout_marginBottom="555dp"
        android:text="로또번호확인"
        app:layout_constraintBottom_toBottomOf="parent"
        tools:layout_editor_absoluteX="16dp" />

    <DatePicker
        android:id="@+id/datePicker"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:calendarViewShown="false"
        android:datePickerMode="spinner"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="120dp"
        android:layout_height="match_parent"
        android:layout_above="@+id/goResultButton"
        android:layout_below="@+id/datePicker"
        android:layout_margin="16dp"
        android:src="@drawable/constellation"/>

    <androidx.appcompat.widget.AppCompatTextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignBottom="@+id/imageView"
        android:layout_alignTop="@+id/imageView"
        android:layout_marginLeft="16dp"
        android:layout_marginRight="32dp"
        android:layout_toRightOf="@+id/imageView"
        android:gravity="center"
        android:maxLines="1"
        android:text="쌍둥이자리"
        android:textColor="@android:color/black"
        app:autoSizeMaxTextSize="48sp"
        app:autoSizeMinTextSize="24sp"
        app:autoSizeStepGranularity="1sp"
        app:autoSizeTextType="uniform"/>

</RelativeLayout>
```