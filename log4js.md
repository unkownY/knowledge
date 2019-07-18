# log4js

> 在 `Express` 中 使用 `log4js` 进行日志记录 

## 配置及使用

```javascript
const log4js = require('log4js');
//log4js 配置
log4js.configure({
    appenders:{
        aboveWarning:{
            type:'file',
            filename:`${LOGPATH}/${new Date().getFullYear()}-${new Date().getMonth()+1}-${new Date().getDate()}.log`,
            maxLogSize:5000000,
            keepFileExt:true,
            layout:{
                type:'pattern',
                pattern:'--TIME: %d --LEVEL: %p --HOST: %h %m %n',
            },
        },
        console:{
            type:'console',
        },
    },
    categories:{
        aboveWarning:{
            appenders:['aboveWarning'],
            level:'warn',
        },
        default:{
            appenders:['console'],
            level:'all',
        },
    },
});

app.use(log4js.connectLogger(log4js.getLogger('aboveWarning'),{
    format:'--ETIME: :response-time --IP: :remote-addr --METHOD: :method --URL: :url --STATUS: :status --UA: :user-agent --REFERRER: :referrer --LEN: :content-length',
    nolog:''
}));
```
