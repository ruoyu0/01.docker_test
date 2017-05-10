######## sinatra.sh ########

# 构建新的sinatra镜像
docker build -t zhuyuan001/sinatra .

# 下载sinatra web应用程序
wget --cut-dirs=3 -nH -r --reject Dockerfile, index.html --no-parent http://dockerbook.com/code/5/sinatra/webapp/

# 确保webapp/bin/webapp可以执行
chmod +x webapp/bin/webapp

# 启动第一个sinatra容器
docker run -d -p 4567 --name webapp -v $PWD/webapp:/opt/webapp zhuyuan001/sinatra

# 检查sinatra容器的日志
docker logs webapp

# 跟踪sinatra容器的日志：
docker logs -f webapp

# 使用docker top来列出sinatra容器进程
docker top webapp

# 检查sinatra映射端口
docker port webapp 4567
