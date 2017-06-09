
# 拉取python:2.7 images
docker pull python:2.7

# 构建composeapp应用
docker build -t zhuyuan001/composeapp .

# 拉取redis镜像
docker pull redis

##########
# 与yml文件同样效果的docker run命令
docker run -d --name redis redis
docker run -d -p 5000:5000 --link redis:redis --name compose_web zhuyuan001/composeapp python app.py

# 查看compose_web容器中的log信息
docker logs -f compose_web

# 查看redis容器中redis数据库中指定key的值
docker exec -i redis redis-cli get hits

# 停止和删除compose_web和redis容器
docker stop compose_web redis
docker rm compose_web redis

##########
# 使用docker-compose up命令启动示例应用服务, 可以看到log随后输出
docker-compose up

# 也可以使用-d参数，以守护进程的模式来运行服务
docker-compose up -d

# 查看docker-compose 可带参数的详细介绍
docker-compose help build

# 停止docker-compose 运行的两容器
docker-compose stop

# 删除docker-compose 创建的两容器
docker-compose rm
