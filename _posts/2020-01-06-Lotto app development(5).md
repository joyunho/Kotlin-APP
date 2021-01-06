---
layout: post
title: "Lotto app development(5)"
subtitle: "2021-01-05(난수 생성)"
background: "/img/posts/04.jpg"
date: 2021-01-06 23:26:00 +0900
categories: ["development"]
---

1. 난수를 생성하는 코드를 작성했으나... setImageResource 가 작동하지 않아 로또 그림이 바뀌지 않는 오류 발생
2. 해결하려했으나 오늘은 실패함... 오류는 안뜨는데 업데이트가 안되는 거라서 구글에 어떻게 검색해야할지 난해함...

> 내일 또한 이 오류를 수정하기 위해 고민해볼 것이다.<br>

***

완성된 레이아웃 XML 코드
=======================
```java
<!-- ResultActivity -->
class ResultActivity : AppCompatActivity() {

    //로또 1번 공 이미지의 아이디를 사용
    val lottoImageStartId = R.drawable.ball_01

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_result)

        // 전달받은 결과 배열을 가져온다
        val result = intent.getIntegerArrayListExtra("result")

        // 전달받은 결과가 있는 경우에만 실행
        result?.let{
            // 결과에 맞게 로또 공 이미지를 업데이트 한다.
            // 전달받은 결과는 정렬되어 있지않으므로 정렬해서 전달한다.
            updateLottoBallImage(result.sortedBy { it })
        }
    }

    // 결과에 따라 로또 공 이미지를 업데이트한다.
    fun updateLottoBallImage(result: List<Int>){
        // 결과 사이즈가 6개 미만인 경우 에러가 발생할 수 있으므로 바로 리턴한다.
        if(result.size < 6) return

        // ball_01 이미지 부터 순서대로 이미지 아이디가 있기 떄문에
        // ball_01 아이디에 결과값 -1을 하면 목표하는 이미지가 된다.
        // ex) result[0]이 2번 공인 경우 ball_01에서 하나 뒤에 이미지가 된다.
        imageView01.setImageResource(lottoImageStartId + (result[0] - 1))
        imageView02.setImageResource(lottoImageStartId + (result[1] - 1))
        imageView03.setImageResource(lottoImageStartId + (result[2] - 1))
        imageView04.setImageResource(lottoImageStartId + (result[3] - 1))
        imageView05.setImageResource(lottoImageStartId + (result[4] - 1))
        imageView06.setImageResource(lottoImageStartId + (result[5] - 1))
    }
}
```

***

```java
<!-- MainActivity -->
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // 랜덤으로 1 ~ 45 번호중 하나의 번호를 생성하는 함수
        fun getRandomLottoNumber(): Int{
            // Random.nextInt 는 0 ~ 전달받은 파라미터 값 미만의 번호르를 생성
            // ex) Random().nextInt(10)은 0 ~ 9 까지의 무작위 수를 반환
            // 1 ~ 45 까지의 번호를 생성하려면 파라미터의 45를 넣고 결과값의 1을 더한다.
            return Random.nextInt(45) + 1
        }

        // 랜덤으로 추출하여 6새의 로또 번호를 만드는 함수
        fun getRandomLottoNumbers(): MutableList<Int>{
            // 무작위로 생성된 로또 번호를 저장할 가변 리스트 생성
            val lottoNumbers = mutableListOf<Int>()

            // 6번 반복하는 for 문
            for(i in 1..6){
                // 리스트에 무작위로 생성된 번호를 추가한다.
                lottoNumbers.add(getRandomLottoNumber())
            }
            return lottoNumbers
        }

        // 랜덤으로 번호 생성 카드의 클릭 이벤트 리스너
        randomCard.setOnClickListener {
            // ResultAcitivity 를 시작하는 Intent를 만들고 startActivity 로 실행
            startActivity(Intent(this, ResultActivity::class.java))

            // ResultActivity 를 시작하는 Intent 생성
            val intent = Intent(this, ResultActivity::class.java)

            // intent 의 결과 데이터를 전달한다
            // int 의 리스트를 전달하므로 putIntegerArrayListExtra 를 사용한다.
            intent.putIntegerArrayListExtra("result", ArrayList(getRandomLottoNumber()))

            // ResultActivity 를 시작하는 Intent 를 만들고 startActivity로 실행
            startActivity(intent)
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