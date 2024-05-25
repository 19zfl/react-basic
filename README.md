# React

### React入门

1. 什么是React

- 发送请求获取数据
- 处理数据（过滤、整理格式）
- 操作DOM呈现页面

React 是一个将数据渲染为HTML视图的开源JavaScript库。

由Facebook开发，且开源

为什么要使用React？

- 原生js操作DOM繁琐，效率底（DOM-API操作UI）
- 使用js直接操作DOM，浏览器会进行大量的重绘重排
- 原生js没有组件化编码方案，代码复用率低

React特点：

- 采用组件化模式、声明式编码，提高开发效率及组件复用率
- 在React Native中可以使用React语法进行移动端开发
- 使用虚拟DOM+优秀的Diffing算法，尽量减少与真实DOM的交互

React高效的原因：

- 使用虚拟DOM，不总是直接操作页面真是DOM
- DOM Diffing算法，最小化页面重绘

#### 虚拟DOM创建的两种方式

- jsx创建
- js创建（不需要引入babel）

#### 真是DOM与虚拟DOM

关于虚拟DOM：

- 本质是Object类型的对象（一般对象）
- 虚拟DOM比较轻（自身属性少），因为虚拟DOM是React内部使用的dom，无需真实DOM上那么多的属性
- 虚拟DOM最终会被React转换为真实DOM，呈现在页面上

#### JSX

- 全称：JavaScript XML

- React定义的一种类似于XML的js扩展语法：JS+XML
- 本质是React.createElement(component, props......children)方法的语法糖
- 作用：用来简化创建虚拟DOM
  - 写法：`const VDOM = <h1>Hello React!</h1>`
  - VDOM不是一个字符串，也不是HTML/XML标签
  - 它最终产生的就是一个JS对象
- 标签名任意：HTML标签或者其他标签

##### 语法规则：

- 定义虚拟DOM时，不要写引号
- 标签中混入JS表达式时要用{ }
- 样式的类名指定不要用class，要用className
- 内联样式，要用style={{key:value}}的形式要写
- 虚拟DOM必须只有一个根标签
- 标签必须闭合
- 标签首字母
  - 若小写字母开头，则将该标签转为html中同名元素，若html中无该标签对应的同名元素，则报错
  - 若大写字母开头，则React就去渲染对应组件，若组件没有定义，则报错

#### 模块与组件、模块化与组件化的理解

##### 模块

1. 理解：向外提供特定功能的js程序，一般就是一个js文件
2. 为什么要拆成模块：随着业务逻辑增加，代码越来越多且复杂
3. 作用：复用js，简化js的编写，提高js运行效率

##### 组件

1. 理解：用来实现局部功能效果的代码和资源的集合（html/css/js/image等等）
2. 为什么：一个界面的功能更复杂
3. 作用：复用编码，简化项目编码，提高运行效率

##### 模块化

当应用的js都以模块来编写的，这个应用就是一个模块化的应用

##### 组件化

当应用是以多组件的方式实现，这个应用就是一个组件化的应用

### React面向组件编程

#### 基本理解和使用

##### 定义组件的方式（两种）：

1. 函数式组件
2. 类式组件

#### 组件实例的三大核心属性1：state

##### 理解：

- state是组件对象最重要的属性，值是对象（可以包含多个key-value的组合）
- 组件被称为“状态机”， 通过更新组件的state来更新对应的页面显示（重新渲染组件）

##### 强烈注意：

- 组件中render方法中的this为组件实例对象
- 组件自定义方法中this为undefined，如何解决？
  - 强制绑定this，通过函数对象的bind()
  - 箭头函数
- 状态数据，不能直接修改或更新

#### 组件实例的三大核心属性2：props

##### 理解：

- 每个组件对象都会有props（properties简写）属性
- 组件标签的所有属性都保存在props中

#### 组件实例的三大核心属性3：refs

- 字符串形式的ref
- 回调函数形式的ref
- createRef API

回调函数形式的ref执行的次数的问题

#### React中的事件处理

- 通过onXxx属性指定事件处理函数（注意大小写）
  - React使用的是自定义（合成）事件，而不是使用的原生DOM事件——为了更好的兼容性
  - React中的事件是通过事件委托方式处理的（委托给组件最外层的元素）——为了高效
- 通过event.target得到发生事件的DOM元素对象——不要过度使用ref

#### 收集表单数据

包含表单的组件分类

- 受控组件
- 非受控组件
- 高阶函数
- 函数柯里化

#### 组件生命周期

- 组件对象从创建到死亡它会经历特定阶段
- React组件对象包含一系列钩子函数（生命周期回调函数），在特定的时刻调用
- 我们在定义组件时，在特定的生命周期回调函数中做特定的工作

##### 生命周期的三个阶段（旧）：

1. 初始化阶段：有ReactDOM.render()触发一次渲染
   1. constructor()
   2. componentWillMount()
   3. render() ==> 常用
   4. componentDidMount() ==> 常用：一般在这个钩子中做一些初始化的事情，例如：开启定时器、发送网络请求、订阅消息等等
2. 更新阶段：有组件内部this.setState()或父组件重新render触发
   1. shouldComponentUpdate()
   2. componentWillUpdate()
   3. render()
   4. componentDidUpdate()
3. 卸载组件：有ReactDOM.unmountComponentAtNode()触发
   1. componentWillUnmount() ==> 常用：一般在这个钩子中做一些收尾的事，例如：关闭定时器、取消订阅消息等等

##### 生命周期的三个阶段（新）：

1. 初始化阶段：由ReactDOM.render()触发第一次渲染
   1. constructor()
   2. getDerivedStateFromProps()
   3. render()
   4. componentDidMount()
2. 更新阶段：由组件内部this.setState()或父组件重新render触发
   1. getDerivedStateFromProps()
   2. shouldComponentUpdate()
   3. render()
   4. getSnapshotBeforeUpdate()
   5. componentDidUpdate()
3. 卸载组件：由ReactDOM.unmountComponentAtNode()触发
   1. componentWillUnmount()

>getSnapshotBeforeUpdate()在最近一次渲染输出（提交到DOM节点）之前调用。它使得组件能在发生更改之前从DOM中捕获一些信息（例如，滚动位置）。此生命周期的任何返回值将作为参数传递给componentDidUpdate()，

##### 重要的钩子函数

1. render：初始化渲染或者更新渲染调用
2. componentDidMount：开启监听，发送ajax请求
3. componentWillUnmount：做一些收尾工作，如：清理定时器

##### 即将废弃的钩子函数

1. componentWillMount
2. componentWillReceiveProps
3. componentWillUpdate

> 现在使用会出现警告，下一个大版本需要加上UNSAFE_前缀才能使用，以后可能会被彻底废弃，不建议使用

#### 虚拟DOM与DOM Diffing算法

1. 虚拟DOM中key的作用：

   1. 简单地说：key是虚拟DOM对象的标识，在更新显示时key是起着极其重要的作用。

   2. 详细地说：当状态中的数据发生变化时，React会根据【新数据】生成【新的虚拟DOM】，随后React进行【新虚DOM】与【旧虚拟DOM】的diffing比较，比较规则如下：

      1. 旧虚拟DOM中找到了与新虚拟DOM相同的key：
         1. 若虚拟DOM中内容未变，直接使用之前的真实DOM
         2. 若虚拟DOM中内容未变，则生成新的真实DOM，随后替换掉页面中之前的真实DOM

      2. 旧虚拟DOM中未找到与新虚拟DOM相同的key：
         1. 根据数据创建新的虚拟DOM，随后渲染到页面

2. 用index作为key可能会引发的问题：
   1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作，会产生没有必要的真实DOM更新==>界面效果没有问题，但效率低
   2. 如果结构中还包含输入类的DOM，会产生错误DOM更新==>界面有问题
   3. 注意：如果不存在对数据进行逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key没有问题

3. 开发中如何选择key？
   1. 最好使用每条数据的唯一标识作为key，比如：id、手机号、身份证号、学号等
   2. 如果确定知识简单的展示数据，用index也是可以的