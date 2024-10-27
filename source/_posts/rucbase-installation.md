---
title: rucbase-installation
date: 2024-10-27 09:10:09
tags: Database
---

# RucBase 数据库实验环境安装
<iframe src="//player.bilibili.com/player.html?isOutside=true&aid=113375174459879&bvid=BV1Jz14YcETQ&cid=26479496308&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
## 环境说明
![env](env.png)
## 安装QEMU
[QEMU官方文档](https://www.qemu.org/docs/master/)
```bash
brew install qemu
```
## 安装Ubuntu 24.04 LTS
### 下载Ubuntu 24 ISO
```bash
wget https://ubuntu.com/download/server/thank-you?version=24.04.1&architecture=amd64&lts=true
```
### 创建虚拟磁盘
```bash
qemu-img create -f qcow2 /Users/stepbystep/Documents/ubuntu/mykvm.qcow2 30G
qemu-img check /Users/stepbystep/Documents/ubuntu/mykvm.qcow2
```
### 启动虚拟机
```bash
qemu-system-x86_64 \
-m 8192 \
-smp 4 \
-name mykvm \
-cdrom /Users/stepbystep/Downloads/ubuntu-24.04.1-live-server-amd64.iso \
-drive file=/Users/stepbystep/Documents/ubuntu/mykvm.qcow2,if=ide,format=qcow2 \
-nic user,model=virtio-net-pci,hostfwd=tcp::2222-:22 \
-boot d &
```
### 安装系统(见视频)

## 基础系统配置
```bash
sudo apt install zsh git build-essential cmake flex bison libreadline-dev vim inetutils-ping psmisc
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
ip a
sudo ip link set enp0s3 up
sudo dhcpcd
sudo systemctl status ssh
sudo apt update
sudo apt upgrade
sudo apt install lsof
mkdir mihomo
chmod +x ./mihomo/mihomo
```
## 源码编译
```bash
git clone --recursive https://github.com/HuangDunD/rucbase-djb2024summer.git
cd rucbase-djb2024summer
git submodule init
git submodule update
cd deps/googletest
mkdir build
cd build
cmake .. && make -j8
sudo make install
cd ..
mkdir build
cd ..
cd rucbase-djb2024summer
cd build
cmake ..
vim ../src/common/config.h
make rmdb -j4
make lru_replacer_test -j4
cd ../rucbase_client
mkdir build
cd build
cmake .. && make -j4
cd ../..
cd build
make lru_replacer_test -j4
./bin/lru_replacer_test
cd
```
## 安装Docker Engine
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
export DOWNLOAD_URL="https://mirrors.bfsu.edu.cn/docker-ce"
curl -fsSL https://raw.githubusercontent.com/docker/docker-install/master/install.sh | sh
```
## 容器启动
```bash
sudo vim /etc/docker/daemon.json
sudo systemctl daemon-reload
sudo systemctl restart docker
sudo docker pull djb2023/rucbase_lab:djb2024
sudo docker run --platform linux/amd64 --user root -e GRANT_SUDO=yes -e PATH=/usr/local/cmake/cmake-3.17/bin/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin -dit djb2023/rucbase_lab:djb2024 /bin/bash
sudo docker ps -a
sudo docker exec -it 073233363e33 /bin/bash
sudo groupadd docker
sudo usermod -aG docker $USER
exit
newgrp docker
docker ps
```
## IDE配置
### 配置免密
```bash
vim  ~/.ssh/config

Host sql
  HostName localhost
  User peter
  Port 2222

ssh-copy-id sql
```
安装VS Code, 左下角点击连接,打开/目录,即可看到实验文件夹