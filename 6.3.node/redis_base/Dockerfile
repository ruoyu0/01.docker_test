# build command: docker build -t zhuyuan001/redis .

# version 0.0.1
FROM ubuntu:14.04
MAINTAINER zhuyuan "849434163@qq.com"

#### ubuntu系统换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
RUN > /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list
RUN apt-get update

# ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc
RUN . ~/.bashrc

#### 添加ppa库，安装最新的redis(这里是3.2.8版本)
RUN apt-get install -qq software-properties-common python-software-properties
RUN add-apt-repository ppa:chris-lea/redis-server
RUN apt-get -qq update

RUN apt-get -qq install redis-server redis-tools

#### 修改redis配置文件

# 绑定的ip更改(把bind127.0.0.1注释掉)
RUN sed -i 's/bind 127.0.0.1$/# bind 127.0.0.1/' /etc/redis/redis.conf
# 改为非守护进程的方式运行redis
RUN sed -i 's/daemonize yes/daemonize no/' /etc/redis/redis.conf
# 关闭保护模式
RUN sed -i 's/protected-mode yes/protected-mode no/' /etc/redis/redis.conf

VOLUME [ "/var/lib/redis", "/var/log/redis" ]

EXPOSE 6379

CMD []
