# Vuejs 响应式系统是如何实现的？

```javascript
let data = { price: 5, quantity: 2 };
let target = null;

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

