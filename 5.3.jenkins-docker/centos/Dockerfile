FROM centos:latest
MAINTAINER zhuyuan "849434163@qq.com"
ENV REFRESHED_AT 2016-06-01
RUN yum -y install ruby rubygems rubygem-rake

# ubuntu换gem源
RUN gem sources -a https://ruby.taobao.org/
RUN gem sources -r http://rubygems.org/
RUN gem sources -u

RUN gem install --no-rdoc --no-ri rspec ci_reporter_rspec
