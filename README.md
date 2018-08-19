# -1
https://mp.weixin.qq.com/s?__biz=MzI4MzAwNTQ3NQ==&mid=209866190&idx=1&sn=0ee75509eb2fab454009125e0a8c6437&scene=0#rd


docker run -d \
  -v /etc/localtime:/etc/localtime:ro \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -e DISPLAY=unix$DISPLAY \
  -v $HOME/slides:/root/slides \
  -e GDK_SCALE \
  -e GDK_DPI_SCALE \
  --name libreoffice \
  jess/libreoffice
  
  
  
