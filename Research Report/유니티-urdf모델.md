### PC2에 ROS 설치
Ubuntu 18.04 -> melodic //현재 우리가 사용하고 있는 ubuntu 버전
**한 줄 설치 명령어**
wget https://raw.githubusercontent.com/orocapangyo/meetup/master/190830/install_ros_melodic.sh && chmod 755 ./install_ros_melodic.sh && bash ./install_ros_melodic.sh

**key 설정 오류**

sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

sudo apt install curl 

curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

sudo apt update //Debian 패키지 목록 최신화

---

### ROS와 연동없이 ROS URDF 파일 자체를 유니티에서 바로 import (Unity version 2018.3 이상, .NET 4.x)

**ROS bridge client 설치 (ROS #)**

Unity project settings에서 playe -> other settings -> configuration .NET 4.X 설정
siemens/ros-sharp 에서 해당하는 패키지만 다운 후 Unity로 끌어옴

유니티 재실행시, ROS bridge client window창이 추가

**URDF import**
scout_v2 게임 오브젝트 생성
실체는 없고 collider 형태로만 존재

![dd](https://user-images.githubusercontent.com/82865552/162558181-5f7214e0-0630-4fab-ada6-5346149258b4.PNG)


**.dae**

.dae: 3d 교환 파일 형식으로, 유니티에 사용하는 3d 파일 확장자인 obj 또는 fbx로 변환

- 파일구성

![파일구성](https://user-images.githubusercontent.com/82865552/162558279-1527f50f-137b-440a-9f88-50f4463fb61a.PNG)

- base_link (몸체)

![baselink](https://user-images.githubusercontent.com/82865552/162558289-49dde25e-aa71-459b-9933-6e3d7811f540.PNG)

- hokuyo(라이다)

![lidar](https://user-images.githubusercontent.com/82865552/162558293-7ed1154b-7059-44c5-8847-35e171d27f46.PNG)

- D435(깊이 지각 카메라 Intel realsense)

- I515(라이다 카메라, intel realsense)

- wheel_type1(앞바퀴)

![wheeltype1](https://user-images.githubusercontent.com/82865552/162558296-37511901-239e-4f22-836c-1eb5055182fa.PNG)

- wheel_type2(뒷바퀴)

![wheeltype2](https://user-images.githubusercontent.com/82865552/162558298-b0e2a623-c996-43e5-af79-daeccf69e282.PNG)

![car2](https://user-images.githubusercontent.com/82865552/162558312-e3915182-59d8-4cae-94bd-5b9a7b031bde.PNG)


**실제 WeGoCar와 Unity에서의 WeGoCar**

![wegocar](https://user-images.githubusercontent.com/82865552/162558320-8b75820c-a2a0-4b9b-8b70-44f394b6bbfd.jpg)
![car](https://user-images.githubusercontent.com/82865552/162558323-4a136abb-be67-42b3-8ddb-503b5c2aa180.PNG)


- ROS connector 스크립트를 통해 웹소켓 연결 후 ROS와 통신이 가능할 것

- URDF Robot 스크립트 속성들 사용관련 study 필요
