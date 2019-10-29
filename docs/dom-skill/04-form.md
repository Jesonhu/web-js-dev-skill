# 表单相关

## input 可输入位数限定

+ **onInput 中处理**

```html
<input type="number" oninput="if(value.length>11)value=value.slice(0,11)"/>
```