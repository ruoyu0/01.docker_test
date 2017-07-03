# version 0.0.1
FROM ubuntu:14.04
MAINTAINER zhuyuan "849434163@qq.com"
ENV REFRESHED_AT 2017-07-01

# build command
# docker build -t "zhuyuan001/distributed_app" .

# ubuntu系统换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
RUN > /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list
RUN apt-get update

# ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc

# ubuntu 安装ruby, git
RUN apt-get install -y ruby-dev git libcurl4-openssl-dev curl build-essential python
RUN apt-get install -y ruby

# ubuntu 换gem源
# RUN gem sources -a https://ruby.taobao.org/
# RUN gem sources -r http://rubygems.org/
# RUN gem sources -u
RUN gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
RUN gem sources -l

# RUN apt-get install -y python-pip
# RUN pip install -i http://pypi.douban.com/simple uwsgi

# ubuntu 通过gem安装sinatra, json, redis
RUN gem install --no-rdoc --no-ri sinatra uwsgi

RUN uwsgi --build-plugin https://github.com/unbit/uwsgi-consul

ADD uwsgi-consul.ini /opt/distributed_app/
ADD config.ru /opt/distributed_app/

ADD uwsgi-consul.ini /opt/distributed_app/
ADD config.ru /opt/distributed_app/


ENTRYPOINT [ "uwsgi", "--ini", "uwsgi-consul.ini", "--ini", "uwsgi-consul.ini:server1", "--ini", "uwsgi-consul.ini:server2"  ]
CMD []
