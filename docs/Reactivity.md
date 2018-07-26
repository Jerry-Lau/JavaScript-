# Vuejs 响应式系统是如何实现的？

```javascript
let data = { price: 5, quantity: 2 };
// every target is a dependency, which depends on the state.
// and when the state changes, the dependencies get notified automatically.
let target = null;

// 一个 Dep 类用来实现存储和通知依赖
// 实现了一个标准的观察者模式 Observer pattern
class Dep {
  constructor() {
    // store the targets that are dependent, and should be run when notify is called
    this.subscribers = [];
  }

  depend() {
    if (target && !this.subscribers.includes(target)) {
      this.subscribers.push(target);
    }
  }

  notify() {
    this.subscribers.forEach(sub => sub());
  }
}

// Go through each of our data properties
Object.keys(data).forEach(key => {
  let internalValue = data[key];

  const dep = new Dep();

  // add property access hooks
  Object.defineProperty(data, key, {
    get() {
      dep.depend();
      return intervalValue;
    },
    set(newValue) {
      internalValue = newValue;
      dep.notify();
    }
  })
})

function watcher(func) {
  target = func;
  target();
  target = null;
}

watcher(() => { 
  data.total = data.price * data.quantity;
})
```

