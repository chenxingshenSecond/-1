# 在远程连接到可视化docker 
https://mp.weixin.qq.com/s?__biz=MzI4MzAwNTQ3NQ==&mid=209866190&idx=1&sn=0ee75509eb2fab454009125e0a8c6437&scene=0#rd
https://blog.csdn.net/ericcchen/article/details/79253416

# 在不能连接到外网的服务器上，下面的网址下载deb来安装。 
https://apt.dockerproject.org/repo/pool/main/d/docker-engine/ 
sudo dpkg -i ***.deb 

及时绕过了这个墙 外面还有一层公司的不能连接dockerhub的问题。 

sudo apt-get install x11-xserver-utils




docker run -d \
-v /etc/localtime:/etc/localtime:ro 
-v /tmp/.X11-unix:/tmp/.X11-unix 
-e DISPLAY=unix$DISPLAY 
-v $HOME/slides:/root/slides 
-e GDK_SCALE 
-e GDK_DPI_SCALE 
--name libreoffice 
jess/libreoffice

开启docker图形话界面时候的指令，主要是： nvidia-docker run --shm-size=8gb -it -v pwd:/workspace -e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix 1240803839cgw/cuda_caffe:latest

开机需要执行 xhost +

# 如果是远程的GUI显示 则需要进行额外的操作： 

首先windows需要下载一个Xming跑起来，

docker run -d \
  -v /etc/localtime:/etc/localtime:ro \
  --net=host \
  -e DISPLAY=:10.0 \
  -v $HOME/slides:/root/slides \
  -v $HOME/.Xauthority:/root/.Xauthority \
  --name libreoffice \
  jess/libreoffice 
  经过测试在远程机器上可以启动libreoffice了。 
  
  
  # 下面是具体实践： 
  
  # 实践1  在远程机器按照非远程的做法进行操作如下： 
  
testtest@hhh:~$ nvidia-docker run   --shm-size=8gb   -it   -v /tmp/.X11-unix:/tmp/.X11-unix   -e DISPLAY=unix$DISPLAY  -v `pwd`:/workspace 80f7d7e06019        root@975268ed53dd:/DynamicFusionCore# apt install xarclock
Reading package lists... Done
Building dependency tree

Reading state information... Done
The following NEW packages will be installed:

xarclock

0 upgraded, 1 newly installed, 0 to remove and 147 not upgraded.
Need to get 17.3 kB of archives.

After this operation, 71.7 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu xenial/universe amd64 xarclock amd64 1.0-13 [17.3 kB]
Fetched 17.3 kB in 1s (15.5 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package xarclock.
(Reading database ... 41993 files and directories currently installed.)
Preparing to unpack .../xarclock_1.0-13_amd64.deb ...
Unpacking xarclock (1.0-13) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up xarclock (1.0-13) ...
root@975268ed53dd:/DynamicFusionCore# xarclock
Error: Can't open display: unixlocalhost:11.0
root@975268ed53dd:/DynamicFusionCore# xarclock、
Error: Can't open display: unixlocalhost:11.0
证明了远程如果不开相关的端口，以及其他失败了 


# 实践2   
nvidia-docker run   --shm-size=8gb   -it    --net=host   -e DISPLAY=:10.0   -v $HOME/slides:/root/slides   -v $HOME/.Xauthority:/root/.Xauthority    -v `pwd`:/workspace 80f7d7e06019   


nvidia-docker run   --shm-size=8gb   -it    --net=host   -e DISPLAY=:10.0  -v $HOME/.Xauthority:/root/.Xauthority    -v `pwd`:/workspace 7fc9a8b440fc 


xarclock: 可以display了。 

但是存在GPU和OpenGL 的问题



有可能需要本地的OpenGL安装、

https://www.linuxidc.com/Linux/2017-03/141555.htm   

有效的东西： 

nvidia-docker run   --shm-size=8gb   -it    --net=host   -e DISPLAY=:10.0  -v $HOME/.Xauthority:/root/.Xauthority    -v `pwd`:/workspace 7fc9a8b440fc


sudo  nvidia-docker run   --shm-size=8gb   -it    --net=host   -e DISPLAY=:10.0  -v $HOME/.Xauthority:/root/.Xauthority    -v `pwd`:/workspace 7fc9a8b440fc

# 记住需要在本地安装Xming, xhost + 和安装相关的东西 

# 如果不是root用户可能adduser会有问题

向容器里面拷贝东西： 
sudo docker cp   data2/  4f12091a14e6:/DynamicFusionCore/

add user to group  渐渐 
https://blog.csdn.net/point0mine/article/details/79448402 

# Docker中容器的备份、恢复和迁移
https://blog.csdn.net/superdangbo/article/details/78688904

https://www.cnblogs.com/boshen-hzb/p/6373549.html 

# Docker容器和主机如何互相拷贝传输文件 
https://blog.csdn.net/u011596455/article/details/76862271

为ubuntu开启图形界面
https://blog.csdn.net/qq_34450601/article/details/78300701
https://blog.csdn.net/sunbaigui/article/details/6624110
https://www.cnblogs.com/boyzgw/p/6610139.html

# On Wei Server : 
c00464489@ubuntu-arvr04:~$ sudo apt-get install docker-ce
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
  aufs-tools cgroup-lite pigz
The following NEW packages will be installed:
  aufs-tools cgroup-lite docker-ce pigz
0 upgraded, 4 newly installed, 0 to remove and 3 not upgraded.
Need to get 39.8 MB/40.0 MB of archives.
After this operation, 201 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
WARNING: The following packages cannot be authenticated!
  docker-ce
Install these packages without verification? [y/N] y
0% [Working]
0% [Working]
0% [Working]

# Shame on WE

# 在docker中一切都很快解决，什么min的问题之类的 
可视化也完成了。 


