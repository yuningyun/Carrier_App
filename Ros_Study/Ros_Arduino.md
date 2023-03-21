# ros 아두이노

ros - arduino 사용을 위한 환경설정 방법

1. arduino에 라이브러리를 추가한다.
라이브러리명 : openagriculturefoundation/rosserial_arduino@0.0.0-alpha+sha.1834b766b0

2. ros 패키지를 설치한다.

```
sudo apt-get install ros-melodic-rosserial-arduino
sudo apt-get install ros-melodic-rosserial
```

ros버전이 Melodic으로 ros-melodic으로 설치를 진행한다.

아두이노 업로드 후 ros 실행해야 동작됨

ros 실행코드는 아래와 같다. 각 탭에 따로 작성해야한다.


```
roscore
rosrun rosserial_python serial_node.py _port:=/dev/ttyACM0 _baud:=57600

# ros topic을 확인하기 위해 작성
rostopic list

# topic에서 나오는 값을 확인하기 위해
rostopic echo {topic}
# 현재 코드에서
# rostopic echo /chatter
# rostopic echo /talk

# pub을 하여 바로 아두이노의 움직임을 확인하고 싶을 때
rostopic pub {topic-name} {msg-type} {data}

# 현재 코드에서 
# rostopic pub /talk std_msgs/String "data: 'on'"
# rostopic pub /talk std_msgs/String "data: 'off'"
```

ros 실행에서 _band를 57600으로 설정하였기 때문에 monitor_speed를 57600으로 설정해야 ros와 arduino의 통신이 가능하다.
이렇게 하지 않고 monitor_speed = 9600을 작성한다면  [ERROR] [1679396127.626042]: Lost sync with device, restarting…
를 발생시키며 통신이 끊겨 다른 것을 못하게 된다.
이를 주의하여 _band를 57600으로 잘 작성하여야 한다.

upload_port = /dev/ttyACM0를 작성하였으며 이는 아두이노가 연결되어 있는 포트 번호이다.
아두이노의 포트 번호를 확인하는 방법은 터미널에서 

ls /dev/tty*

을 작성하여 확인이 가능하다. 많은 것이 뜨지만 아두이노를 연결하고 확인하고 연결 안하고 확인하면 된다.


ini 파일 작성

```
[env:uno]
platform = atmelavr
board = uno
framework = arduino
monitor_speed = 57600
upload_speed = 115200
upload_port = /dev/ttyACM0
monitor_port = /dev/ttyACM0
board_build.filesystem = littlefs
build_flags = 
	-D MQTT_MAX_PACKET_SIZE=512
lib_deps = 
	bblanchon/ArduinoJson@^6.18.5
	frankjoshua/Rosserial Arduino Library@^0.9.1
	openagriculturefoundation/rosserial_arduino@0.0.0-alpha+sha.1834b766b0
```

아두이노 코드 작성

```
#include <Arduino.h>

#include <ros.h>
#include <std_msgs/String.h>

#define ledPin 13

ros::NodeHandle  nh;

std_msgs::String str_msg;
ros::Publisher chatter("chatter", &str_msg);

void led_turn( const std_msgs::String& cmd_msg)
{
  Serial.println(cmd_msg.data);
  if(!strcmp(cmd_msg.data, "on"))
  {
    digitalWrite(ledPin, HIGH);
    str_msg.data = "led_turn_on";
    chatter.publish( &str_msg );
  } else if(!strcmp(cmd_msg.data, "off"))
  {
    digitalWrite(ledPin, LOW);
    str_msg.data = "led_turn_off";
    chatter.publish( &str_msg );
  }
}

ros::Subscriber<std_msgs::String> sub("talk", &led_turn);

void setup()
{
  pinMode(ledPin, OUTPUT);

  Serial.begin(9600);

  nh.initNode();
  nh.subscribe(sub);
  nh.advertise(chatter);
}

void loop()
{
  nh.spinOnce();
  delay(1);
}
```