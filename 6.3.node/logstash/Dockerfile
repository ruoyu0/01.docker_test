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

RUN apt-get -qq install wget
RUN wget -O - http://packages.elasticsearch.org/GPG-KEY-elasticsearch |  apt-key add -
RUN echo 'deb http://packages.elasticsearch.org/logstash/1.5/debian stable main' > /etc/apt/sources.list.d/logstash.list
RUN apt-get -qq update
RUN apt-get -qq install logstash default-jdk

ADD logstash.conf /etc/

WORKDIR /opt/logstash

ENTRYPOINT [ "bin/logstash" ]
CMD [ "--config=/etc/logstash.conf" ]
