# build command: docker build -t zhuyuan001/redis_replica .

# version 0.0.1
FROM zhuyuan001/redis
MAINTAINER zhuyuan "849434163@qq.com"

ENV REFRESHED_AT 2014-06-01

ENTRYPOINT [ "redis-server", "/etc/redis/redis.conf", "--logfile /var/log/redis/redis-replica.log", "--slaveof redis_primary 6379" ]

