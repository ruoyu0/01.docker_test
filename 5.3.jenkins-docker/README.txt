######## docker 用于持续集成 ########

# 构建包含jenkins和Docker的镜像
docker build -t zhuyuan001/docker-jenkins .

# 运行docker-jenkins容器
docker run -p 8080:8080 --name docker-jenkins --privileged -d zhuyuan001/docker-jenkins

# 检查docker-jenkins容器的日志
docker logs jenkins

# 
