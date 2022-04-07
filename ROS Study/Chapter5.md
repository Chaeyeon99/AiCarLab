ROS 명령어

I. ROS 명령어 정리
command-line tools

II. ROS 쉘 명령어
roscd: ros+cd 지정한 ROS 패키지의 디렉토리로 이동 
rosls: ROS패키지 파일목록 확인
rosed: ROS패키지 파일 편집

III. ROS 실행 명령어
노드 실행, 다른 노드 및 패키지 설정 변경
roscore: ROS네임 서비스(master), rosout(로그기록), 파라미터 관리(parameter server)
rosrun:노드 실행
roslaunch: 노드 여러 개 실행 및 실행 옵션 설정
복수의 노드를 한꺼번에 실행시킬 수 있는 실행 파일
rosclean: ROS 로그파일을 검사하거나 삭제

IV. ROS 정보 명령어
rostopic: ROS 토픽 정보 확인
rosservice: ROS 서비스 정보 확인
rosnode: ROS 노드정보 확인
rosparam: ROS 파라미터 정보확인, 수정
rosbag: ROS 메시지 기록,재생
rosmsg: ROS 메시지 정보확인
rossrfv: ROS 서비스 정보 확인
roversion: ROS 패키지 배포 릴리즈 버전 정보 확인
rosswtf: ROS 시스템 검사

V. ROS catkin 명령어
로스의 컴파일, 빌드 관련 시스템
catkin 명령어를 통해 빌드를 한다.

빌드시스템을 이용하여 현재 패킷을 수행했는데 그 패킷에 대한 정보를 갱신, 워크스페이스 지정, 전환 등

catkin_create_pkg: 패키지 자동 생성
catkin_make: 캐킨 빌드 시스템에 기반을 둔 빌드
catkin_eclipse: 캐킨 빌드 시스템으로 생성한 패키지를 이클립스에서 사용할 수 있게 변경
catkin_prepare_release: 릴리즈할 때 사용되는 로그 정리 및 버전 태깅
catkin_generate_changelog: 릴리즈할때 CHANGELOG.rst 파일 생성 또는 업데이트
catkin_init_workspace: 캐킨 빌드시스템의 작업 폴더 초기화
catkin_find: 캐킨 검색

->빌드 관련 명령어

VI. ROS 패키지 명령어
rospack: ROS 패키지와 관련된 정보 보기
rosinstall: ROS 추가 패키지 설치
rosdep: 해당 패키지의 의존성 파일 설치
roslocate: ROS 패키지 정보 관련 명령어
roscreate-pkg: ROS 패키지 자동생성
rosmake: ROS 패키지를 빌드

wiki.ros.org