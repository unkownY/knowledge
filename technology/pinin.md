# 汉字转拼音

## 安装

```js
    npm install pinyin
```

## 使用

```js
    // 汉字 : 你好
    console.log(
        pinyin('你好',{
            style:pinyin.STYLE_NORMAL
        }).join('')
    )
    // 拼音 : nihao

```

## 参数

* `.STYLE_NORMAL`
    普通风格，即不带声调。

    如：pin yin

* `.STYLE_TONE`
    声调风格，拼音声调在韵母第一个字母上。

    注：这是默认的风格。

    如：pīn yīn

* `.STYLE_TONE2`
    声调风格 2，即拼音声调以数字形式在各个拼音之后，用数字 [0-4] 进行表示。

    如：pin1 yin1

* `.STYLE_TO3NE`
    声调风格 3，即拼音声调以数字形式在注音字符之后，用数字 [0-4] 进行表示。

    如：pi1n yi1n

* `.STYLE_INITIALS`
    声母风格，只返回各个拼音的声母部分。对于没有声母的汉字，返回空白字符串。

    如：中国 的拼音 zh g

    注：声明风格会区分 zh 和 z，ch 和 c，sh 和 s。

    注意：部分汉字没有声母，如 啊，饿 等，另外 y, w, yu 都不是声母， 这些汉字的拼音声母风格会返回 ""。请仔细考虑你的需求是否应该使用首字母风格。 详情请参考 为什么没有 y, w, yu 几个声母

* `.STYLE_FIRST_LETTER`
    首字母风格，只返回拼音的首字母部分。

    如：p y