# EventEmitter

> JS 的一道坎就是事件的处理，那么如何自定义事件，如何处理事件呢，这篇主要讲解事件的监听、派发与移除的封装. 自定义事件处理类，非基于 dom 的自定义事件处理类. 继承: 无

## 源码

```js
class EventEmitter {
  constructor() {
    this.$_listeners = {};
  }

  on(name, callback, scope = null) {
    this.$_listeners[name] = this.$_listeners[name] || [];
    if ( scope !== null) callback['_scope'] = scope;
    this.$_listeners[name].push(callback);
  }

  off(name, callback) {
    const listeners = this.$_listeners[name];

    if (Array.isArray(listeners)) {
      const index = listeners.indexOf(callback);
      if (index === -1) return;
      listeners.splice(index, 1);
    }
  }

  trigger(name, params = null) {
    const listeners = this.$_listeners[name];

    if (Array.isArray(listeners)) {
       if (listeners.length <= 0) return;
       listeners.forEach(cb => {
         if (cb && cb instanceof Function) {
           const scope = cb['_scope'];
           if (scope === null) {
             (params === null) ? cb() : cb(params);
           } else {
              (params === null) ? cb.call(scope) : cb.call(scope, params);
           }
         } 
       });
    }
  }

}
```

## demo1:

```js
class Hello extends EventEmitter {}

const obj = {
  name: '我是scope',
  
  fn1: function() {
    console.log('fn1');
  },

  fn2: function(params) {
    console.log('=== fn2 ===', params, this);
  }
}

function fn1() {
  console.log('fn1');
}

function fn2(params) {
  console.log('fn2', params, this);
}

const hello = new Hello();

hello.on('hello', obj.fn1);
hello.on('hello', obj.fn2, obj);
hello.trigger('hello', '参数');
hello.off('hello', obj.fn1);
hello.trigger('hello', '参数');

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


## 实践 Project

+ 砸金蛋: fehelper-res
+ [webSocket 浏览端的事件封装](https://juejin.im/post/5d78b3956fb9a06b2d77fe78)
+ [node.js ws 摇一摇事件处理](https://gitee.com/weblife/scene-wx-server/blob/ws_wsclient/src/Shake.js)

## 参考资料

+ [greensock-EventDispatcher](https://github.com/greensock/GreenSock-JS/blob/86b54d1c70237daeb754f6be8b5d9ee4f4c9cbe2/src/uncompressed/TweenLite.js#L216)
+ [createjs-EventDispatcher](http://www.createjs.cc/src/docs/preloadjs/files/createjs_events_EventDispatcher.js.html#l41)
