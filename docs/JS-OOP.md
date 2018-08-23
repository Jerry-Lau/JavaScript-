# JavaScript 的面向对象模型 —— Prototypal inheritance

> JavaScript is a bit confusing for developers coming from Java or C++, as it's all dynamic, 
all runtime, and it has no classes at all. It's all just instances (objects). 

when you call
```javascript
function Foo() {
  this.name = 'foo';
}

const f = new Foo();
```
JavaScript actually just does

```javascript
const f = new Object();
f.[[Prototype]] = Foo.prototype;
Foo.call(f);
```