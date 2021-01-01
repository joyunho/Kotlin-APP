---
layout: post
title: "Lotto app development(1)"
subtitle: "2021-01-01(Main Activity Category)"
date: 2021-01-01 21:12:00 +0900
background: "/img/posts/01.jpg"
categories: ["development"]
---

![2021-01-01(1)](https://user-images.githubusercontent.com/76092057/103438837-f0868180-4c7a-11eb-89e6-89b571f2f572.PNG){: width:"100%" height:"100%"}

1. LottoApp을 실행시켰을 때 4가지 버튼이 보이도록 설계
==> "MAIN ACTIVITY" // CONSTELLATION ACTIVITY // NAME ACTIVITY //
RESULT ACTIVITY

![2021-01-01(3)](https://user-images.githubusercontent.com/76092057/103438902-92a66980-4c7b-11eb-86ce-368490e89f7e.PNG){: width:"100%" height:"100%"}

2. 각각의 버튼을 눌렀을 때, 화면이 전환되는 것을 알려주기 위해 각 버튼의 이름
이 화면이 전환되었을 떄 보이도록 설계

![2021-01-01(2)](https://user-images.githubusercontent.com/76092057/103438943-ec0e9880-4c7b-11eb-8326-b2f3b6b0d2e5.PNG){: width:"100%" height:"100%"}

3. 먼저 MAIN ACTIVITY 버튼을 눌렀을 때 View를 만들기로 했다. 목차로는
"랜덤으로 번호 생성" // "별자리로 번호 생성" // "이름으로 번호 생성" 이 있다.
또한 'clickable' 속성을 이용하여 Click 이벤트를 설계<br>

***
<br>

완성된 레이아웃 XML 코드
=======================

{% raw %}
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:weightSum="3"
    android:id="@+id/linearLayout">

    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        app:cardCornerRadius="8dp"
        app:cardUseCompatPadding="true">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="?attr/selectableItemBackground"
            android:clickable="true"
            android:foreground="?attr/selectableItemBackground"
            android:gravity="right|center_vertical"
            android:orientation="horizontal">

            <LinearLayout
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:gravity="center"
                android:orientation="vertical">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="랜덤으로 번호 생성"
                    android:textSize="24sp" />

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="8dp"
                    android:text="랜덤으로 로또번호를 생성합니다" />
            </LinearLayout>

            <ImageView
                android:layout_width="140dp"
                android:layout_height="140dp"
                app:srcCompat="@drawable/lottery" />

        </LinearLayout>
    </androidx.cardview.widget.CardView>

    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_marginTop="2dp"
        android:layout_weight="1" >

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:gravity="right|center_vertical"
            android:orientation="horizontal">

            <LinearLayout
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:gravity="center"
                android:orientation="vertical">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="별자리로 번호 생성"
                    android:textSize="24sp" />

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="8dp"
                    android:text="별자리로 로또번호를 생성합니다" />
            </LinearLayout>

            <ImageView
                android:layout_width="140dp"
                android:layout_height="140dp"
                android:padding="16dp"
                android:paddingLeft="16dp"
                android:paddingTop="16dp"
                android:paddingRight="16dp"
                android:paddingBottom="16dp"
                app:srcCompat="@drawable/constellation" />

        </LinearLayout>
    </androidx.cardview.widget.CardView>

    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_marginTop="2dp"
        android:layout_weight="1" >

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:gravity="right|center_vertical"
            android:orientation="horizontal">

            <LinearLayout
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:gravity="center"
                android:orientation="vertical">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="이름으로 번호 생성"
                    android:textSize="24sp" />

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="8dp"
                    android:text="이름으로 로또번호를 생성합니다" />
            </LinearLayout>

            <ImageView
                android:layout_width="140dp"
                android:layout_height="140dp"
                android:padding="16dp"
                android:paddingLeft="16dp"
                android:paddingTop="16dp"
                android:paddingRight="16dp"
                android:paddingBottom="16dp"
                app:srcCompat="@drawable/name" />

        </LinearLayout>
    </androidx.cardview.widget.CardView>

</LinearLayout>
```
{% endraw %}