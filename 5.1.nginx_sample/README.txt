使用Docker测试静态网站, 由nginx运行

# 常用命令：

# 构建镜像
docker build -t "zhuyuan001/nginx" . 

# 运行容器
docker run -d -p 80 --name web_site -v $PWD/website:/var/www/html/website zhuyuan001/nginx nginx

# 进入容器内部
docker exec -i -t web_site /bin/bash

# 查看容器端口映射情况
docker port web_site

# 查看容器ip地址
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web_site
或者
docker exec -i web_site "ifconfig" |grep "inet addr"

