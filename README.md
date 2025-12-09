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

sudo 제 실행)

```bash
cd ~/ros2_ws
source ./install/setup.bash
ros2 run dss_controller dss_controller
```

---
