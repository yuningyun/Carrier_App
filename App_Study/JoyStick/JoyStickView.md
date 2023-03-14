# JoyStickView 코드 분석

1. 페이지 세팅

'''
<com.zerokol.views.joystickView.JoystickView
        android:id="@+id/joystickView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
'''

위 부분을 activity_main에 추가하였다. 이 부분은 JoystickView에 있는 JoyStickView를 표현하는 부분을 들고 온 것이다.

### initJoystickView (색깔 지정 및 스타일 지정)



    protected void initJoystickView() {
        mainCircle = new Paint(Paint.ANTI_ALIAS_FLAG);
        mainCircle.setColor(Color.WHITE);
        mainCircle.setStyle(Paint.Style.FILL_AND_STROKE);

        secondaryCircle = new Paint();
        secondaryCircle.setColor(Color.rgb(186, 215, 233));
        secondaryCircle.setStyle(Paint.Style.STROKE);
        secondaryCircle.setStrokeWidth(4);

        verticalLine = new Paint();
        verticalLine.setStrokeWidth(5);
        verticalLine.setColor(Color.rgb(235, 69, 95));

        horizontalLine = new Paint();
        horizontalLine.setStrokeWidth(2);
        horizontalLine.setColor(Color.BLACK);

        button = new Paint(Paint.ANTI_ALIAS_FLAG);
        button.setColor(Color.rgb(43, 52, 103));
        button.setStyle(Paint.Style.FILL);
    }


initJoystickView의 전제 코드.

1. 색 지정

Color.RED, Color.WHITE, Color.GREEN, Color.BLACK

으로 적혀져 있던 색 지정을 원하는 색으로 변경하고자 하였다. 먼저 바꾸고 싶은 부분의 색을 어떤색으로 바꿀 것인지 찾았다.

#EB455F, #2B3467, #BAD7E9 으로 3가지 색상으로 변경을 시도하였다.

Android Studio에서는 색상을 지정할 때 Color.rgb(int red, int green, int blue)를 사용하여 원하는 색상으로 변경할 수 있다는 것을 확인하고 Hex코드를 Int로 변환하여 색상을 변경하였다.


    Color.rgb(186, 215, 233)
    Color.rgb(235, 69, 95)
    Color.rgb(43, 52, 103)


다음의 코드를 사용하여 색상을 변경하였다.

