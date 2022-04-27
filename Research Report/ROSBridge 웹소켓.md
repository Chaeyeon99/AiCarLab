$roscore <br/>
ROS_MASTER_URI=http://swu:11311/

$ifconfig

$ipconfig

enp2s0: 유선랜으로 연결되었을 때의 주소
lo: local 로 그냥 자기 자신을 계속 loop calling
wlpls0: 무선랜(wifi)로 연결되었을 때의 주소
inet 부분이 ip주소 

*주의사항: 통신하고자 하는 두 PC는 같은 LAN(Wi-fi)을 사용하고 있어야 함.

웹소켓 통신: 두 프로그램 간 메세지를 교환하기 위한 통신 방법
양방향 통신, client-server 송수신 동시에 처리
실시간 네트워킹 
handshaking...


**ROS Bridge - ROS Connector 연결

rosbridge: ROS 환경에서 실행되는 노드로, 웹소켓을 생성하여 ROS와 비ROS 사이에 JSON 형식으로 통신함으로써 ROS의 범용성을 높임.


**ROS

Web Socket 기반 rosbridge_suite 라이브러리
ros bridge 설치
ros bridge 실행(마스터 노드 구동)
WebSocket on port 9090 by default
오류 발생 시, 업데이트
$ sudo apt-get update


우분투 18.0에서 rosbridge 설치 명령어
$sudo apt-get install ros-melodic-rosbridge-suite

rosbridge 실행 명령어
$roslaunch rosbridge_server rosbridge_websocket.launch

![우분투2](https://user-images.githubusercontent.com/82865552/163678376-ac86da94-f090-4c19-93c6-e934d5ef05be.jpg)
![우분투3](https://user-images.githubusercontent.com/82865552/163678381-02c3dafa-509b-40d5-a104-b82f5574274e.jpg)


0.0.0.0:9090 접속

![우분투1](https://user-images.githubusercontent.com/82865552/163678368-4dfe4857-3fc5-4bcf-b7fd-65384b3fc9ae.PNG)


유니티와 ROS 통신을 위해 로컬 IP주소 확인
$hostname -I

default port는 web 8080으로 되어 있으나, default 포트번호를 확인하기 위한 명령어

$ roscd  rosbridge_server

$ cd launch

$ cat rosbridge_websocket.launch


 <launch>
   <arg name="port" default="9090" />
   ..
 </launch>


이상태로 PC에서 Chrome을 열고 IP주소와 포트번호를 넣었을 때 실행되면 다른 PC에서도 접속할 수 있는 웹소켓 실행상태. ex. http://0.0.0.0:9090

![우분투4](https://user-images.githubusercontent.com/82865552/163678387-2959644a-b1ce-4c4c-8be0-205d793ca5a3.PNG)


**Unity

WebSocket 연결할 url 지정 (ex. ws://0.0.0.0:9090)
Twist publisher
ROS와 주고받을 Topic 지정 /cmd_vel

![유니티1](https://user-images.githubusercontent.com/82865552/163678336-ea26bbe9-3954-4e87-ac61-734b68f49fdf.PNG)

![유니티2](https://user-images.githubusercontent.com/82865552/163678343-15bbab7e-a56a-4159-87ed-e41a122e8fed.PNG)


이후 각각 publisher와 subscriber python 코드 작성 필요
Socket 통신 서버, 클라이언트 구축
