# React 相关

### Redux

> http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html

- Redux 的设计思想很简单，就两句话：

```
（1）Web 应用是一个状态机，视图与状态是一一对应的。
（2）所有的状态，保存在一个对象里面。
```

- Reducer

```
Store 收到 Action 以后，必须给出一个新的 State，这样 View 才会发生变化。这种 State 的计算过程就叫做 Reducer。
Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。
Reducer 是纯函数，不能改变 State，必须返回一个全新的对象
```

- bindActionCreators(actionCreators, dispatch)

  > http://cn.redux.js.org/docs/api/bindActionCreators.html

```
把 action creators 转成拥有同名 keys 的对象，但使用 dispatch 把每个 action creator 包围起来，这样可以直接调用它们。
惟一使用 bindActionCreators 的场景是当你需要把 action creator 往下传到一个组件上，却不想让这个组件觉察到 Redux 的存在，而且不希望把 Redux store 或 dispatch 传给它。
```

### React-dedux

> http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html
>
> http://cn.redux.js.org/docs/react-redux/api.html

- React-Redux 将所有组件分成两大类：UI 组件（presentational component）和容器组件（container component）
- React-Redux 规定，所有的 UI 组件都由用户提供，容器组件则是由 React-Redux 自动生成
- TodoList是 UI 组件，VisibleTodoList就是由 React-Redux 通过connect方法自动生成的容器组件:

```
import { connect } from 'react-redux'
const VisibleTodoList = connect(
  mapStateToProps,
  mapDispatchToProps,
  mergeProps,
  options
)(TodoList);
```

```
// mapStateToProps(state, [ownProps])
const mapStateToProps = (state) => {
  return {
    todos: getVisibleTodos(state.todos, state.visibilityFilter)
  }
}
// connect方法可以省略mapStateToProps参数，那样的话，UI 组件就不会订阅Store，就是说 Store 的更新不会引起 UI 组件的更新
```

- <Provider store=...>组件，使组件层级中的 `connect()` 方法都能够获得 Redux store（容器组件），原理是利用了React的getChildContext方法
- 正常情况下，根组件应该嵌套在 `<Provider>` 中才能使用 `connect()` 方法

### PureComponent

- [在React.js中使用PureComponent的重要性和使用方式](http://www.zcfy.cc/article/why-and-how-to-use-purecomponent-in-react-js-60devs-2344.html)

### 高阶组件

- 比如：react-redux的connect函数

  把redux的state和action创建函数，通过props注入给了Component。
  你在目标组件Component里面可以直接用this.props去调用redux state和action创建函数了。

  ```
  ConnectedComment = connect(mapStateToProps, mapDispatchToProps)(Component);
  ```

- antd的Form也是一样的

  ```
  const WrappedNormalLoginForm = Form.create()(NormalLoginForm);
  ```

- http://react-china.org/t/react-higher-order-components/14949

- 实现高阶组件的两种方式：参数代理、继承反转：https://zhuanlan.zhihu.com/p/24776678

### typescript

- 泛型的『类型变量』

  - 使用了 *类型变量*，它是一种特殊的变量，只用于表示类型而不是值

  ```
  function identity<T>(arg: T): T {
      return arg;
  }

  ------

  function loggingIdentity<T>(arg: T[]): T[] {
      console.log(arg.length);
      return arg;
  }
  ```

  - 我们给identity添加了类型变量`T`。 `T`帮助我们捕获用户传入的类型（比如：`number`），之后我们就可以使用这个类型。 之后我们再次使用了 `T`当做返回值类型。现在我们可以知道参数类型与返回值类型是相同的了。 这允许我们跟踪函数里使用的类型的信息。
  - 不同于使用 `any`，它不会丢失信息，像第一个例子那像保持准确性，传入数值类型并返回数值类型

- 一组 declare 的合集组成了 .d.ts 文件。部分IDE可以智能提示。

### 一些文章
- [React性能优化总结](https://github.com/Pines-Cheng/blog/issues/3)
- [精读 Immutable 结构共享](https://github.com/ascoders/blog/issues/20)
- [助你完全理解React高阶组件（Higher-Order Components）](http://react-china.org/t/react-higher-order-components/14949)