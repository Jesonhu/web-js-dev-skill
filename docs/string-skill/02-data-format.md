# 日期格式化

> 日期各种格式化处理.

## meizz 版本

```js
Date.prototype.Format = function(fmt) { //author: meizz 
  var o = {
      "M+": this.getMonth() + 1, //月份 
      "d+": this.getDate(), //日 
      "h+": this.getHours(), //小时 
      "m+": this.getMinutes(), //分 
      "s+": this.getSeconds(), //秒 
      "q+": Math.floor((this.getMonth() + 3) / 3), //季度 
      "S": this.getMilliseconds() //毫秒 
  };
  if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1
      .length));
  for (var k in o)
      if (new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[
          k]) : (("00" + o[k]).substr(("" + o[k]).length)));
  return fmt;
}
```

食用方式

```js
输入：new Date().Format('MM-dd hh:mm:ss:S')
输出："09-17 17:41:12:892"
```

PS: 这种方式未对 `年份` 进行处理.


## 使用 moment.js 库

## 参考资料

+ [tinydate-轻量级, 快速日期格式化](https://github.com/lukeed/tinydate#patterns)