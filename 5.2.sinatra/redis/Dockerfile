# version 0.0.1
FROM ubuntu:14.04
MAINTAINER zhuyuan "849434163@qq.com"

# build command
# docker build -t "zhuyuan001/redis" .

# ubuntu系统换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
RUN > /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list
RUN apt-get update

# ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc
RUN . ~/.bashrc

# ubuntu安装redis
RUN apt-get install -y redis-server redis-tools
EXPOSE 6379

ENTRYPOINT [ "/usr/bin/redis-server" ]
CMD []
