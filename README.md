@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');

# Carrier_App

# **new project 생성**

![Untitled](https://user-images.githubusercontent.com/90883561/216004386-5e7b09f3-dd53-4822-b685-5d3a849c636e.png)

![Untitled (1)](https://user-images.githubusercontent.com/90883561/216004445-5652ec4f-3d47-48e8-b83d-3bc0db7b8405.png)
얼마나 많은 사람들이 사용할 수 있는지 알려준다. API LEVEL이 높을 수록 최신 모델이며 사용가능한 핸드폰의 %(퍼센트)는 줄어드는 것을 볼 수 있다. 버전에 따라 지원하는 것의 양도 다르기 때문에 확인을 잘하고 선택해야한다. 많은 사람들이 사용할 수 있어도 성능이 따라주지 않을 수 있으면 사용의 이유가 없어지기 때문에 잘 확인해야한다.

90%이상이 사용하며 Media, Wireless & Connectivity가 가능한 API26:Android 8.0(Oreo)를 선택하여 먼저 테스트를 해보도록 하겠다. 언어는 Kotlin을 사용할 예정이다. Kotlin은 JAVA와 유사하지만 조금 더 쉽고 JAVA또한 지원이 되며 간결하게 적을 수 있다는 장점이 있는 언어이다. 

![Untitled (2)](https://user-images.githubusercontent.com/90883561/216004509-d4bf2cda-ffcc-456a-9761-ab8f86279153.png)


# 프로젝트 생성 후

![Untitled (3)](https://user-images.githubusercontent.com/90883561/216004552-5c7757db-385a-4197-a17c-dbb7536332f8.png)


위는 가장 주요하게 사용하는 두 파일이다.

- **.xml —> App의 겉모습. 즉 사용자가 보는 화면이다.**
- **.kt —> 동작을 실행하기 위해 존재하는 파일이다.**

두 파일이 클래스로 연결되어 작동하게 된다.

- **디바이스 만들기**

![Untitled (4)](https://user-images.githubusercontent.com/90883561/216004585-1eafced7-8ec0-4c65-a09a-f29550d257a8.png)


클릭하면 아래와 같은 창이 열리게 되고 Create virtual device를 클릭한다.

![Untitled (5)](https://user-images.githubusercontent.com/90883561/216004615-ee4fd605-9b39-4547-96de-33051e847edf.png)


![Untitled (6)](https://user-images.githubusercontent.com/90883561/216004646-1110c373-d412-427c-8980-26eda07faa06.png)


클릭하였을 때 등장하게 되는 창이며 구글 플래이 스토어를 지원하는 **Pixel2**를 가상디바이스로 만들어 사용할 예정이다.

![Untitled (7)](https://user-images.githubusercontent.com/90883561/216004671-a2626929-d195-41a4-b793-b02aaa687d18.png)


다음으로 안드로이드 버전을 선택하는 창이 등장하는데 나의 핸드폰에서 돌리기위해 어떤 것이 필요한 지는 잘 모르겠어서 일단 인터넷에서 찾은 방법에서 R을 사용하고 있기 때문에 같은 버전으로 만들고자한다. (일단 시도를 해보는 것이 먼저 인것같다.)

옆에 있는 다운로드 버튼을 눌러 설치를 진행한다.

설치가 완료되고 난후 next를 눌러 다음으로 넘어가고 디바이스의 이름을 작성한 후 finish를 눌러 virtual device를 생성한다.

![Untitled (8)](https://user-images.githubusercontent.com/90883561/216004714-79f75ae2-4a0a-4e28-877e-bfff6bec1f13.png)


no device에서 first phone으로 변경된 것을 볼 수 있다.

# 에러 발생

![Untitled (9)](https://user-images.githubusercontent.com/90883561/216004755-dad07f5d-325b-4178-9686-0e91b41e1b96.png)


생성할 때부터 이게 존재하면 안되는 것으로 보인다.

가상디바이스에서 실행이 완전히 안되는 것을 볼 수 있다.

이를 해결하기 위해 

```diff
sudo apt install qemu-kvm
```

코드를 작성하여 설치를 진행한다.


![Untitled (10)](https://user-images.githubusercontent.com/90883561/216004797-1e9e7149-1cfc-40d6-900f-cf7d813096ec.png)


설치 완료 후

![Untitled (11)](https://user-images.githubusercontent.com/90883561/216004849-aadb75da-0364-49fd-8a28-9c478c20b1ef.png)
```diff
ls -al /dev/kvm

grep kvm /etc/group
```

을 작성하여 사용자 등록이 되어 있는지 확인한다. 현재 상태에서 등록이 되어 있지 않으므로 사용자 등록을 진행해야한다.
```diff
sudo adduser $USER kvm

sudo chown $USER /dev/kvm
```

명령어를 사용하여 등록을 진행하며 $USER 대신 yun을 입력하여 추가하여도 된다. 위 두 명령어 중 하나만 동작하여도 상관없다.

![Untitled (12)](https://user-images.githubusercontent.com/90883561/216004900-4aeaf720-8a93-43d4-9a37-6d5c0954dc41.png)

![Untitled (13)](https://user-images.githubusercontent.com/90883561/216004938-bb7c1548-760f-43fc-a89b-bab59e485df7.png)


위 코드가 동작했을 때 다음과 같이 변경되는 것을 확인 할 수 있다.

![Untitled (14)](https://user-images.githubusercontent.com/90883561/216004982-3371c383-51eb-405d-9755-9abd2d28ddba.png)


추가 후 어떤한 에러코드도 등장하지 않는 것을 확인할 수 있었으며 생성도 잘 되고 실행이 되는 것을 볼 수 있다.

![Untitled (15)](https://user-images.githubusercontent.com/90883561/216005035-ed17f93b-3a38-40cc-a2fe-ecf6e8216437.png)

![Untitled (16)](https://user-images.githubusercontent.com/90883561/216005076-18a91319-0524-43a6-995f-abd187a8f62a.png)


어떻게 해서 생성하는 것까지는 완료하였다. 하지만 원래 앱이 나타나야하는데 나타나지 않고 계속해서 오류를 발생시키는 문구가 등장하였다.

![Untitled (17)](https://user-images.githubusercontent.com/90883561/216005108-f1d79c30-dc49-47f8-bdde-002f7a5ddc05.png)

[오류문구 전체 내용](https://github.com/yuningyun/Carrier_App/blob/89b39b707756914b30a909453bd208301f714e62/Error%20All%20text1)

다른 에러가 다시 발생하였다. 그것은 build.gradle(:app)에 찾아 들어가서 compleSdk 와 targetSdk가 32로 적혀져 있었는데 돌아가기 위해서는 33으로 변경해주어야 한다.

![Untitled (18)](https://user-images.githubusercontent.com/90883561/216005155-ed63ddc5-79ed-45e2-8a8b-23d0f65c0705.png)


변경을 하고나서 다음과 같이 앱이 열리는 것을 볼 수 있었다.


![Untitled (19)](https://user-images.githubusercontent.com/90883561/216005200-e65b0b93-e057-440a-80cb-1674ab374733.png)

