#### build command: docker build -t "zhuyuan001/tomcat7" .

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

#### 
RUN apt-get -y install tomcat7 default-jdk

ENV CATALINA_HOME /usr/share/tomcat7
ENV CATALINA_BASE /var/lib/tomcat7
ENV CATALINA_PID /var/run/tomcat7.pid
ENV CATALINA_SH /usr/share/tomcat7/bin/catalina.sh
ENV CATALINA_TMPDIR /tmp/tomcat7-tomcat7-tmp

RUN mkdir -p $CATALINA_TMPDIR

VOLUME [ "/var/lib/tomcat7/webapps/" ]

EXPOSE 8080

ENTRYPOINT [ "/usr/share/tomcat7/bin/catalina.sh", "run" ]
