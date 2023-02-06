# Make App

# 목차
1. [실행단축키](#실행-단축키)
2. [위젯넣기](#위젯-넣기)
3. [동작부여](#동작-부여)

# 실행 단축키

앱 실행 : 

+ Shift + F10

을 누르면 바로 앱이 실행되는 것을 볼 수 있다.

주석 처리 : 

+ Ctrl + /

그래그 한 후 위 키를 누르면 그래그되어 있는 부분들이 주석처리 되는 것을 볼 수 있다.



# 위젯 넣기
![Untitled (1)](https://user-images.githubusercontent.com/90883561/216999477-0fac3319-0d68-4baf-a5cd-b658c7736a8b.png)

왼쪽에서 원하는 위젯을 끌어다가 올려놓는다. 처음 올려놓게 되면 실행시켰을 때 화면상에 보이는 위치와 달리 왼쪽상단에 나타나기 때문에 위치 지정을 해주어야 한다. 

위치지정은 Layout에서도 가능하고 직접 마우스로 끌어 놓으면서도 가능하다.

화면을 기준으로 위치를 지정할 수도 있지만 다른 위젯을 기준으로 위치를 지정하는 것도 가능하다.

오른쪽에 있는 부분에 있는 것들을 변경하면 xml파일에 자동으로 필요한 코드가 추가되고 삭제된다. 따라서 필요한 것이 있다면 이부분을 변경하면 된다. 폰트 크기와 텍스트를 변경할수도 있다.

![Untitled](https://user-images.githubusercontent.com/90883561/216999433-4c1b0153-585d-4371-97f2-c8553e27e0d7.png)

![Untitled (2)](https://user-images.githubusercontent.com/90883561/216999500-c9d3fcde-c2a2-40c2-bce9-432afc733cd0.png)


# 동작 부여


![Untitled (3)](https://user-images.githubusercontent.com/90883561/216999525-4af263ca-a4e1-4e0f-9ffa-f889e69629c3.png)


xml파일과 연동 된다.

    setContentView(R.layout.activity_main)

이라고 적으면 이는 activity_main.xml파일을 화면에 나타낸다는 것이다.

변경하지 않을 상수는

    val

로 작성하고, 변경할 변수는 

    var

로 작성한다.

    val tv: TextView = findViewById(R.id.tv_hello)

이 코드의 의미는 상수로 tv를 만드는데 TextView 객체로 만들것이며 findViewById 'tv_hello' id를 가지고 있는 TextView를 저장할 것이라는 의미이다.

따라서 위젯에서 저장하고 있는 id의 이름을 알아보기 쉬운 이름으로 누구나 보고 이해할 수 있는 이름으로 저장해놓고 변경해놓아야한다.

    btn.setOnClickListener {}

은 btn이 클릭되었을 때 {}안에 있는 코드를 실행한다는 의미이다.

현재 보이는 코드에서는 tv의 text를 '안녕'으로 변경하고 있는 것을 볼 수 있다.