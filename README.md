vemoji是一个基于vue框架的emoji键盘组件 方便用户输入emoji表情

## npm

https://www.npmjs.com/package/v-emoji

## 用法

### cdn引用
```html
  <script src="https://cdn.jsdelivr.net/npm//v-emoji/dist/v-emoji.min.js"></script>

```
### 单文件引用
```js
npm i v-emoji -S
```
```js
import VEmoji from "v-emoji";

export default {
 components: {
    "v-emoji": VEmoji,
  },
}

```

## 示例

![示例](https://raw.githubusercontent.com/wlor0623/v-emoji/main/example/Snipaste_2021-03-31_17-49-52.png)


## 更新记录
- 2021-04-07 适配暗黑模式
