# JoyStickView 코드 분석

1. 페이지 세팅

```
<com.zerokol.views.joystickView.JoystickView
    android:id="@+id/joystickView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```

위 부분을 activity_main에 추가하였다. 이 부분은 JoystickView에 있는 JoyStickView를 표현하는 부분을 들고 온 것이다.

## initJoystickView (색깔 지정 및 스타일 지정)



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

### 색 지정

Color.RED, Color.WHITE, Color.GREEN, Color.BLACK

으로 적혀져 있던 색 지정을 원하는 색으로 변경하고자 하였다. 먼저 바꾸고 싶은 부분의 색을 어떤색으로 바꿀 것인지 찾았다.

#EB455F, #2B3467, #BAD7E9 으로 3가지 색상으로 변경을 시도하였다.

Android Studio에서는 색상을 지정할 때 Color.rgb(int red, int green, int blue)를 사용하여 원하는 색상으로 변경할 수 있다는 것을 확인하고 Hex코드를 Int로 변환하여 색상을 변경하였다.


    Color.rgb(186, 215, 233)
    Color.rgb(235, 69, 95)
    Color.rgb(43, 52, 103)


다음의 코드를 사용하여 색상을 변경하였다.


### 스타일 지정

    mainCircle.setStyle(Paint.Style.FILL_AND_STROKE);
    secondaryCircle.setStyle(Paint.Style.STROKE);

setStyle()로 스타일을 지정한다.
Paint.Style.FILL_AND_STROKE : 채우기와 테두리 모두를 그리도록 하는 것이다.

Paint.Style.STROKE : 채우기 없이 테두리만 그린다.

Paint.Style.FILL : 색상이 채워지고 테두리는 그리지 않는다.

### 테두리 두께

    verticalLine.setStrokeWidth(5);
    horizontalLine.setStrokeWidth(2);
    secondaryCircle.setStrokeWidth(4);

setStrokeWidth(float width) 로 Paint의 굵기를 설정한다.

### ANTI_ALIAS_FLAG

앤티앨리어싱을 활성화하는 페인트 플래그이다. 앤티앨리어싱은 네모난 픽셀로 이로어진 곡선, 원형 등의 이미지가 매끄럽지 못하게 보이는 것을 부드럽게 만들어 준다.

![Screenshot from 2023-03-14 21-48-37](https://user-images.githubusercontent.com/90883561/225013996-aeaffacd-59f8-4cb0-913d-191c063e7e20.png)


## onDraw (화면에 그리기)



    protected void onDraw(Canvas canvas) {
        // super.onDraw(canvas);
        centerX = (getWidth()) / 2;
        centerY = (getHeight()) / 2;

        // painting the main circle
        canvas.drawCircle((int) centerX, (int) centerY, joystickRadius,
                mainCircle);
        // painting the secondary circle
        canvas.drawCircle((int) centerX, (int) centerY, joystickRadius / 2,
                secondaryCircle);
        // paint lines
        canvas.drawLine((float) centerX, (float) centerY, (float) centerX,
                (float) (centerY - joystickRadius), verticalLine);
        canvas.drawLine((float) (centerX - joystickRadius), (float) centerY,
                (float) (centerX + joystickRadius), (float) centerY,
                horizontalLine);
        canvas.drawLine((float) centerX, (float) (centerY + joystickRadius),
                (float) centerX, (float) centerY, horizontalLine);

        // painting the move button
        canvas.drawCircle(xPosition, yPosition, buttonRadius, button);
    }

### 1. canvas에서 가로와 세로를 구한 후 X, Y의 중앙 지점을 잡는다.
### 2. initJoystickView에서 지정해놓은 Paint를 이용하여 화면을 그린다.

canvas.drawCircle((int) centerX, (int) centerY, joystickRadius, mainCircle);

canvas에 원을 그린다는 의미로 중심 좌표 x, y와 반지름을 넣고, Paint정보를 넣는다.

canvas.drawLine((float) centerX, (float) centerY, (float) centerX, (float) (centerY - joystickRadius), verticalLine);

Line을 그리는 것은 시작점과 끝점, Paint정보를 작성하면 된다.

![Screenshot from 2023-03-14 21-33-32](https://user-images.githubusercontent.com/90883561/225013865-d5e2277b-734d-4c27-a1c9-ad78fdde30e1.png)
