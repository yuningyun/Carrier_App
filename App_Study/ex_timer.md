# Timer make

# 목차
1. [Timer 관련함수](#timer-관련-함수)
2. [변경되는 값 나타내기(UI다시그리기)](#변경되는-값-ui에-나타내기)
3. [NULL](#null)


# Timer 관련 함수

Timer는 ``` 
import java.util.* 
``` 에 들어있다.

```
timerTask = kotlin.concurrent.timer(period = 1000) {
    sec++
}
```

kotlin에 타이머를 실행하며 주기는 1000ms에 한번 sec의 값을 증가한다. 

타이머를 멈출 때는
    timerTask?.cancel()
을 사용하며 이때 '?'가 붙은 것을 null 때문이다. 이는 아래에서 더 자세히 다룰 예정이다.

# 변경되는 값 UI에 나타내기

```
runOnUiThread {

}
```

를 사용한다. 안에 들어있는 것들만 변경되었을 때 UI를 다시 그리며 나타내준다. 변경되는 값을 실시간으로 보기 위한 방법이다.

# null?

var timerTask: Timer? = null

로 처음 선언하였다. 이때 ?가 붙은 것은 null로 값이 없을 수도 있고 값이 있을 수도 있어서이다. 이 변수는 처음엔 null이었지만 나중에 값이 생긴다. 따라서 뒤에 사용할 때는 값이 있을수도 없을수도 있는 모르는 상태일 것이다. timerTask.cancel()을 그래로 쓴다면 지금에서는 에러를 낸다. 언제나 값이 있는 것이 아니기 때문이다. 하지만 ?를 붙이면 null일 수도 있다고 하는 것이기 때문에 괜찮아진다. 아직 Android Studio는 잘 모르지만 얼마전 ios수업을 들었을 때는 이런 값을 unpack하는 방법이 있었다. '!'로 했었는데 여기에도 unpack하는 방법이 존재할 것이라고 생각이 든다. 항상 값을 가지고 있는 것이 아닌 아무 값도 없는 null도 있을 수 있다는 것을 생각해두어야한다.

timerTask?.cancel()