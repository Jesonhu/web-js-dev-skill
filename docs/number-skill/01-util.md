# 数字处理

## 百分比

```js
/**
 * 格式为`百分比方式显示` 
 * 
 * @param {number} molecular 分子 `横线`上面的数
 * @param {number} denominator 分母
 * @return {string} 百分比结果
 * @see [百度百科-分数](https://baike.baidu.com/item/%E5%88%86%E6%95%B0/2067623?fr=aladdin)
 * @see [a](http://www.css88.com/archives/7340)
 */
function getPercentNumber(molecular, denominator) {
  return `${parseInt(String(molecular / denominator * 100))}%`;
}
```

结果输出

```js
输入: getPercentNumber(3, 5)
输出：60%

输入: getPercentNumber('3', '5')
输出：60%

输入: getPercentNumber(3, '5')
输出：60%
```

+ **方法2**

```js
function getPercent(num) {
  return num * 100 | 0;
}
```

```js
输入: getPercentNumber(0.1)
输入: getPercentNumber('0.1')
输出：10

输入: getPercentNumber(0.1311)
输出：13

输入: getPercentNumber(1)
输出：100
```

## 随机数

+ 方式1: **指定区间的随机数**

```js
function randomNum(start, end) {
  return Math.round( Math.random() * (end - start) + start );
}
```

```
输入: randomNum(3, 9)
输出: 3 ~ 9 之间的整数，包括 3 和 9
```