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


2. 패키지 설정 파일(package.xml) 수정

- 기본 구조
    - <?xml>: 문서 문법을 정의하는 문구. xml 버전을 나타냄
    - <package>: 해당 태그로 감싼 부분이 ROS 패키지 설정 부분임
- 패키지 정보
    - <name>: 패키지의 이름. 패키지 생성시 입력한 이름이 적용되며, 사용자의 임의 변경이 가능함
    - <version>: 패키지 버전으로, 자유로운 지정이 가능하다,
    - <description>: 패키지에 대한 설명으로, 2-3문장으로 입력한다.
    - <maintainer>: 패키지 관리자의 이름과 메일 주소(태그의 옵션 email을 이용)를 입력한다.
    - <license>: 라이선스를 기재한다.(e.g. GPL, BSD, ASL)
    - <url>: 패키지를 설명하는 웹페이지, 버그 관리, 저장소 등의 주소
    - <author>: 패키지 개발에 참여한 개발자의 이름과 이메일 주소를 적는다. 여러 명의 개발자의 경우 바로 다음줄에 해당 태그를 추가하며 입력한다.
- 의존 패키지(Dependency)
    - <buildtool_depend>: 빌드 시스템의 의존성이며, Catkin 빌드 시스템을 이용한다면 catkin을 입력한다.
    - <build_depend>: 패키지를 빌드할 때 의존하는 패키지 이름을 입력한다.
    - <run_depend>: 패키지를 실행할 때 의존하는 패키지 이름을 입력한다.
    - <test_depend>: 패키지를 테스트할 때 의존하는 패키지 이름을 입력한다.
- 메타패키지(Metapacakge)
    - <export>: ROS에서 명시하지 않은 태그명을 사용할 때 주로 쓰인다.
    - <metapackage>: export 태그 안에서 사용하는 공식적인 태그 중 하나로, 현재 패키지가 메타패키지일 경우 선언한다.


해당 내용을 맞게 바꾸어준다. 주석과 당장 필요 없는 부분을 지운다. 패키지 생성 당시 의존성으로 std_msgs, rospy, roscpp를 입력해주었으므로 자동적으로 <build_depend>, <build_export_depend>, <exec_depend>가 채워져 있다. 만약 패키지 생성 당시 명령어 옵션으로 추가하지 못했거나 추후 추가한다하면 해당 의존성 패키지를 이 파일에 입력해주면 된다.


3. 빌드 설정 파일(CMakeList.txt) 수정
`CMakeList.txt` 는 빌드 환경을 기술하고 있는 파일로, 실행 파일 생성과 의존성 패키지 우선 빌드, 링크 생성 등을 설정할 수 있다.


