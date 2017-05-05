#### build command: docker build -t "zhuyuan001/docker-jenkins" .

#### version 0.0.1
FROM ubuntu:14.04
MAINTAINER zhuyuan "849434163@qq.com"

#### ubuntu14.04系统换阿里源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
COPY sources.list /etc/apt/sources.list 
# 需要sources.list文件
RUN apt-get update

#### ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc
RUN . ~/.bashrc

#### ubuntu常用工具安装
RUN apt-get install -y man
RUN apt-get install -y tree
RUN apt-get install -y curl 
RUN apt-get install -y wget
RUN apt-get install -y iptables 
RUN apt-get install -y git-core 

#### ubuntu安装docker
RUN apt-get install -y apt-transport-https ca-certificates 
RUN curl -fsSL https://yum.dockerproject.org/gpg | sudo apt-key add -
RUN apt-key fingerprint 58118E89F3A912897C070ADBF76221572C52609D
COPY docker-engine_17.04.0~ce-0~ubuntu-trusty_amd64.deb /usr/local/src/
# 下载地址: https://apt.dockerproject.org/repo/pool/main/d/docker-engine/docker-engine_17.04.0~ce-0~ubuntu-trusty_amd64.deb
RUN apt-get install -y libsystemd-journal0 libapparmor1 libltdl7
RUN dpkg -i /usr/local/src/docker-engine_17.04.0~ce-0~ubuntu-trusty_amd64.deb
RUN rm -vrf /usr/local/src/docker-engine_17.04.0~ce-0~ubuntu-trusty_amd64.deb

#### docker换国内镜像源
RUN curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://f084c6e1.m.daocloud.io
RUN restart docker

#### ubuntu jenkins安装
RUN apt-get update
RUN apt-get install -y libicu52
RUN apt-get install -y openjdk-7-jdk
ENV JENKINS_HOME /opt/jenkins/data
ENV JENKINS_MIRROR http://mirrors.jenkins-ci.org
RUN mkdir -vp $JENKINS_HOME/plugins
# 下载命令: RUN curl -sf -o /opt/jenkins/jenkins.war -L $JENKINS_MIRROR/war-stable/latest/jenkins.war
COPY jenkins.war /opt/jenkins/jenkins.war
RUN for plugin in chucknorris greenballs scm-api git-client git ws-cleanup ; \
    do \
        echo "curl -sf -o $JENKINS_HOME/plugins/${plugin}.hpi -L $JENKINS_MIRROR/plugins/${plugin}/latest/${plugin}.hpi"; \
        curl -sf -o $JENKINS_HOME/plugins/${plugin}.hpi -L $JENKINS_MIRROR/plugins/${plugin}/latest/${plugin}.hpi ; \
    done
# ADD .dockerjenkins.sh /usr/local/bin/dockerjenkins.sh
RUN wget https://raw.githubusercontent.com/jamtur01/dockerbook-code/master/code/5/jenkins/dockerjenkins.sh
RUN mv dockerjenkins.sh /usr/local/bin
RUN chmod 0755 /usr/local/bin/dockerjenkins.sh

VOLUME /var/lib/docker
EXPOSE 8080
ENTRYPOINT [ "/usr/local/bin/dockerjenkins.sh" ]

