# 构建consul镜像
docker build -f ./Dockerfile_0.3.1 -t "zhuyuan001/consul03" .
docker build -f ./Dockerfile_0.8.4 -t "zhuyuan001/consul" .

# 运行consul容器，开始测试
docker run -p 8500:8500 -p 53:53/udp -h node1 --name consul zhuyuan001/consul03 -server -bootstrap
#### -server：告诉代理服务器运行子啊服务器模式
#### -bootstrap:

# 使用浏览器访问web界面，其中chrome访问不了web界面，360浏览器可以

# PUBLIC_IP赋值
PUBLIC_IP=`ifconfig eth0 |grep "inet addr" |awk -F ' ' '{print $2}' |awk -F':' '{print $2}'`

# JOIN_IP赋值
# JOIN_IP=192.168.11.4

# docker 配置文件修改
DOCKER_OPTS="--dns 172.17.42.1 --dns 8.8.8.8 --dns-search service.consul"

# 重启dockre守护进程
sudo service docker restart

# 启动具有自启动功能的consul节点
docker stop `docker ps -lq`
docker rm `docker ps -lq`
docker run -h $HOSTNAME -p 8300:8300 -p 8301:8301 -p 8301:8301/udp \
-p 8302:8302 -p 8302:8302/udp -p 8400:8400 -p 8500:8500 -p 53:53/udp \
--name larry_agent zhuyuan001/consul -server -bootstrap-expect=3 -advertise=192.168.11.4
#### -expect：告诉Consul集群有多少代理。

# 查看ip地址
docker exec -i larry_agent ifconfig

# 启动剩下的curly_agent节点
docker stop `docker ps -lq`
docker rm `docker ps -lq`
docker run -h $HOSTNAME -p 8300:8300 -p 8301:8301 -p 8301:8301/udp \
-p 8302:8302 -p 8302:8302/udp -p 8400:8400 -p 8500:8500 -p 53:53/udp \
--name curly_agent zhuyuan001/consul -server -join=192.168.11.4 -advertise=192.168.11.5

# 启动剩下的moe_agent节点
docker stop `docker ps -lq`
docker rm `docker ps -lq`
docker run -h $HOSTNAME -p 8300:8300 -p 8301:8301 -p 8301:8301/udp \
-p 8302:8302 -p 8302:8302/udp -p 8400:8400 -p 8500:8500 -p 53:53/udp \
--name moe_agent zhuyuan001/consul -server -join=192.168.11.4 -advertise=192.168.11.6
