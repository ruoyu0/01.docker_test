FROM debian:jessie
MAINTAINER zhuyuan "849434163@qq.com"
ENV REFRESHED_AT 2016-06-01

# ubuntu系统换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak 
RUN > /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list
RUN apt-get update

# ubuntu修改PS1变量
RUN echo 'export PS1="\[\e[37;1m\][\[\e[36;1m\]\u\[\e[37m\]@\[\e[36m\]\h \[\e[33m\]\W\[\e[37m\]]\[\e[36m\]$\[\e[m\]"' >> /root/.bashrc
RUN . ~/.bashrc

RUN apt-get -y --force-yes install ruby rake

# ubuntu换gem源
RUN gem sources -a https://ruby.taobao.org/
RUN gem sources -r http://rubygems.org/
RUN gem sources -u

RUN gem install --no-rdoc --no-ri rspec ci_reporter_rspec
