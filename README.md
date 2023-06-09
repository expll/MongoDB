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
   bindIp: localhost
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

