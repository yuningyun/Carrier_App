# Ros Tutorial

# 목차
1. [Ros_설치](#Install-Ros)
2. [Ros_패키지_생성](#Create-Ros-Package)
3. [Ros_패키지_빌드](#Building-Ros-Package)
4. [ROS_노드](#ROS-Nodes)
5. [ROS_토픽](#ROS-Topics)

# Install Ros

ros를 사용하고자하는 보드와 컴퓨터에 설치되어 있는 ubuntu 커널은 18.04 버전이다. ROS는 ubuntu 버전에 따라 설치하는 버전이 달라지기 때문에 어느 환경에서 사용할 것이지가 매우 중요하다. 

|ubuntu 버전|ROS버전|
|-----------|---------|
|16.04 LTS|Kinetic|
|18.04 LTS|Melodic|
|20.04 LTS|Noetic|

Ubuntu 18.04 LTS 버전을 사용하고 있기 때문에 ROS Melodic을 설치한다.

http://wiki.ros.org/melodic/Installation/Ubuntu

위에 사이트에 있는 내용을 따라 Melodic설치를 진행하였다.

1. 1. packages.ros.org에 있는 소프트웨어를 컴퓨터에서 허용할 수 있도록 명령어를 입력한다.

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

1. 2. 설치를 위한 키를 설정한다.

```
sudo apt install curl # if you haven't already installed curl

curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

1. 3. 데비안 패키지를 업데이트 한 후, 설치한다.

```
sudo apt update
```

full 로 설치 할 경우

```
sudo apt install ros-melodic-desktop-full
```

개별 패키지를 설치하고 싶은 경우

```
sudo apt install ros-melodic-<패키지이름>
```

패키지 설치 확인

```
apt search ros-melodic
```

1. 4. ROS를 사용하기 전에 rosdep를 초기화 해야한다. rosdep를 사용하면 컴파일 하려는 소스에 종속된 시스템을 쉽게 설치 가능하다.
 
```
sudo rosdep init
```

```
rosdep update
``` 

1. 5. 새로운 쉘이 실행될 때마다 ROS 환경변수가 bash에 자동으로 추가되는 것이 편리하기 때문에 ~/.bashrc 파일을 수정한다.

```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc (혹은 ~/.bashrc 파일에 직접 ""안의 문장을 집어넣어도 된다.)
```
 
```
source ~/.bashrc
```
 
1. 6. 패키지 컴파일을 위해 필요한 것들을 추가로 설치해준다.

```
sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential
```

workspace 생성

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```

Package 정보 얻기. 패키지 경로 반환 받는 법
```
rospack find [패키지 이름]
```

예를 들어
```
rospack find roscpp
```



# Create Ros Package



# Building Ros Package

# ROS Nodes

# ROS Topics
