# version 0.0.1
FROM ubuntu:14.04
MAINTAINER zhuyuan "849434163@qq.com"

# build command
# docker build -t "zhuyuan001/sinatra" .

# ubuntu系统换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
RUN > /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list
RUN apt-get update

# ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc
RUN . ~/.bashrc

# ubuntu 安装ruby, rubygem,
RUN apt-get install -y ruby ruby-dev build-essential redis-tools

# ubuntu 换gem源
RUN gem sources -a https://ruby.taobao.org/
RUN gem sources -r http://rubygems.org/
RUN gem sources -u

# ubuntu 通过gem安装sinatra, json, redis
RUN gem install --no-rdoc --no-ri sinatra json redis

RUN mkdir -p /opt/webapp
EXPOSE 4567

CMD ["/opt/webapp/bin/webapp"]
