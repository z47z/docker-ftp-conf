# 测试协议：ftp

# 拉取镜像

docker pull million12/vsftpd

# 启动

docker run \
  --name vsftpd \
  -v ./vsftpc.log:/var/log/vsftpd/vsftpd.log \
  -v ./afl-qemu-trace:/usr/sbin/afl-qemu-trace \
  -v ./wfuzz-cov-run:/usr/sbin/wfuzz-cov-run  \
  -v ./bootest.sh:/bootstrap.sh  \
  --privileged=true \
  -it \
  -d \
  -e FTP_USER=joe\
  -e FTP_PASS=mypwd \
  -e ANONYMOUS_ACCESS=true \
  -p 20-21:20-21 \
  -p 21100-21110:21100-21110 \
  -p 19240:19240 \
  million12/vsftpd

# wingfuzz中参数填写

主机名：127.0.0.1
端口：21
ftp用户名：joe
ftp密码：mypwd