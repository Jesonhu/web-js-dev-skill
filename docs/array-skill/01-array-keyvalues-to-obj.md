# 数组(keyValues)转换为对象

```js
input = [
  {
    key: 'key1',
    value: 'value1' 
  },
  {
    key: 'key2',
    value: 'value2'  
  }
]

output = { key1: 'value1', key2: 'value2' }

输入：input
输出：output

```

|名称|说明|
|--|--|
|方法1|代码易于理解|
|方法2|代码风格风骚:解构、`1,2,3`方式|

<details>
  <summary>方法1</summary>

```js
 const keyValues = [
    {
      key: 'key1',
      value: 'value1'
    },
    {
      key: 'key2',
      value: 'value2'
    }
 ] 

function transform(total, currentValue) {
    const key = (currentValue && currentValue.key) || '';
    const value = (currentValue && currentValue.value) || '';
    let formatObj = {};
    if (key && value) {
        formatObj[key] = value;
    }
    return Object.assign({}, total, formatObj);
}

const arr2obj = (arr) => {
  return arr.reduce(transform, {})
}
const result = arr2obj(keyValues);
console.log('result', result);

```

</details>

[在线示例](https://codepen.io/Jesonhu/pen/wvwoJmQ)
    
<details>
  <summary>方法2</summary>

```js
const keyValues = [
  {
    key: 'key1',
    value: 'value1'
  },
  {
    key: 'key2',
    value: 'value2'
  }
]

function transform(total, currentValue) {
  const { key, value } = currentValue;
  total[key] = value;
  return total;
}

const arr2obj = (arr) => {
  return arr.reduce(transform, {})
}
const result = arr2obj(keyValues);
console.log('result', result);


// 补充点1: 如果返回 a,b,c,d 真正返回的是什么？
// 返回: 1,2,3,4 结果：4
// 返回：{x: 1}, { x: 2 }, {x: 3}, {x: 4} 结果: {x: 4}

// 代码更精简方式
const arr2obj2 = (arr) => arr.reduce((total, { key, value }) => (total[key] = value, total), {});
const result2 = arr2obj2(keyValues);
console.log('result2', result2);
```

</details>

[在线示例](https://codepen.io/Jesonhu/pen/RwbopBM)