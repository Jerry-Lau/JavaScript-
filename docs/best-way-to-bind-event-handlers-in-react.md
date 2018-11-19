## React 应用中，事件绑定的最佳实践
(https://medium.freecodecamp.org/the-best-way-to-bind-event-handlers-in-react-282db2cf1530)

### 1.在 JSX 中动态绑定

```javascript
class HelloWorld extends Component {
  handleClick(event) {}

  render() {
    return (
      <p>Hello, {this.state.name}!</p>
      <button onClick={this.handleClick.bind(this)}>Click</button>
    );
  }
}
```

#### 缺点
- 每一次re-render, 都会生成一个全新的 event handler，从而导致 button 组件也会被重新渲染，性能糟糕。

### 2.在 Constructor 中提前绑定

```javascript
class HelloWorld extends Component {
  constructor() {
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick(event) {}

  render() {
    return (<button onClick={this.handleClick} />);
  }
}
```

这是一种最传统的绑定方式，缺点就是比较繁琐，必须手动在构造函数中去一个个绑定。

### 3.利用箭头函数绑定

利用 arrow function 的词法作用域特性，在方法声明的时候，就能绑定，这是最简单方便的。

```javascript
class HelloWorld extends Component {
  handleClick = (event) => {

  }

  render() {
    return (<button onClick={this.handleClick} />)
  }
}
```

### 4.多个 input 元素动态绑定 event handler

```javascript
class HelloWorld extends Component {
  handlers = {}

  handleChange = name => {
    if (!this.handlers[name]) {
      this.handlers[name] = event => {
        this.setState({ [name]: event.target.value });
      };
    }
    return this.handlers[name];  
  }

  render() {
    return (
      <input onChange={this.handleChange('name')} />
      <input onChange={this.handleChange('description')} />
    )
  }
}
```


### 5.使用 autobind 修饰符

使用类的修饰符来自动绑定

```javascript
import { autobind } from 'core-decorators';

@autobind
class HelloWorld extends Component {
  handleClick(e) {
    console.log(e.nativeEvent);
  }

  render() {
    return (<button onClick={this.handleClick} />)
  }
}
```