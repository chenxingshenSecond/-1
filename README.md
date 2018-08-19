https://mp.weixin.qq.com/s?__biz=MzI4MzAwNTQ3NQ==&mid=209866190&idx=1&sn=0ee75509eb2fab454009125e0a8c6437&scene=0#rd

docker run -d \
-v /etc/localtime:/etc/localtime:ro 
-v /tmp/.X11-unix:/tmp/.X11-unix 
-e DISPLAY=unix$DISPLAY 
-v $HOME/slides:/root/slides 
-e GDK_SCALE 
-e GDK_DPI_SCALE 
--name libreoffice 
jess/libreoffice

开启docker图形话界面时候的指令，主要是： nvidia-docker run --shm-size=8gb -it -v pwd:/workspace -e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix 1240803839cgw/cuda_caffe:latest 开机需要执行 xhost +

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
# 失败了 


# 实践2   
nvidia-docker run   --shm-size=8gb   -it    --net=host   -e DISPLAY=:10.0   -v $HOME/slides:/root/slides   -v $HOME/.Xauthority:/root/.Xauthority    -v `pwd`:/workspace 80f7d7e06019  

xarclock: 可以display了。 
但是存在GPU和OpenGL 的问题

有可能需要本地的OpenGL安装
https://www.linuxidc.com/Linux/2017-03/141555.htm
