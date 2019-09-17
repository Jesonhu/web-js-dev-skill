# 事件处理

> JS 的一道坎就是事件的处理，那么如何自定义事件，如何处理事件呢，这篇主要讲解事件的监听、派发与移除的封装


## 存粹的实现 .on() .off() .emit()

```js
class EventHandle {
  constructor() {
    this.init();
  }

  init() {
    this._callbacks = {};
  }

  on(name, callback) {
    this._callbacks[name] = this._callbacks[name] || [];
    this._callbacks[name].push(callback);
  }

  off(name, callback) {
    const callbacks = this._callbacks[name];
    if (callbacks && callbacks instanceof Array) {
      const index = callbacks.indexOf(callback);
      if (index === -1) return;
      callbacks.splice(index, 1);
    }
  }

  trigger(name, params) {
    const callbacks = this._callbacks[name];
    if (callbacks && callbacks instanceof Array) {
      callbacks.forEach(cb => {
        if (cb && cb instanceof Function) cb();
      });
    }
  }
}


// 测试部分

class Hello extends EventHandle {}

const hello = new Hello();

function fn1() {
  console.log('fn1');
}

function fn2() {
  console.log('fn2');
}

hello.on('hello', fn1);
hello.on('hello', fn2);
hello.trigger('hello');
hello.off('hello', fn2);
hello.trigger('hello');

```

PS: 这种方式的处理要注意一下两种事件绑定不能被移除的情况

```js
// Bad1:

const hello = new Hello();
hello.on('hello', function() {
    // some code
});
hello.on('hello', function() {
    // another code
});
hello.off('hello', function() {
    // some code;
});

// Bad2:

const hello = new Hello();
hello.on('hello', function fn1() {
    // some code
});
hello.on('hello', function fn2() {
    // another code
});
hello.off('hello', function fn2() {
    // some code;
});

```

以上代码为什么不能被移除呢？请移步看 `匿名函数` `函数重复定义` 相关的知识点.

## 参考资料
+ [webSocket 浏览端的事件封装](https://juejin.im/post/5d78b3956fb9a06b2d77fe78)
+ [node.js ws 摇一摇事件处理](https://gitee.com/weblife/scene-wx-server/blob/ws_wsclient/src/Shake.js)