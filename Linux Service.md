## 리눅스에서 Service를 이용하여 부팅시에 ROS가 실행되게 하기

1. 경로를 /etc/systemd/system/으로 변경

		$ cd /etc/systemd/system/
2. ros_init.service 파일을 생성(관리자 권한 필수)

		$ sudo nano ros_init.service
3. ros_init.service 파일안에 코드를 작성

		# /etc/systemd/system/ros_init.service

		[Unit]
		Description=Ros Init Daemon

		[Service]
		Type=simple
		ExecStart=/home/pc/Init/ros_init.sh
		

		[Install]
		WantedBy=multi-user.target

	- ExecStart는 스크립트 파일이 위치하는 경로에 맞춰서 지정한다.
4. 경로를 ExecStart에 입력한 디렉토리로 변경하고 ros_init.sh파일을 생성

		cd ~/Init/
		nano ros_init.sh
5. ros_init.sh파일 안에 코드를 작성

		#! /bin/bash

		source /opt/ros/kinetic/setup.bash
		source /home/pc/catkin_ws/devel/setup.bash

		sleep 3
		roslaunch rosbridge_server rosbridge_websocket.launch

6. ros_init.sh파일에 실행권한을 준다

		sudo chmod +x ros_init.sh
7. systemctl을 이용해서 데몬을 리로드하고 ros_init.service를 실행하고 상태를 확인한다.

		systemctl daemon-reload
		systemctl start ros_init.service
		systemctl status ros_init.service
8. 상태 확인 결과가 이상하면 에러를 수정한다.(아마 대부분 스크립트파일 ros_init.sh에서 발생할 듯), 에러가 발생하지 않으면 ros_init.service를 자동 실행 서비스로 등록한다.(등록을 해야 부팅시 자동실행)

		자동 실행 등록
		systemctl enable ros_init.service

		자동 실행 해제
		systemctl disable ros_init.service

