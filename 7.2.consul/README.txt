# 构建consul镜像
docker build -t "zhuyuan001/consul" .

# 运行consul容器，开始测试
docker run -p 8500:8500 -p 53:53/udp -h node1 --name consul zhuyuan001/consul -server -bootstrap

# 使用浏览器访问web界面，chrome访问不了web界面，360浏览器可以
