# Ros Publish and Subscribe

1. 패키지 생성
가장 먼저 패키지를 생성한다.
터미널을 열고
```
/catkin_ws/src
``` 
로 이동하고 명령어를 입력한다. catkin_create_pkg [패키지 이름] [의존성 패키지]

```
catkin_create_pkg test_pkg std_msgs rospy roscpp
```

- 의존성 패키지 해당 패키지에서 사용할 의존성 기술
    - std_msgs --> 주고 받을 메시지 타입 위함
    - rospy --> python 사용
    - roscpp --> C++ 사용
- 의존성 패키지는 동시에 여러개 선언 할 수 있으며 package.xml에서 추가/ 변경할 수 있다.
- 사용자가 위와 같이 패키지 작성 시 catkin build system에서 필요한 CMakeList.txt, package.xml 폴더를 생성한다.
- 패키지 이름에는 공백 있으면 안된다. 소문자를 사용하고, 언더바(_)를 사용해 단어를 붙인다.

해당 명령 직후 ~/catkin_ws/src/ 패키지명 폴더 내에 생성되는 파일 및 폴더는 아래와 같다. 추후 사용자의 필요에 따라 /launch, /msg 등의 폴더를 추가적으로 생성할 수 있다.

|폴더, 파일|설명|
|-----------|---------|
|/include|헤더 파일|
|/src|코드 소스 파일|
|CMakeList.txt|빌드 설정 파일|
|package.xml|패키지 설정 파일|