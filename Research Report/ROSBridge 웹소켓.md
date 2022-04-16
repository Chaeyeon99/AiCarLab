$roscore
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


** ROS Bridge - ROS Connector 연결
rosbridge: ROS 환경에서 실행되는 노드로, 웹소켓을 생성하여 ROS와 비ROS 사이에 JSON 형식으로 통신함으로써 ROS의 범용성을 높임.


** ROS

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

0.0.0.0:9090 접속

유니티와 ROS 통신을 위해 로컬 IP주소 확인
$hostname -I

default port는 web 8080으로 되어 있으나, default 포트번호를 확인하기 위한 명령어

$ roscd  rosbridge_server

$ cd launch

$ cat rosbridge_websocket.launch

<launch>
  <arg name="port" default="9090" />
    ...
</launch>

이상태로 PC에서 Chrome을 열고 IP주소와 포트번호를 넣었을 때 실행되면 다른 PC에서도 접속할 수 있는 웹소켓 실행상태. ex. http://0.0.0.0:9090

** Unity
WebSocket 연결할 url 지정 (ex. ws://0.0.0.0:9090)


이후 각각 publisher와 subscriber python 코드 작성 필요
Socket 통신 서버, 클라이언트 구축