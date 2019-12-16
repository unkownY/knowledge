# [redis](https://redis.io/)

## 安装
1. 第一种
```
sudo apt-get install redis-server
```
2. 第二种
    * 安装依赖
    ```
    sudo apt-get install build-essential -y
    ```
    * 下载编译
    ```
    wget wget http://download.redis.io/releases/redis-5.0.7.tar.gz
    tar xzf redis-5.0.7.tar.gz
    cd redis-5.0.7
    make 
    sudo make install
    ```
    * 修改 配置文件
    ```
    daemonize yes
    logfile /var/log/redis/redis-server.log
    dir /var/lib/redis
    ```
    * 拷贝配置文件
    ```
    sudo mkdir /etc/redis
    sudo cp redis.conf /etc/redis/6379.conf
    ```
    * 拷贝服务脚本
    ```
    sudo cp utils/redis_init_script /etc/init.d/redisd
    ```
    * 创建需求文件夹
    ```
    sudo mkdir /var/log/redis
    sudo mkdir /var/lib/redis
    ```
    * 服务脚本授权
    ```
    sudo chmod +x /etc/init.d/redisd
    ```
    * 创建服务
    ```
    cd /etc/init.d/
    sudo update-rc.d redisd defaults
    sudo /etc/init.d/redisd start
    ```



## redis 设置验证

```redis
config get requirepass          # 查看密码设置情况
config set requirepass passwd   # 设置密码
auth passwd                     # 输入密码进行授权
```

## 使用

* `Nodejs` : [ioredis](https://github.com/luin/ioredis)

