#  node.js相关代码片段

1. 图片下载
    ```js
    const superagent = require('superagent');
    const fs = require('fs');
    const path = require('path');

    // 图片地址
    let API = '';

    // 请求图片数据
    let res = await superagent.get(API);

    if(!res) console.warn('Do not have response.');
    if(res.status>=400) console.warn(`Http code: ${res.status}.`);

    // 请求头
    let headers = res.headers;

    // 文件类型
    let fileType = headers['content-type'].split('/')[1];

    // 文件名称
    let fileName = `./OnePiece/${Date.now()}.${fileType}`;
    // 存储位置
    let destination = path.join(__dirname,fileName);

    fs.writeFileSync(destination,res.body);

    ```