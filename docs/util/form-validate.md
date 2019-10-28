# 表单验证

## 自实现的简单表单验证

```js
/**
* 表单验证.
*
* @author Jesonhu
* @update 2019/09/27 
*/

/**
 * @example
 * 
  const rules = [
    {
      name: 'name',
      validate: (val) => val !== '',
      msg: '用户名不能为空'
    },
    {
      name: 'name',
      validate: (val) => /^[\u4E00-\u9FA5]+$/.test(val),
      msg: '用户名格式不正确'
    },
    {
      name: 'phone',
      validate: (val) => val !== '',
      msg: '手机号不能为空'
    },
    {
      name: 'phone',
      validate: (val) => /^((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,5-9]))\d{8}$/.test(val),
      msg: '手机号格式不正确'
    }
  ]

 const validateData = { name: 'xx', phone: 'xxx' }
 validater(rules, validateData, (errMsgArr) => {
    if (errMsgArr.length > 0) { // has error

    } else { // validate pass

    }
 })
 * 
 * 
 */

/**
 * 表单验证
 * @param {Array} rules 验证规则
 * @param {Array} validatedData 验证数据
 * @param {Function} cb 处理回调
 */
function validater(rules, validatedData, cb) {
  let formatRules = [];
  formatRules = rules.map((item, index, array) => {
    // add value
    const name = item['name'];
    // console.log(name, validatedData);
    if (name in validatedData) {
      item['value'] = validatedData[name];
    } else {
      item['value'] = '';
    }
    return item;
  });

  const valideter = (formatRules) => {
    const msgArr = [];
    const len = formatRules.length;
    for (let i = 0; i < len; i++) {

      const value = formatRules[i]['value'];
      const validteFn = formatRules[i]['validate'];
      // 验证通过
      const isPass = validteFn(value);
      if (!isPass) {
        const errorMsg = formatRules[i]['msg'];
        msgArr.push(errorMsg);
      }
    }
    return msgArr;
  }

  let errorMsgArr = valideter(formatRules);

  if (cb && cb instanceof Function) cb(errorMsgArr);
}

export default validater;

```

```js
// 使用方式
const  rules = [
  {
    name: 'name',
    validate: (val) => val !== '',
    msg: '姓名不能为空'
  },
  {
    name: 'name',
    validate: (val) => /^[\u4E00-\u9FA5]+$/.test(val),
    msg: '用户名格式不正确'
  },
  {
    name: 'phone',
    validate: (val) => val !== '',
    msg: '手机号不能为空'
  },
  {
    name: 'phone',
    validate: (val) => /^((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,5-9]))\d{8}$/.test(val),
    msg: '手机号格式不正确'
  },
  {
    name: 'time',
    validate: (val) => val !== '',
    msg: '请选择看房时间!'
  }
]

```