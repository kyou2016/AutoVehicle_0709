# WeCar 시뮬레이터 실행하는 방법

1. 시뮬레이터 경로로 이동하여서 시뮬레이터를 관리자 권한으로 실행

		sudo ./WeCarSimulator.x86_64

2. 새 터미널에서 rosbridge를 실행한다.

		roslaunch rosbridge_server rosbridge_websocket

3. 시뮬레이터에 로그인(KunSan_JMS, kunsanjms) 후 맵에 들어가서 rosbridge와 시뮬레이터를 연결한다.

		network - apply
		sensor - confirm
4. rosbridge에서 연결이 되었는지 확인하고 새 터미널에서 다른 소스들을 실행하고 rviz를 실행하여 확인한다
