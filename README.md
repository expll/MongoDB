# MongoDB Linux安装
下载地址：https://www.mongodb.com/try/download/community
```
wget下载后解压
# tar -zxvf xxoo.tgz
# mv mongodb-linux-x86_64-rhel70-6.0.6 /usr/local/mongodb
# ls /usr/local/mongodb

vim ~/.bashrc 
//添加
PATH=$PATH:/usr/local/mongodb/bin
//让~/.bashrc生效， 重启电脑后也是OK的
source ~/.bashrc
```

```
# 创建文件夹
# mkdir data log conf
```


### vim conf/mongod.conf
```
# 守护进程
processManagement:
   fork: true

# 配置端口
net:
   bindIp: 0.0.0.0
   port: 27017

# 数据存放位置
storage:
   dbPath: /usr/local/mongodb/data

# 系统日志存放位置
systemLog:
   destination: file
   path: "/usr/local/mongodb/log/mongod.log"
   logAppend: true

# 是否开启授权模式【如果是enabled那么你的一些操作需要登录之后才能使用】
security:
   authorization: enabled
   
```

### 启动： mongod -f conf/mongod.conf 

### 下载mongosh
```
https://www.mongodb.com/docs/mongodb-shell
卸载这个文件mongosh-1.9.1-linux-x64.tgz并且解压，然后将/bin下的
mongosh  mongosh_crypt_v1.so  拷贝到 
/usr/local/mongodb/bin
执行：
# mongosh
test>
```

### 自启动运行mongodb (mongodb-start.sh 需要运行权限)

```
vim /etc/init.d/mongodb-start.sh
写入以下内容
#!/bin/bash
# chkconfig: 2345 80 20
# description: MongoDB Start Service

### BEGIN INIT INFO
# Provides:          mongodb-start
# Required-Start:    $network $syslog
# Required-Stop:     $network $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: MongoDB Start Service
### END INIT INFO
/usr/local/mongodb/bin/mongod -f /usr/local/mongodb/conf/mongod.conf

(注释是必须的)

# chkconfig --add mongodb-start.sh
# chkconfig mongodb-start.sh on
```


# 关闭conf中验证
```
ps aux | grep mongo
kill
重启
mongod -f /usr/local/mongodb/conf/mongod.conf
```

# 查看用户情况
```
db.getUsers()
{ users: [], ok: 1 }
没有用户， 所以需要添加用户
admin> db.createUser({user: "root", pwd: "wanglei@123", roles: ["root"]})
{ ok: 1 }

```
既然有了一个用户了就可以开启conf中验证， 重启mongodb


# 如果是centos环境安装mongod-shell:
```
yum install mongodb-mongosh-shared-openssl11-1.10.1.x86_64.rpm
安装完成之后，在
/usr/bin/mongosh
```








