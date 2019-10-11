# node

# npm

## npm源 管理

### 安装

```shell
    npm install -g nrm
```

### 列出可用源(带星号是当前选中源)
```shell
    npm ls
    ---
    npm ---- https://registry.npmjs.org/
    cnpm --- http://r.cnpmjs.org/
  * taobao - https://registry.npm.taobao.org/
    nj ----- https://registry.nodejitsu.com/
    npmMirror  https://skimdb.npmjs.com/registry/
    edunpm - http://registry.enpmjs.org/
```

### 更换源
```
    nrm use cnpm
    ---
    Registry has been set to: http://r.cnpmjs.org/
```

### 增加源
```
    nrm add <registry> <url> [home]
```

### 删除源
```
    nrm del <registry>
```

### 测试速度
```js
    nrm test npm
    // nrm test 测试所有源
    ---
    * taobao - 475ms
```
