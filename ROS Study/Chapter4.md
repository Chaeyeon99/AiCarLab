I. 용어정리
Node: 최소 단위의 실행 가능한 프로세서
ex. 받은 로우 데이터를 각종 필터 처리할 때 한 각각의 노드, 프로세스를 짠다. 노드로 각각의 프로그램을 짠다. 각각의 기능별로 할 수 있다.

Packgae: 하나 이상의 노드를 묶음, 메타패키지
ex. 20개의 노드를 묶어놨을 때 어떤 프로그램이 작동

메세지를 나눠줘야함
모터는 모터끼리, 센서는 센서끼리, ...

Message: 메세지를 통해 노드간의 데이터를 주고 받는다. 형태를 point, boolean, integer ... 변수형태
많은 종류의 메세지


II. 메세지 통신
ROS에서 가장 기본이 되는 poinit: 노드간의 메세지 통신


메세지는 목적에 따라 4가지로 분류
1. Topic: 단방향 연속성을 가진 통신 방법
- Publisher: 메세지를 보내는
- Subscriber: 메세지를 받는
1:1, 1:n, n:1, n:n
같은 메세지를 복수의 subscriber가 받을 수 있다.

로봇의 정보를 topic 메세지 방식으로 전송 ...
일방적인 데이터를 보내야할 때 사용
ex. 센서 데이터

2. Service: 양방향으로 통신할 때 사용
ex. 지금 몇시야? 지금 12시야. -> 서비스 응답
로봇의 좌표 요청(service client) -> 동작처리, 끝났다고 응답(service surver)
양방향
일회성: 응답이 끝나면 접속이 끊긴다. 주고받고, 재접속..
cf. Topic은 계속 보낸다.

3. Action: 중간 중간 피드백을 날리고 마지막 결과값을 전달
복잡한 task, 장시간 걸리는 것, 피드백을 받고 싶을 때 사용
자주 사용하는 방식은 아니다.

III. 메세지
- 마스터

$roscore
//ROS가 제대로 설치되어 있는지 확인
노드 정보를 관리, 노드 통신을 연결해주는 매개체
XMLRPC:XML 기반의 간단한 서버클라이언트 시스템 구동
http://ROS_MASTER_URI:11311

$rosrun
노드 실행
토픽을 받는 노드(subscriber)을 실행되자마자 노드정보를 마스터에게 전달
노드의 이름, topic의 이름, 어떤 형태의 메세지를 보낼 것인지(레이다, 카메라..), ip번호와 포트번호 전송(네트워크정보)

퍼블리셔 노드도 실행되면 정보를 마스터에게 전달
->마스터는 전달받은 이 정보들을 매칭해준다. 
토픽이름과 메세지 형태 매칭. 맞으면 퍼블리셔의 정보를 서브스크라이버 노드에게 전달해준다. 

그러면 퍼블리셔의 정보가 있기 때문에 마스터가 필요없다. 직접적으로 TCPROS 접속 요청
퍼블리셔는 응답

그럼 TCPROS 로 데이터 송수신

서비스도 마찬가지 형태로 연결

* 메세지 통신 개념잡기
* turtlesim 패키지
$roscore 
//한번만 실행
$rosrun turtlesim turtlesim_node
//turtlesim_code : 노드 이름
노드 하나를 실행시켜라 터틀심 패키지 안에 이 노드를 -> subscriber 실행
$rosrun turtlesim turtle_teleop_key
//노드 하나를 실행시켜라 터틀심 패키지 안에 turtle_teleop_key 노드를 
$rosrun rqt_graph rqt_graph

cmd_vel: 전진 속도를 전송

- 예제 정리
서브스크라이버 노드정보:
/turtlesim, (노드이름)
/turtle1/cmd_vel, (토픽이름)
geomety_msgs/Twist,
http://192.168.4.100:50051


turtlesim_teleop_key: 키보드 좌우상하 입력, publisher 노드 정보발행, 실행
turtlesim_node: subscirber 노드
turtle/cmd_vel: 토픽의 이름
geomety_msgs/Twist: 전진 속도, 회전속도가 들어감
아이피번호, 포트번호

키보드에 해당되는 전진속도 회전속도가 메세지(geomety_msgs/Twist) 형태로 전송 및 프로세싱

메시지??
4. 파라미터
변수(ex. 글로벌 변수를 네트워크에서 지정)를 외부에서 변경시키고 그 변수를 다른 노드에서 실시간으로(혹은 임의의 시간으로) 받아서 프로세스를 바꿀 수 있다.

ex. Twist 메세지
Vector3 linear //전진 속도
Vector3 angular //회전 속도
Vector3 메시지 이름

float 64 x
float 64 y
float 64 z

전진속도 x축의 데이터를 float64로 전송하겠다. x, y, z 포함

즉, Twist는 6개의 속도값을 전송
(linear의 x,y,z angular의 x,y,z)

- 메시지는 노드 간에 데이터를 주고 받을 때 사용하는 데이터의 형태
토픽, 서비스, 액션은 모두 메세지를 사용
단순 자료형으로 구성 (integer, float boolean)
메세지 안에 메세지를 품고 있는 데이터 구조
메세지들이 나열된 배열과 같은 구조
ex. 레이저 스캔을 쓸 때 2차원의 배열로 데이터 전송
float32[] ranges
sensor_msgs/LaserScan

Ex. ROS 메시지 (geometry_msgs/Twist)
정보발행 -> 메세지 전송 -> 정보구독
키보드를 누르면 해당되는 메세지가 전송

IV. 네임
Name, TF client Library 이기종 디바이스 간의 통신

Name: 노드의 이름, 메세지의 이름을 어떻게 관리할 것인지

같은 이름 실행 불가
노드 이름 변경, 메세지 이름 변경

global: 문자 없이 이름을 바로 쓰거나 앞에 / 붙임
ex. /bar

private: ~ 를 붙임
ex. ~bar

V. 좌표변환 TF(transform)
각 조인트(joint)들의 상대 좌표 변환
tree의 형태로 조인트들간의 관계도 표시

VI. 클라이언트 라이브러리
다양한 언어 지원
ROS C++

VII. 이기종 디바이스 간의 통신
카메라를 동작하면 카메라의 정보를 받아보고 제어
네트워크 연결
원격으로 이미지 전송, 안드로이드 스마트폰 가속도 값을 PC에서 확인, 안드로이드 스마트폰으로 turtle bot 제어

VIII. 파일 시스템

IX. 빌드 시스템