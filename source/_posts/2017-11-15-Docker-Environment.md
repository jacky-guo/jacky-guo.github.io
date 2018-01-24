---
title: "Nvidia-Docker環境設定&中文編碼問題"
subtitle: 
date: 2017-11-15 17:57:56
author: 
header-img: 
tags:
	- Environment Setting
	- Docker
	- Ubuntu 16.04
---

# 利用nvidia-docker 設置環境
```
sudo apt-get update
sudo apt-get install -y build-essential git
```

安裝 nvidia-docker
```
# Install nvidia-docker and nvidia-docker-plugin
wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```

測試 nvidia-smi 验证是否安装成功
```
sudo nvidia-docker run --rm nvidia/cuda nvidia-smi
```

從 Tensorflow 的 Docker Hub 拉 Image
```
sudo nvidia-docker run -d -p 8889:8888 --name test2 -v /home/jacky/Downloads:/workspace tensorflow/tensorflow:latest-gpu
sudo nvidia-docker exec -it 容器name bash 或者 sudo nvidia-docker exec -it 容器ID  
```
**-p 將外部的8889port對到內部的8888port**
**-v 將本機的Downloads文件夾掛載到Dockder的workspace**

進入容器後 通過以下指令可以得到 jupyter notebook 的 token
```
jupyter notebook list
```

用nvdia-docker替代docker命令
```
echo 'alias docker=nvidia-docker' >> ~/.bashrc
bash
```

啟動、停止、刪除docker container
```
sudo docker container ls -a                      //查看所有容器狀態
sudo docker ps 									 //查看啟動的容器
sudo docker container start container-name		 //啟動
sudo docker container restart container-name	 //重新啟動
sudo docker container stop container-name	 	 //終止容器
sudo docker container rm container-name         //刪除容器 (需要先終止容器)
```

# 解決Docker容器中文亂碼問題

當出入如下問題時
![](error-message.png)

通過locale指令 可以發現 當前編碼格式為 POSIX 
```
locale
```

解決方法：
step1: 安裝 locales 
```
apt-get update
apt-get install -y locales
```
step2: change locale setting
```
locale-gen en_US.UTF-8
export LANG=en_US.UTF-8 LANGUAGE=en_US.en LC_ALL=en_US.UTF-8
```

[docker install 1](https://wyde.github.io/2017/11/08/How-to-Install-Docker-CE-on-Ubuntu-16-04-and-Fedora-26/)
[docker install 2](https://wyde.github.io/2017/11/09/How-to-Install-Tensorflow-using-Docker-on-Ubuntu-16-04/)
[docker gitbook](https://yeasy.gitbooks.io/docker_practice/content/)
[Set the locale to UTF-8 for Python 3](https://webkul.com/blog/setup-locale-python3/)
