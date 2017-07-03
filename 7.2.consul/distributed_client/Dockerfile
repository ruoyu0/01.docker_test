FROM ubuntu:14.04
MAINTAINER zhuyuan "849434163@qq.com"
ENV REFRESHED_AT 2017-07-01

# build command
# docker build -t "zhuyuan001/distributed_client" .

# ubuntu系统换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
RUN > /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list
RUN apt-get update

# ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc

# ubuntu 安装ruby, rubygem,
RUN apt-get install -y ruby ruby-dev build-essential

# ubuntu 换gem源
RUN gem sources -a https://ruby.taobao.org/
RUN gem sources -r http://rubygems.org/
RUN gem sources -u

RUN gem install --no-ri --no-rdoc json

RUN mkdir -p /opt/distributed_client
ADD client.rb /opt/distributed_client/

WORKDIR /opt/distributed_client

ENTRYPOINT [ "ruby", "/opt/distributed_client/client.rb" ]
CMD []
