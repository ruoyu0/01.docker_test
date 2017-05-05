#### build command: docker build -t "zhuyuan001/jekyll" .

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

#### ruby安装
RUN apt-get -y install ruby2.0 ruby2.0-dev make nodejs

#### ubuntu 换gem源 gem2.0也会变成这个
# RUN gem sources -a https://ruby.taobao.org/
RUN gem sources -r http://rubygems.org/
# 使用https网址安装jekyll会有ssl证书问题，故先用http的方式
RUN gem sources -a http://gems.ruby-china.org/
RUN gem sources -u

#### gcc安装
RUN apt-get install -y gcc

#### jekyll安装
RUN gem2.0 install jekyll -v 2.5.3

VOLUME /data
VOLUME /var/www/html
WORKDIR /data

ENTRYPOINT [ "jekyll", "build", "--destination=/var/www/html" ]
