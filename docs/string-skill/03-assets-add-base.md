# 资源添加基础域

> 在使用后台传过来的富文本或资源数组的时候有时候需要添加基础域，当前文档就是这种情况的解决方案

## 富文本字符串

```js
/**
 * 图片添加基础域.
 * 
 * @params {string} str 操作的字符串
 * @params {string} baseUrl 基础域
 */
function assetsAddBaseUrl(str, baseUrl) {
  return str.replace(/<img [^>]*src=['"]([^'"]+)[^>]*>/gi, `<img src="${baseUrl}$1" />`);
}
```

以上函数的结果如下所示

```js
// 结果
const str1 = '<img src="/aa.png" /><span>1</span><img src="/aa.png" /><span>1</span><img src="/aa.png" />';

const str2 = assetsAddBaseUrl(str1, 'http://www.baidu.com');

输入: assetsAddBaseUrl(str1, 'http://www.baidu.com/');
输出: "<img src="http://www.baidu.com/aa.png" /><span>1</span><img src="http://www.baidu.com/aa.png" /><span>1</span><img src="http://www.baidu.com/aa.png" />"
```

## 资源数组

```js
/**
 * 资源批量添加基础域.
 *
 * @param {array} sourceArr 来源数据
 * @param {string} key 需要添加域的属性值.
 * @param {string} baseUrl 基于域
 */
function assetsAddBaseUrl(sourceArr, key, baseUrl) {
  // 无数据.
  if (sourceArr.length === 0) {
    return sourceArr;
  };

  // 有数据.
  sourceArr.forEach((item) => {
    item[key] = `${baseUrl}${item[key]}`
  });

  return sourceArr
}
```
