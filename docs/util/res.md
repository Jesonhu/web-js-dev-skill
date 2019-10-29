# 资源预加载类

> 基于浏览器 createjs preloadjs 的资源, 代码结构参考 egret RES 的资源域加载

## 代码结构简析

```js
const RES = {};

/** 资源配置处理 */
class ResourcesConfig {}
const resourcesConfig = new ResourcesConfig();

/** 异步处理 */
class PromiseQueue {
  aaa() {
  
  }
}
const queue = new PromiseQueue;

/** 管理(联合：异步处理与资源配置处理) */
const manager = {
  config: resourcesConfig,
  aaa() {
    const { config } = this;
    return queue.aaa();
  }
}
RES.manager = manager;

/** 事件派发类 */
class EventEmitter {}

class Resources extends EventEmitter {
  aaa() {
    return RES.manager.aaa()
  }
}

const instance = new Resources();

RES.aaa = function() {
  instance.aaa();
}


window.RES = RES;

```

## 相关资源

+ [砸金蛋-res 源码](https://gitee.com/weblife/beat-egg/blob/master/lib/res/fehelper-res.js)