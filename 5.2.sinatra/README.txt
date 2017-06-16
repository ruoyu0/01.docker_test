######## sinatra.sh ########

# 构建新的sinatra镜像
docker build -t zhuyuan001/sinatra .

# 下载sinatra web应用程序
wget --cut-dirs=3 -nH -r --reject Dockerfile, index.html --no-parent http://dockerbook.com/code/5/sinatra/webapp/

# 确保webapp/bin/webapp可以执行
chmod +x webapp/bin/webapp

#### 启动第一个sinatra容器
docker run -d -p 4567 --name webapp -v $PWD/webapp:/opt/webapp zhuyuan001/sinatra

# 检查sinatra容器的日志
docker logs webapp

# 跟踪sinatra容器的日志：
docker logs -f webapp

# 使用docker top来列出sinatra容器进程
docker top webapp

# 检查sinatra映射端口
docker port webapp 4567

#### 将sinatra应用程序连接到Redis容器

# 创建新的Docker网络
docker network create app

# 查看app网络信息
docker network inspect app

# 构建redis镜像
docker build -t "zhuyuan001/redis" .

# 运行redis容器
docker run -d --net=app --name db zhuyuan001/redis

# 构建webapp_redis镜像
docker build -t "zhuyuan001/webapp_redis" .

# 交互式运行容器, 看能否访问redis容器
docker  run -p 4567 --net=app --name webapp_redis -t -i -v $PWD/webapp:/opt/webapp zhuyuan001/webapp_redis /bin/bash

# ping redis容器, 这里是可以直接ping通的
ping db

# 连接redis容器中的redis服务
redis-cli -h db

# 运行webapp_redis容器, 提供服务, (注意：在webapp_redis目录下运行)
docker  run -d -p 4567 --net=app --name webapp_redis -t -i -v $PWD/:/opt/webapp zhuyuan001/webapp_redis

# curl测试,写入数据，读取数据,(端口可能不一致)
curl -i -H 'Accept: application/json' -d 'name=Foo&status=Bar' http://localhost:32770/json
curl -i http://localhost:32770/json

