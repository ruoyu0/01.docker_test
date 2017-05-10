#### 多容器的应用栈示例

######## node ########

#### 镜像构建

# redis基础镜像：
docker build -t zhuyuan001/redis .

# redis主镜像：
docker build -t zhuyuan001/redis_primary .

# redis副本镜像：
docker build -t zhuyuan001/redis_replica .

#### redis 后端集群

# express网络创建
docker network create express

# 运行redis主容器：
docker run -d -h redis_primary --name redis_primary --net express zhuyuan001/redis_primary

# 读取redis主容器日志：
docker run -i -t --rm --volumes-from redis_primary ubuntu:14.04 cat /var/log/redis/redis-server.log
# 或者
docker exec -i -t redis_primary tailf /var/log/redis/redis-server.log

# 运行第一个副本容器：
docker run -d -h redis_replica1 --name redis_replica1 --net express zhuyuan001/redis_replica

# 读取redis副本容器日志：
docker run -i -t --rm --volumes-from redis_replica1 ubuntu:14.04 cat /var/log/redis/redis-replica.log
# 或者
docker exec -i -t redis_replica1 tailf /var/log/redis/redis-replica.log

# 运行第二个副本容器：
docker run -d -h redis_replica2 --name redis_replica2 --net express zhuyuan001/redis_replica

# 读取redis副本容器日志：
docker run -i -t --rm --volumes-from redis_replica2 ubuntu:14.04 cat /var/log/redis/redis-replica.log
# 或者
docker exec -i -t redis_replica2 tailf /var/log/redis/redis-replica.log

#### 创建node容器
docker run -d --name nodeapp -p 3000:3000 --net express zhuyuan001/nodejs
