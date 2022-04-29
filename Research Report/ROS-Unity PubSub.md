### ROS-Unity Publish
ros bridge 실행

- rqt graph

![image](https://user-images.githubusercontent.com/82865552/165927169-01ced962-3f3d-4a52-a865-4bdb26f7c192.png)


publisher : talker.py
(ArchivosPY.tar.gz)

![image](https://user-images.githubusercontent.com/82865552/165927790-d37f459e-427b-461c-af7e-a5e57aa6d60d.png)

command

cd ~/catkin_ws

catkin_make

source ./devel/setup.bash

rosrun beginner_tutorials talker.py

* 패키지 오류(does not exist Tutorial_beginner)

catkin ws /src

catkin_create_pkg beginner_tutorilas message_generation std_msgs rospy

파이썬파일을 사용하고 메세지를 publish 할 수 있게 해준다는 명시어

xml 파일 생성 

![image](https://user-images.githubusercontent.com/82865552/165927571-925f4744-dfd4-49b8-acf1-6ab9613f20b3.png)

- rqt graph

![image](https://user-images.githubusercontent.com/82865552/165927195-7af2e467-b845-4e87-b984-2ebfe587494f.png)


### ROS PC RUN

![Uploading image.png…]()

![Hnet com-image (1)](https://user-images.githubusercontent.com/74848401/165255395-24614146-292e-4279-b340-cd789f2fa2ee.gif)

### ROS-Unity Subscribe

unity version 2021

ROS sharp - ROS Bridge 사용

create empty (ros connector)

Script: PoseStampedSubscriber, ROSConnector

PoseStampedSubscriber.cs

```
using UnityEngine;
namespace RosSharp.RosBridgeClient
{
    public class PoseStampedSubscriber : UnitySubscriber<MessageTypes.Geometry.Pose>
    {
        //public Transform PublishedTransform;

        public Vector3 position;
        public Quaternion rotation;
        private bool isMessageReceived;

        protected override void Start()
        {
			base.Start();
		}
		
        private void Update()
        {
            if (isMessageReceived)
                ProcessMessage();
        }

        protected override void ReceiveMessage(MessageTypes.Geometry.Pose message)
        {
            position = GetPosition(message).Ros2Unity();
            rotation = GetRotation(message).Ros2Unity();
            isMessageReceived = true;
        }

        private void ProcessMessage()
        {
            //PublishedTransform.position = position;
            //PublishedTransform.rotation = rotation;
        }

        private Vector3 GetPosition(MessageTypes.Geometry.Pose message)
        {
            return new Vector3(
                (float)message.position.x,
                (float)message.position.y,
                (float)message.position.z);
        }

        private Quaternion GetRotation(MessageTypes.Geometry.Pose message)
        {
            return new Quaternion(
                (float)message.orientation.x,
                (float)message.orientation.y,
                (float)message.orientation.z,
                (float)message.orientation.w);
        }
    }
```

Topic: /chatter_

Serializer: Newtonsoft_JSON

Ros Bridge Server Url: ws://(웹소켓 연 IP주소)

- rqt graph
pub/sub 잘 연결되어 있어 양방향 통신
![image](https://user-images.githubusercontent.com/82865552/165927210-301b76ba-c4c7-4c4f-b780-508459c02c28.png)

### Unity PC RUN
![Hnet com-image (2)](https://user-images.githubusercontent.com/74848401/165256211-27200d9f-8c2f-430c-a933-292c9bc6e5c5.gif)

![Hnet com-image](https://user-images.githubusercontent.com/74848401/165251839-2d2a0240-2c84-47f4-a995-3d55c62d6b6f.gif)

