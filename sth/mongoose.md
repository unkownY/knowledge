# MONGOOSE

## 分页
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
## 模糊查询

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

## 位置查询

```node
    // 数据库定义时
    'gps':{type:[Number],index: '2d'}, // 地址经纬度 [longitude/经度,latitude/纬度]
    // 数据库查询 距离远近排序
    DBNAME.find({
        'gps':{$near:gps}
    })
```

## 去重查询

```node
    let oidArr = await DBNAME.distinct('oid');
```

## 聚合查询

```node
let data = await AlarmReport.aggregate([
    {$match: {'ip':{'$nin':['',null]}}}, // 条件查询
    {$group: {'_id': '$ip', count: {$sum: 1}}}, // 分组(以ip为键,统计个数)
    {$project: {'_id': 0, 'ip': '$_id', 'count': 1}}, // 返回值(显示ip,count)
    {$sort: {'count': -1}}, // 排序(按照count进行反向排序)
    {$limit:3}, // 截取个数
]);
```