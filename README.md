# zxprompt

> prompt 弹出组件

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```
## 使用方法
``` bash
 import zxprompt from 'zxprompt'
 <zxprompt promptShow></zxprompt>
```

## 说明

字段|类型|默认值|含义
---|:--:|---:|---:
promptTitle|String|提示|提示框头部
sure|String|确认|确认按钮文字
content|String|哎呀，报错了！|提示内容
cancle|String|取消|取消按钮文字
promptShow|Boolean|false|控制弹出显示隐藏
confirm|Boolean|false|是否开起comfirm