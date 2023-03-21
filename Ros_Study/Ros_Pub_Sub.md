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

```
# 운영체제에 설치된 cmake의 최소 요구 버전
cmake_minimum_required(VERSION 3.0.2)

# 패키지의 이름으로, package.xml에서 입력한 패키지 이름을 그대로 사용
project(test_pkg)

# 캐킨 빌드할 시 요구되는 구성 요소 패키지. 사용자가 만든 패키지가 의존하는 다른 패키지를 먼저 설치하는 옵션
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
)

# ROS 이외의 패키지를 사용하는 예: Boost를 사용할 때 system 패키지를 설치하도록 함
find_package(Boost REQUIRED COMPONENTS system)

# 파이썬을 이용하기 위해 rospy를 사용할 때 설정하는 옵션. 파이썬 설치 프로세스인 setup.py를 부르는 역할
catkin_python_setup()

# 메시지 파일을 추가
# FILES: 현재 패키지 폴더의 msg 폴더 안의 .msg 파일들을 참조해 헤더 파일(.h)를 자동으로 생성한다는 의미
# 만약 새 메시지를 만든다면 msg 폴더를 만든 뒤 그 안에 있는 메시지 파일 이름을 입력함. 여기에서는 MyMessage1.msg 등이 그 예.
add_message_files(
  FILES 
  MyMessage1.msg
  MyMessage2.msg
)

# 사용하는 서비스 파일을 추가. 방식은 메시지 파일과 같으며, 사용하려면 srv 폴더를 만든 뒤 해당 파일 이름을 입력해둬야 한다.
add_service_files(
  FILES
  MyService.srv
)

# 사용하는 서비스 파일을 추가. 방식은 메시지, 서비스 파일과 같다.
add_action_files(
  FILES
  Action1.action
  Action2.action
)

# 의존하는 메시지를 설정
# DEPENDENCIES: 아래에 해당하는 메시지 패키지를 사용한다는 의미
# std_msgs, sensor_msgs가 그 예시
generate_messages(
  std_msgs 
  sensor_msgs
)

# 캐킨 빌드 옵션
## INCLUDE: 뒤에 설정한 패키지 내부 폴더인 include의 헤더 파일을 사용함
## LIBRARIES: 뒤에 설정한 패키지의 라이브러리를 사용함
## CATKIN_DEPENDS: 의존하는 패키지 지정
## DEPENDS: 시스템 의존 패키지
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES test_pkg
#  CATKIN_DEPENDS roscpp rospy std_msgs
#  DEPENDS system_lib
)

# include 폴더 지정
include_directories(
  ${catkin_INCLUDE_DIRS} # 각 패키지 내의 include 폴더를 의미. 이 안의 헤더파일을 이용할 것. 
  # 사용자가 추가할 때는 이 밑의 공간 이용
)

# 빌드 후 생성할 라이브러리. C++을 사용할 경우!
add_library(${PROJECT_NAME}
  src/${PROJECT_NAME}/test_pkg.cpp
)

# 해당 라이브러리 및 실행파일을 빌드하기 전, 생성해야 할 의존성이 있는 메시지와 dynamic reconfigure이 있다면 우선으로 수행하도록 함
add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

# 빌드 후 생성할 실행파일에 대한 옵션 지정
## `__실행 파일 이름__` `__참조할 파일__` 순서대로 기재
## 복수 개의 참조 .cpp 파일이 있을 경우 한 괄호 뒤에 연속적으로 기재
## 생성할 실행파일이 2개 이상일 경우 add_executable 항목을 추가함
add_executable(${PROJECT_NAME}_node src/test_pkg_node.cpp)

# 지정 실행 파일을 생성하기 전, 링크해야 하는 라이브러리와 실행파일을 링크함
target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
)
```

4. 메시지 파일 작성
새로운 메시지 파일(.msg)를 만들고 이를 사용해 노드를 이용한 통신을 한다. 
- 패키지 폴더 내 msg폴더(~/test_pkg/msg) 생성
- 텍스트 편집기 혹은 VS Code 등을 열어 아래 내용 입력

```
time stamp
int32 data
```

- msg 폴더에 메시지 파일 `test_msg.msg`로 저장, 확장자 .msg까지 입력

```
❗️ 메시지 타입의 대표적 예
메시지 기본 타입: time, int32, bool, int8, int16, float32, string, duration 등
ROS 사용 빈도 많은 메시지를 모아둔 타입: common_msgs 등
```

5. 소스 코드 작성
토픽을 송신하는 Publisher(퍼블리셔)노드와 토픽을 수신하는 Subscribe(서브스크라이브)노드를 각각 만든다.

python으로 제어를 할 예정으로 