# [redis](https://redis.io/)

## 安装
```js
sudo apt-get install redis-server
```

## redis 设置验证

```redis
config get requirepass          # 查看密码设置情况
config set requirepass passwd   # 设置密码
auth passwd                     # 输入密码进行授权
```

## 使用

* `Nodejs` : [ioredis](https://github.com/luin/ioredis)

