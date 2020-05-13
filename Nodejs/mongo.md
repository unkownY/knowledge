# mongodb

## 创建新用户

```
db.createUser({
    user: 'admin',
    pwd: '_nJ*m?g5TK&(UF3S',
    roles: [{
        role: 'root', 
        db: 'admin',
    }]
})
```
## 用户权限(role)
 * ` Read `：允许用户读取指定数据库
 * ` readWrite `：允许用户读写指定数据库
 * ` dbAdmin `：允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问system.profile
 * ` userAdmin `：允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
 * ` clusterAdmin `：只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。
 * ` readAnyDatabase `：只在admin数据库中可用，赋予用户所有数据库的读权限
 * ` readWriteAnyDatabase `：只在admin数据库中可用，赋予用户所有数据库的读写权限
 * ` userAdminAnyDatabase `：只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
 * ` dbAdminAnyDatabase `：只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。
 * ` root `：只在admin数据库中可用。超级账号，超级权限
 
## 导入/导出数据
 * 导出
    ```
    mongoexport 
        --db <dbname> 
        --collection <collection name>  
        --authenticationDatabase <dbname> 
        --username <user> 
        --password <password> 
        --out filname.json
    ```
 * 导入
    ```
    mongoimport 
        --db <bdname> 
        --collection <collection name> 
        --authenticationDatabase <dbname> 
        --username <user> 
        --password <password> 
        --drop 
        --jsonArray filename.json
    ```
    
## 代码相关

  ### 基本数据类型

EN|CH
---|---
String|字符串
Integer|整型
Boolean|布尔
Double|双精度浮点
Array|数组
Min/max keys|与BSON对比最小/大
Timestamp|时间戳
Object|对象(用于内嵌文档)
Null|创建空值
Symbol|符号(用于特殊字符串符号)
Date|日期时间
Object ID|对象ID (用于创建文档的ID)
Binary Data|二进制数据
Code| 代码(用于存储JS代码)
Regular expression|正则表达式

### 操作符

操作|名称
---|---
等于|%eq
不相等|$ne
大于|$gt
大于等于|$gte
小于|$lt
小于等于|$lte
在数组中|$in
不在数组中|$nin
判断类型|$type
判断是否存在|$exists
$and|例:$and:[{l:1},{k:1}]
$not|例:$not:/^[a-z]$/
$nor|例:$nor:[{l:1},{k:1}]
$or|例:$or:[{l:1},{k:1}]

### 安装

#### [Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)

1. Import the public key used by the package management system 
    * `wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add - `
1. Create a list file for MongoDB.
    * Ubuntu 16.04 (Xenial): `echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list`
    * Ubuntu 18.04 (Bionic): `echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list`
1. Reload local package database
    * `sudo apt-get update`
1. Install the MongoDB packages.
    * the latest version: `sudo apt-get install -y mongodb-org`
    * specific release: `sudo apt-get install -y mongodb-org=4.2.0 mongodb-org-server=4.2.0 mongodb-org-shell=4.2.0 mongodb-org-mongos=4.2.0 mongodb-org-tools=4.2.0`
1. Some Operation:
    * Start : `sudo service mongod start`
    * Stop : `sudo service mongod stop`
    * Restart : `sudo service mongod restart`
    * using : `mongo`
1. File Default Location:
    * logs: `/var/log/mongodb/mongod.log`
    * config: `/etc/mongod.conf`
    * bin: `/usr/bin/mongod`