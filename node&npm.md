# 有关于 Node.js 和 NPM 一些东西

## express

* 获取 `ip` 地址
    * 正常: `req.ip`
    * 使用 nginx 进行了反向代理
        1. 设置`niginx`,下面两个这个
            ```node
                proxy_pass http://127.0.0.1:5555
                proxy_set_header Host $http_host;
                proxy_set_header X-Real-IP $remote_addr; // 这个
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; // 这个
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
            ```
        1. 后端自定义函数
            ```node
                exports.ip = req => {
                    return req.headers['x-forwarded-for'] ||
                    req.ip ||
                    req._remoteAddress ||
                    (req.socket &&
                        (req.socket.remoteAddress ||
                        (req.socket.socket && req.socket.socket.remoteAddress)
                        )
                    );
                };
            ```
        1. ip 获取 complete.

## mongodb / mongoose

* **常用:**

```node
    // limit+skip = 分页
    DBNAME
        .find({})   // 查询数据
        .sort()     // 排序
        .limit()    // 返回数据个数
        .skip()     // 跳过数据个数
        .countDocument()    // 查找到的数据个数(mongoose)
        .count()    // 查找到的数据个数(mongodb)
```

* **模糊查询:** 

```node
    // 构建正则 => keyword是查询的词
    let rex = new RegExp(keyword,'i');
    // 数据库搜索
    DBNAME.find({
        $or:[
            {'title': {$regex: rex}}, // 搜索 title 字段
            {'nickname': {$regex: rex}}, // 搜索 nickname 字段
        ]
    })
```

* **位置查询:**

```node
    // 数据库定义时
    'gps':{type:[Number],index: '2d'}, // 地址经纬度 [longitude/经度,latitude/纬度]
    // 数据库查询 距离远近排序
    DBNAME.find({
        'gps':{$near:gps}
    })
```
