# WeCar 시뮬레이터 실행하는 방법

1. 시뮬레이터 경로로 이동하여서 시뮬레이터를 관리자 권한으로 실행

		sudo ./WeCarSimulator.x86_64

2. 새 터미널에서 rosbridge를 실행한다.

		roslaunch rosbridge_server rosbridge_websocket

3. 시뮬레이터에 로그인(KunSan_JMS, kunsanjms) 후 맵에 들어가서 rosbridge와 시뮬레이터를 연결한다.

		network - apply
		sensor - confirm
4. rosbridge에서 연결이 되었는지 확인하고 새 터미널에서 다른 소스들을 실행하고 rviz를 실행하여 확인한다

# 각 코드 설명

## kinematics_with_imu.py
시뮬레이터의 imu, lidar에서 토픽을 받아 odometry를 만드는 코드

## make_path_with_imu.py
odometry의 시간당 위치를 경로에 txt파일로 만들어 실시간으로 입력하는 프로그램
종료하면 저장이 된다.
실행하면 해당 경로의 txt파일은 초기화된 상태로 시작한다.

## load_path.py
입력된 경로의 txt파일을 읽어서 경로를 publish해주는 코드
pure pursuit에 필요한 코드

## pure_pursuit.py
읽어온 경로를 추종하여 따라가는 코드

### 하위 폴더의 .git폴더 삭제하는 명령어 (우분투)
		find . -mindepth -name '.git' -prune -exec rm -rf {} +
