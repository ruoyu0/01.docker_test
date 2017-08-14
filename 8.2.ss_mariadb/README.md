### docker下运行mariadb:10.1.17

#### 拉去镜像
```
docker pull mariadb:10.1.17
```

#### 查看镜像构建历史
```
docker history --no-trunc --format "{{.CreatedBy}}" mariadb:10.1.17
```

#### 运行容器
```
docker run -p3306:3306 -v /mnt/data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root --net host --name mariadb10.1 mariadb:10.1.17
```

#### centos安装mysql客户端
```
yum install mysql
```

#### 连接mysql
```
mysql -h 127.0.0.1 -uroot -proot
```

#### mysqldump
```
# mysqldump -uroot -A > mysql_all.sql
# 备份部分数据库
mysqldump -uroot --databases alarms app_catalog cinder cisco_neutron conversions dbs dr ec2api entitlement events hot_upgrade keystone kubernetes lbaas metrics ml2_neutron nova ovs_neutron policy_store quotas statedb strato_kapacitor test > mysql_part.sql
```

#### mysqlrestore
```
# mysql -h 127.0.0.1 -uroot -proot <  mysql_all.sql
# 还原部分数据库
mysql -h 127.0.0.1 -uroot -proot <  mysql_part.sql
```
