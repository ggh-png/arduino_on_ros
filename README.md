 ros에 아두이노 연동 방법

## 아두이노 사용
1. 
아두이노 설치의 경우 터미널창 'arduino' 를 치면 깔아야하는 명령어 자동으로 유도해준다. -> 설치시 home 경로에 아두이노 설치됨
<br/><br/><br/>
2. 
port 권한 문제 port(USB) 권한을 승인해주어야 IDE에서 대응하는 PORT가 뜬다.<br/>

    ls -l /dev/tty*
    
명령어를 통해 아두이노 port를 찾고 

    sudo chmod a+rw /dev/ttyUSB~ 
    
를 통해 해당 포트 권한을 해제하기 !
<br/><br/><br/>
## ROS와 아두이노 연동 -> rosserial 설치

1.  

    sudo apt-get install ros-melodic-rosserial 
    
이는 PC의 ROS는 TCP/IP 기반의 통신을 하기때문에, 
아두이노 값을 serial 통신으로 받아와 tcp/ip로 중재할 수 있는 serial_server로 동작가능한 노드생성을 위해 다운.
<br/><br/>
2-1. 

    sudo apt-get install ros-melodic-rosserial-arduino 
    
이는 아두이노가 ros통신을 위해 serial_client로 동작하기 위함. 


<br/><br/>
2-2. 
아두이노 라이브러리 경로에서 (보통 ~/Arduino/libraries 경로) 

    rosrun rosserial_arduino make_libraies.py . 
    
실행시, ros_lib가 해당 경로에서 설치됨(이미 설치된 파일이 존재시, rm -rf ros_lib 를 통해 삭제) 

 ros_lib 설치시, 통신포트는 기본으로 설정된다.( 57600bps)<br/>
라이브러리의 ArduinoHardware.h 파일에서 통신속도를 변경할 수 있음
(115200bps의 속도는 메시지 개수가 많아지면 응답,처리속도가 느려질 수 있다.)

<br/><br/>

3. arduino IDE의 스케치메뉴의 라이브러리 가져오기를 통해 ros_lib를 가져오면 해당 예제를 사용할 수 있다.
<br/><br/>


4. 
  ros와 통신하기 위해서는 roscore를 항상 실행시켜주어야 하며

    rosrun rosserial_python serial_node.py 
    
  로 serial_server인 중재 노드를 실행시켜주어야 ros와 연동이 가능해진다.
