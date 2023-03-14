# JoyStick 사용

1. 모듈 등록

안드로이드 스튜디오에서 원하는 기능을 추가하기 위하여 직접 제작할 수도 있지만 프로젝트를 하나 모듈로 등록하여 모듈의 안에 있는 객체와 함수를 사용하는 방법을 선택하였다.


git에 JoystickView로 Joystick을 다루는 것을 찾았고 이를 사용하기 위해 다음 스탭을 따라 모듈을 등록하였다.

1. Download or Clone the library (using Git, or a zip archive to unzip)

'''
git clone https://github.com/alvesoaj/JoystickView.git
'''

2. Open project in Android Studio

3. Go to File -> New -> Import Module

4. Find and select JoystickView in project tree

5. Right-click app in project view and select "Open Module Settings"

6. Click the "Dependencies" tab and then the '+'button (Module Dependency)

7. Select "joystickView"

위 7가지 step을 진행하면 joystickView에 있는 객체와 함수를 사용할 수 있다. 
git clone 부분을 제외한 나머지 부분은 project를 하나의 모듈로 등록하는 부분이기에 만들어둔 project를 그대로 사용하고 싶을 때 같은 방법으로 모듈로 등록하여 사용하면 될 것으로 보인다.


'''
<com.zerokol.views.joystickView.JoystickView
        android:id="@+id/joystickView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
'''

git에 있는 설명에 따라 진행해보면 joystick의 화면과 작동을 확인할 수 있다.

조이스틱에 함수를 적절하게 사용하고 활용을 하기 위해 코드 분석을 진행하였다.