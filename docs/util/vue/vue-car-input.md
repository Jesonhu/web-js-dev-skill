# 基于 Vue 的车牌号输入组件

|更新时间|创建时间|来源|
|--|--|--|
|2019/01/29|2018/06/06|原创|

## Props 配置

无

## 组件属性

|属性|类型|说明|默认值|可选值|
|--|--|--|--|--|
|`searchValue`| Object | 当前选中值的相关属性 |  [] | - |
| `isValidatePass` | Boolean | 车牌号是否验证通过, | false | - |
| `isShowCarNoKeyBoard` | Boolean | 键盘是否显示 | false | - |

## 组件事件

|事件名|说明|参数|返回值|
|--|--|--|--|
|`carNoInput`|车牌号输入时派发|args1: 是否通关验证(类型: Boolean。true: 成功; false: 失败); args2: 当前输入的车牌号(类型: String)|-|
|`validateCarNo`|验证当前车牌|args1: 是否点击了 `搜索车牌` 按钮(类型: Boolean。true: 点击); args2: 当前输入的车牌号(类型: String)|-|

## 相关资料

+ [源码1-xldjd](https://gitee.com/weblife/fh-xldjd-wx-parking/blob/2.0/src/components/Car-input-basic/index.vue)