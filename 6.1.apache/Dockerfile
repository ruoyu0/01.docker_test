#### build command: docker build -t "zhuyuan001/apache" .

#### version 0.1.0
FROM ubuntu:14.04
MAINTAINER zhuyuan "849434163@qq.com"
ENV REFRESHED_AT 2014-06-01

#### ubuntu14.04系统换阿里源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
COPY sources.list /etc/apt/sources.list 
# 需要sources.list文件
RUN apt-get update

#### ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc
RUN . ~/.bashrc

#### apache安装
RUN apt-get -y install apache2

VOLUME [ "/var/www/html" ]
WORKDIR /var/www/html

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

RUN mkdir -vp $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

EXPOSE 80

ENTRYPOINT [ "/usr/sbin/apache2" ]
CMD [ "-D", "FOREGROUND" ]
