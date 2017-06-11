#### project address
https://docs.docker.com/compose/django/#define-the-project-components

# 拉取postgres image
docker pusll postgres

# 写好docker-compose.yml后，创建一个Django project
docker-compose run web django-admin.py startproject composeexample .
# 运行完之后，会发现当前目录建立一个composeexample的Django工程，因为我们把当前目录做为volume挂载进去了

# 修改composeexample的Django项目中的数据库配置文件

# 使用docker-compose启动服务
docker-compose up

# 访问web项目
curl localhost:8000

# 停止服务
docker-compose stop 

# 删除服务容器
docker-compose rm

# 也可以一条命令搞定，停止服务和删除服务容器
docker-compose down
