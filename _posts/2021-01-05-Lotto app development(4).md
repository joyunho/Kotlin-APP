---
layout: post
title: "Lotto app development(3)"
subtitle: "2021-01-05(이름 검색)"
background: "/img/posts/03.jpg"
date: 2021-01-01 17:03:00 +0900
categories: ["development"]
---

![2021-01-06(2)](https://user-images.githubusercontent.com/76092057/103663385-61e46e00-4fb4-11eb-8c06-acc2519002ef.PNG){: width:"100%" height:"100%"}

1. 결과 화면 창을 만듬

![2021-01-06(1)](https://user-images.githubusercontent.com/76092057/103663153-1f229600-4fb4-11eb-82e7-864782a60203.PNG){: width:"100%" height:"100%"}

2. MainActivity를 메인페이지로 바꾸고, setoOnClickListener를 사용하여 페이지가 넘어가도록 설정

![2021-01-06(2)](https://user-images.githubusercontent.com/76092057/103663385-61e46e00-4fb4-11eb-8c06-acc2519002ef.PNG){: width:"100%" height:"100%"}

3.  랜덤으로 번호생성을 눌렀을 때 열리는 화면

![2021-01-06(3)](https://user-images.githubusercontent.com/76092057/103663475-79bbf200-4fb4-11eb-98fd-e6831066c4e5.PNG){: width:"100%" height:"100%"}

4. 별자리로 번호생성을 눌렀을 때 열리는 화면

![2021-01-06(4)](https://user-images.githubusercontent.com/76092057/103663529-8a6c6800-4fb4-11eb-9af1-78e3dad9963f.PNG){: width:"100%" height:"100%"}

5. 이름으로 번호생성을 눌렀을 때 열리는 화면

> 내일은 난수 생성을 이용하여 로또 번호를 무작위로 나오게 만들 예정

오류사항
=======
1. 랜덤으로 번호 생성이 클릭만 되고 결과 화면창으로 넘어 가지 않음
2. 어느곳에서 문제가 생겼는지 나중에 확인해 볼 것!<br>

***

```java
    <androidx.cardview.widget.CardView
        android:id="@+id/randomCard"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        app:cardCornerRadius="8dp"
        android:clickable="false"
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
```

> 현재는 별다른 이상이 없는 별자리 번호생성을 복사하여 내용을 바꾸어서 수정함
<br>

***

완성된 레이아웃 XML 코드
=======================

```java
@ Activity_result.xml
<androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_begin="20dp"
        app:layout_constraintGuide_percent="0.3" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_begin="20dp"
        app:layout_constraintGuide_percent="0.5" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_begin="20dp"
        app:layout_constraintGuide_percent="0.08" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_begin="20dp"
        app:layout_constraintGuide_percent="0.92" />

    <view
        android:id="@+id/resultLabel"
        class="androidx.appcompat.widget.AppCompatTextView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="16dp"
        android:layout_marginLeft="16dp"
        android:layout_marginEnd="16dp"
        android:layout_marginRight="16dp"
        android:gravity="center"
        android:maxLines="3"
        android:text="홍길동님의\n로또번호입니다"
        android:textSize="60sp"
        app:autoSizeMaxTextSize="60sp"
        app:autoSizeMinTextSize="16sp"
        app:autoSizeStepGranularity="1sp"
        app:autoSizeTextType="uniform"
        app:layout_constraintBottom_toTopOf="@+id/guideline1"
        app:layout_constraintEnd_toStartOf="@+id/guideline4"
        app:layout_constraintStart_toStartOf="@+id/guideline3"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/imageView01"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintEnd_toStartOf="@+id/imageView02"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="@+id/guideline3"
        app:layout_constraintTop_toTopOf="@+id/guideline1"
        app:srcCompat="@drawable/ball_01" />

    <ImageView
        android:id="@+id/imageView02"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintEnd_toStartOf="@+id/imageView03"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/imageView01"
        app:layout_constraintTop_toTopOf="@+id/guideline1"
        app:srcCompat="@drawable/ball_07" />

    <ImageView
        android:id="@+id/imageView03"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintEnd_toStartOf="@+id/imageView04"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/imageView02"
        app:layout_constraintTop_toTopOf="@+id/guideline1"
        app:srcCompat="@drawable/ball_13" />

    <ImageView
        android:id="@+id/imageView04"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintEnd_toStartOf="@+id/imageView05"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/imageView03"
        app:layout_constraintTop_toTopOf="@+id/guideline1"
        app:srcCompat="@drawable/ball_22" />

    <ImageView
        android:id="@+id/imageView05"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintEnd_toStartOf="@+id/imageView06"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/imageView04"
        app:layout_constraintTop_toTopOf="@+id/guideline1"
        app:srcCompat="@drawable/ball_34" />

    <ImageView
        android:id="@+id/imageView06"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintEnd_toStartOf="@+id/guideline4"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/imageView05"
        app:layout_constraintTop_toTopOf="@+id/guideline1"
        app:srcCompat="@drawable/ball_43" />

    <ImageView
        android:id="@+id/imageView10"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/guideline4"
        app:layout_constraintStart_toStartOf="@+id/guideline3"
        app:layout_constraintTop_toTopOf="@+id/guideline2"
        app:srcCompat="@drawable/money" />
```
***

```java
@ Main Activity
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // 랜덤으로 번호 생성 카드의 클릭 이벤트 리스너
        randomCard.setOnClickListener {
            // ResultActivity 를 시작하는 Intent 를 만들고 startActivity 로 실행
            startActivity(Intent(this, ResultActivity::class.java))
        }

        // 별자리로 번호 생성 카드의 클릭 이벤트 리스너
        constellationCard.setOnClickListener {
            // ConstellationActivity 를 시작하는 Intent 를 만들고 startActivity 로 실행
            startActivity(Intent(this, ConstellationActivity::class.java))
        }

        // 이름으로 번호 생성 카드의 클릭 이벤트 리스너
        nameCard.setOnClickListener{
            // NameActivity 를 시작하는 Intent 를 만들고 startActivity 로 실행
            startActivity(Intent(this, NameActivity::class.java))
        }
    }
}
```

***

```java
@ Name Activity
goButton.setOnClickListener{
            // ResultActivity 를 시작하는 인텐트를 만들고 startActivity 로 실행
            startActivity(Intent(this, ResultActivity::class.java))
        }

        // 뒤로가기 버튼의 클릭이벤트 리스너 설정
        backButton.setOnClickListener({
            // 액티비티 종료
            finish()
        })
```

```java
@ Constellation Activity
 goResultButton.setOnClickListener{
            // ResultActivity를 시작하는 인텐트 만들고 startActivity 로 실행
            startActivity(Intent(this, ResultActivity::class.java))
        }
```