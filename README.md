# DSS Controller 설치 가이드 (Python 기반, ROS 2 Humble)

이 문서는 **Ubuntu 22.04 / WSL2 환경에서 ROS 2 Humble + Python 기반 DSS Controller** 설치 과정을 안내합니다.

---

# 1. ROS 2 Humble 설치

## 1.1 기본 패키지 업데이트

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl gnupg lsb-release
```

---

## 1.2 ROS 2 Humble 저장소 추가 및 설치

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt update

curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.key | sudo apt-key add -

sudo sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros2-latest.list'
sudo apt update

sudo apt install ros-humble-desktop
sudo apt install python3-colcon-common-extensions
```

---

## 1.3 ROS 2 환경 설정

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

# 2. Python 기반 의존성 설치

C++ 개발용 라이브러리는 제거하고  
➡️ **Python 기반 NATS / Protobuf / ROS 2 의존성**으로 변경하였습니다.

---

## 2.1 필수 Python 패키지 설치

```bash
sudo apt update
sudo apt install -y python3-pip python3-venv
```

---

## 2.2 Python 가상환경 설정(선택)

```bash
python3 -m venv ~/dss_env
source ~/dss_env/bin/activate
```

---

## 2.3 Python 패키지 설치

```bash
pip install nats-py setuptools wheel
pip install protobuf==3.20.3

```

---

## 2.4 Protobuf 컴파일러 설치 (선택)

```bash
sudo apt install protobuf-compiler
protoc --version
```

---

# 3. 저장소 Clone

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
git clone https://github.com/kimbyoungkyu/dss_controller.git
```

---

# 4. 빌드하기 (Python 패키지 중심)

```bash
cd ~/ros2_ws
source /opt/ros/humble/setup.bash
colcon build --symlink-install
```

---

# 5. 실행하기 (브릿지 실행)

```bash
cd ~/ros2_ws
source ./install/setup.bash
ros2 run dss_controller dss_controller
```

---
