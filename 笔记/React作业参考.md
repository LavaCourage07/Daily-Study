# Day01 作业布置

## 一. 完成课堂所有的代码







## 二. React开发的三个依赖包是什么？分别有什么作用？

* react:包含react所有必须的核心代码
* react-dom：react 渲染在不同平台所需要的核心代码
* babel:将jsx转换为 React 代码的工具





## 三. React如何封装组件，组件里面包含哪些内容？

* 类的方式封装组件

* 定义一个类（类名大写，组件的名称是必须大写的，小写会被认为是HTML元素），继承自React.Component

* .实现当前组件的render函数

  ~~~js
  class App extends React.Component{
      render(){
          return <h2> Hello React<h2/>
      }
  }
  #渲染根组件
  const root =ReactDOM.createRoot(document.querySelector("#r oot"))
  #使用组件
  root.render(<App/>)
  ~~~

  





## 四. 在进行函数绑定时，如何进行this关键字的绑定？

* 在传入函数时直接绑定this

  ~~~js
     render() {
          return (
            <div>
              <h2>{this.state.message}</h2>
              <button onClick={this.btnClick.bind(this)}>点击</button>
            </div>
          )
        }
  ~~~

  

* 在类中提前绑定需要使用的函数的this

  ~~~js
     class App extends React.Component {
        // 组件数据
        constructor() {
          super()
          this.state = {
            message: "Hello World",
           
          }
  
          // 对需要绑定的方法, 提前绑定好this
          this.btnClick = this.btnClick.bind(this)
        }
     
     render() {
          return (
            <div>
              <h2>{this.state.message}</h2>
              <button onClick={this.btnClick}>点击</button>
            </div>
          )
        }
  }
  ~~~

  



## 五. React如何进行列表数据的展示？回顾数组的常见高阶函数。

* 方式一：直接使用for循环 

  ~~~js
      render() {
          // 1.对movies进行for循环
          const liEls = []
          for (let i = 0; i < this.state.movies.length; i++) {
          const movie = this.state.movies[i]
          const liEl = <li>{movie}</li>
          liEls.push(liEl)
          }
            <div>
              <h2>电影列表</h2>
              <ul>
               <li> {liEls}</li>
              </ul>
            </div>
          )
        }
  ~~~

  

* 方式二：map 高阶函数

  ~~~js
  
  
        render() 
  #返回一个新的数组
          const liEls = this.state.movies.map(movie => <li>{movie}</li>)
  
          return (
            <div>
              <h2>电影列表</h2>
              <ul>
                 <li> {liEls}</li>
              </ul>
            </div>
          )
        }
        
        
  ~~~

  

* 方式三： map 高阶函数 表达式

  ~~~js
  <ul>
  {this.state.movies.map(movie => <li>{movie}</li>)}
  </ul>
  ~~~

  

## 六. JSX如何绑定数据？如何绑定内容、属性，有哪些规则？

* 绑定数据

  ~~~js
      class Home extends React.Component {
          constructor() {
              super();
              this.state = {
                  message: 'BNTang'
              }
          }
  
          render() {
              return (
                  <div>
                      <p id="box">{this.state.message}</p>
                      <p title={this.state.message}>{this.state.message}</p>
                  </div>
              )
          }
      }
  
  ~~~

  

* 绑定class

  ~~~js
    class Home extends React.Component {
          constructor() {
              super();
              this.state = {
                  isActive: true,
                   objStyle: {color: "red", fontSize: "30px"}
              }
          }
  
          render() {
           const { title, imgURL, href, isActive, objStyle } = this.state
          #1.class绑定的写法一: 字符串的拼接
          const className = `abc cba ${isActive ? 'active': ''}`
          
         # 2.class绑定的写法二: 将所有的class放到数组中
          const classList = ["abc", "cba"]
          if (isActive) classList.push("active")
              
         # 3.class绑定的写法三: 第三方库classnames -> npm install classnames
            
              return (
                  <div>
                     <h2 className={className}>哈哈哈哈</h2>
                     <h2 className={classList.join(" ")}>哈哈哈哈</h2>
                  </div>
              )
          }
      }
  
   
  ~~~
  
  



* 绑定style

  ~~~js
   class Home extends React.Component {
          constructor() {
              super();
              this.state = {
                  message: 'BNTang'
              }
          }
  
          render() {
              return (
                  <div>
                      <p style={{color: 'red', fontSize: '100px'}}>{this.state.message}</p>
                  </div>
              )
          }
      }
  ~~~

  

* 绑定属性

  ~~~js
  <p title="我是标题">我是段落</p>
  
  <p title={message}>我是段落</p>
  ~~~

  

* 书写规范
  * 顶层只有一个根元素
  * jsx 的外层需要包裹一个 （） 方便阅读，可以进行换行书写
  * jsx的标签可以是单标签，也可以是双标签
  * 单标签必须以/>结尾
  * jsx中的注释 { /* */}
  * JSX嵌入变量作为子元素
    * 情况一：当变量是Number、String、Array类型时，可以直接显示
    * 情况二：当变量是null、undefined、Boolean类型时，内容为空；
      如果希望可以显示null、undefined、Boolean，那么需要转成字符串；
      转换的方式有很多，比如toString方法、和空字符串拼接，String(变量)等方式；
    * 情况三：Object对象类型不能作为子元素（not valid as a React child）





# Day02 作业布置

## 一. 完成课堂所有的代码







## 二. JSX绑定事件，this绑定有哪些规则？如何给函数传递参数？

* this绑定规则

  * 普通绑定 - `onClick={this.btnClick}` - 在内部是独立函数调用,所以this为undefined
  * this绑定方式一: bind绑定 - `onClick={this.btnClick.bind(this)}`
  * this绑定方式二: ES6 class fields - `onClick={this.btnClick}` - `btnClick = () => {}`
  * this绑定方式三: 直接传入一个箭头函数 - `onClick={() => this.btnClick()}`

* 给函数传递参

  * event参数的传递 - `onClick={(event) => this.btn1Click(event)}`
  * 额外参数的传递 - `onClick={(event) => this.btn2Click(event, "http", 18)}`

  ```js
  btn1Click(event) {
    console.log(event);
  }
  btn2Click(event, name, age) {
    console.log(event, name, age);
  }
  ```





## 三. JSX的代码是如何被编译为React代码的？它的本质是进行什么操作？

* jsx是通过babel工具转换编译成React代码的
* 本质
  * jsx 仅仅只是 React.createElement(component, props, ...children) 函数的语法糖
  * 所有的jsx最终都会被转换成React.createElement的函数调用

`



## 四. 什么是虚拟DOM？虚拟DOM在React中起到什么作用？

* 什么是虚拟DOM？
  * Virtual DOM 是一种编程概念，UI以一种理想化或者说虚拟化的方式保存在内存中
  * Virtual DOM 本质上是 JavaScript 对象，是真实 DOM 的描述，⽤⼀个 JS 对象来描述⼀个 DOM 节点
  * 我们知道jsx转成React代码的本质是 - 转换成React.createElement的函数调用
  * 通过React.createElement的函数创建出来的`ReactElement`对象
  * React利用`ReactElement`对象组成了一个JavaScript的对象树 - JavaScript的对象树就是**虚拟DOM**
* 虚拟DOM在React中的作用
  * 虚拟DOM 通过diff算法 - 以最⼩的代价更新变化的视图
  * 跨平台渲染
  * 声明式编程 - 虚拟DOM帮助我们从命令式编程转到了声明式编程的模式
    * 你只需要告诉React希望让UI是什么状态
    * React来确保DOM和这些状态是匹配的
    * 不需要直接进行DOM操作，就可以从手动更改DOM、属性操作、事件处理中解放出来







## 五. 分析脚手架创建的React项目目录结构，并且删除文件后自己编写代码

* public
  * favicon.ico -- 应用程序顶部icon图标
  * index.html -- 应用的index.html入口文件
  * logo192.png -- 在manifest.json中被使用
  * logo512.png -- 在manifest.json中被使用
  * manifest.json -- 与web app配置相关
  * robots.text -- 指定搜索引擎可以或者不可以爬取那些信息
* src
  * App.css -- App组件相关样式
  * App.js -- App组件代码文件
  * App.test.js -- App组件的测试代码文件
  * index.css -- 全局样式文件
  * index.js -- 整个应用程序的入口文件
  * logo.svg -- 启动项目时,所看到的React图标
  * reportWebVitals.js -- 默认帮我们写好的 注册pwa相关的代码
  * setupTests.js -- 测试初始文件
* **pwa是什么?** 全称Progressive Web App，即渐进式WEB应用
  * 一个 PWA 应用首先是一个网页, 可以通过 Web 技术编写出一个网页应用
  * 随后添加上 App Manifest 和 Service Worker 来实现 PWA 的安装和离线等功能
  * 这种Web存在的形式，我们也称之为是 Web App
  * pwa可以将网页添加至主屏幕，点击主屏幕图标可以实现启动动画以及隐藏地址栏
  * pwa实现离线缓存功能，即使用户手机没有网络，依然可以使用一些离线功能
  * pwa实现了消息推送





## 六. 选做：寻找之前课程中的一些案例，尝试使用React来实现







# Day03 作业布置

## 一. 完成课堂所有的代码

- 重点
  - 组件的概念
  - 组件的生命周期
  - 组件通信
    - 父传子
    - 子传父
    - 非父子组件的通信

## 二. React组件可以如何进行划分？分别有哪些不同的概念？

- 根据定义方式
  - 函数组件
  - 类组件
- 根据组件内部有无状态需要维护
  - 无状态组件
  - 有状态组件
- 根据组件的不同职责
  - 展示型组件
  - 容器型组件

- 关注UI的展示
  - 函数组件,无状态组件,展示型组件
- 关注数据逻辑的展示
  - 类组件,有状态组件,容器型组件

## 三. React重要的组件生命周期有哪些？分别列出他们的作用。

- componentDidMount
  - 会在组件挂载后立即调用
  - 操作DOM
  - 发送网络请求
- componentDidUpdate
  - 会在组件更新后立即调用
  - 首次渲染不会执行此方法
  - 可以在组件更新后操作DOM
- conponentWillUnmount
  - 会在组件卸载及销毁前调用
  - 清除定时器
  - 清除事件监听

## 四. React中如何实现组件间的通信？父传子？子传父？

- 父传子
  - 在子组件通过属性传递内容
  - 子组件通过props拿到内容
- 子传父
  - 通过传递函数,调用回调函数
  - 通过函数的参数传递要传递的数据

## 五. React中有插槽的概念吗？如果没有，如何实现插槽的效果呢？

- 没有插槽的概念
- 实现插槽效果的方式
  - 直接在组件中插入children
  - 在目标组件拿到插入的内容进行展示
- 通过props直接将要展示的内容传递给子组件
  - 子组件通过props直接拿到要展示的内容

## 六. 非父子组件的通信有哪些方式？分别是什么作用？

- 事件总线
- 使用context
  - 创建context
  - 在要使用的组件,一般是根组件导入context
  - 使用<context.Provider>包裹后代组件
  - 在要使用的后代组件引入context
    - xxxx.contextType = context
    - 在render方法中可以通过this.context拿到传递过来的值



# Day04 作业布置

## 一. 完成课堂所有的代码







## 二. 非父子组件的通信有哪些方式？分别是什么作用？

- Context
  - 1.创建Context
  - 2.使用<context.Provider>包裹后代组件
  - 3.在要使用的后代xxxx组件引入context
    - xxxx.contextType = context
    - 在render方法中可以通过this.context拿到传递过来的值
- 事件总线EventBus

* Redux







## 三. 面试题：React的setState是同步的还是异步的？React18中是怎么样的？

* 在 React 中，可变状态通常保存在组件的 state 属性中，并且只能通过使用 setState()来更新

* React的setState是异步的 -- 不要指望在调用 `setState` 之后，`this.state` 会立即映射为新的值

* 在react18之前, 在setTimeout,Promise等中操作setState, 是同步操作

* 在react18之后, 在setTimeout,Promise等中操作setState,是异步操作(批处理)

  * 如果需要同步的处理怎么办呢? 需要执行特殊的`flushSync`操作

* 为什么要将setState设计成异步的

  * 首先,若是将setState设计成同步的,在`componentDidMount`中请求多个网络请求时,会堵塞后面的网络请求

  ```js
  componentDidMount() {
    // 网络请求一 : this.setState
    // 网络请求二 : this.setState
    // 网络请求三 : this.setState
    // 如果this.setState设计成同步的,会堵塞后面的网络请求
  }
  ```

  * 一. setState设计为异步，可以显著的提升性能

    * 如果每次调用 setState都进行一次更新，那么意味着render函数会被频繁调用，界面重新渲染，这样效率是很低的
    * 最好的办法应该是**获取到多个更新，之后进行批量更新**

    ```js
    // 在一个函数中有多个setState时,
    this.setState({}) --> 先不会更新,而是会加入到队列(queue)中 (先进先出)
    this.setState({}) --> 也加入到队列中
    this.setState({}) --> 也加入到队列中
    // 这里的三个setState会被合并到队列中去
    // 在源码内部是通过do...while从队列中取出依次执行的
    ```

  * 二: 如果同步更新了state，但是还没有执行render函数，那么state和props不能保持同步





## 四. 性能优化:什么是SCU优化？类组件和函数组件分别如何进行SCU的优化？

* **shouldComponentUpdate -- SCU** -- React提供给我们的声明周期方法

* SCU优化就是 一种巧妙的技术,用来减少DOM操作次数,具体为当React元素没有更新时,不会去调用render()方法

* 可以通过`shouldComponentUpdate`来判断`this.state`中的值是否改变

  ```js
  shouldComponentUpdate(nextProps, nextState) {
     const {message, counter} = this.state
     if(message !== nextState.message || counter !== nextState.counter) {
       return true
     }
     return false 
   }
  ```

* React已经帮我们提供好SCU优化的操作

  * 类组件: 将class继承自`PureComponent`
  * 函数组件: 使用一个高阶组件`memo`

  ```js
  import {mome} from 'react'
  
  const HomeFunc = mome(function(props) {
    console.log("函数式组件")
    return (
      <h4>函数式组件: {props.message}</h4>
    )
  })
  
  export default HomeFunc
  ```





## 五. React为什么要强调不可变的力量？如何实现不可变的力量？

* 不可变的力量: 不要直接去修改this.state中的值(主要指对象),若是想修改的话,应该是将这整个值全部修改掉
  * 注意: 值类型,在修改的时候,本身就全部替换掉了,所以不需要其他操作,直接改就可以
* 实现: 将对象浅拷贝赋值给一个新的变量,在将这个新的变量赋值给this.state中的值





## 六. React中获取DOM的方式有哪些？

* ref获取DOM

  ```jsx
  getDOM() {
  // 方式一: 在react元素上绑定ref字符串 - 这种方式react已经不推荐了
  // console.log(this.refs.http)
  
  // 方式二: 提前创建好ref对象, createRef(), 将创建出来的对象绑定到元素(推荐)
  // console.log(this.titleRef.current)
  
  // 方式三: 传入一个回调函数, 在对应的元素被渲染之后, 回调函数被执行, 并且将元素传入(16.3之前的版本)
  // console.log(this.titleEl)
  }
  <h3 ref="http">大大怪将军</h3>
  <h3 ref={this.titleRef}>小小怪下士</h3>
  <h3 ref={el => this.titleEl = el}>瑞克</h3>
  <button onClick={() => this.getDOM()}>获取DOM</button>
  ```

* ref获取组件实例 -- `createRef`

  ```jsx
  import React, { PureComponent, createRef } from 'react'
  
  constructor() {
      super()
      this.state = {}
      this.HWRef = createRef()
  }
  
  getComponent() {
      console.log(this.HWRef.current)
      this.HWRef.current.test()
  }
  
  <HelloWorld ref={this.HWRef} />
  <button onClick={() => this.getComponent()}>获取组件实例</button>
  ```

* ref获取函数组件 -- 函数式组件是没有实例的，所以无法通过ref获取他们的实例 -- `React.forwardRef`

  ```jsx
  import React, { PureComponent, createRef, forwardRef } from 'react'
  
  const HelloWorld = forwardRef(function(props, ref) {
    return (
      <div>
        <h2 ref={ref}>函数组件</h2>
        <h4>大大怪将军</h4>
      </div>
    )
  })
  constructor() {
      super()
      this.state = {}
      this.HWRef = createRef()
  }
  
  getComponent() {
      console.log(this.HWRef.current)
  }
  
  render() {
      return (
        <div>
          <HelloWorld ref={this.HWRef} />
          <button onClick={() => this.getComponent()}>获取DOM</button>
        </div>
      )
  }
  ```

  



## 七.性能优化:React的diff算法和key的作用

* React的渲染流程

  * 在render函数中返回jsx, jsx会创建出`ReactElement`对象(通过React.createElement的函数创建出来的)
  * `ReactElement`最终会形成一颗树结构, 这颗树结构就是vDOM
  * React会根据这样的vDOM渲染出真实DOM

* React更新流程

  * props/state发生改变
  * render函数重新执行
  * 产生新的DOM树结构
  * 新旧DOM树 进行diff算法
  * 计算出差异进行更新
  * 最后更新到真实DOM

  ```js
  什么是diff算法?
      diff算法并非React独家首创,但是React针对diff算法做了自己的优化,使得时间复杂度优化成了O(n)
  对比两颗树结构,然后帮助我们计算出vDOM中真正变化的部分,并只针对该部分进行实际的DOM操作,而非渲染整个页面,从而保证了每次操作后页面的高效渲染。
  ```

* React在props或state发生改变时，会调用React的render方法，会创建一颗不同的树

* React需要基于这两颗不同的树之间的差别来判断如何有效的更新UI

* 如果一棵树参考另外一棵树进行完全比较更新，那么即使是最先进的算法，该算法的**复杂程度为 O(n³)**，其中 n 是树中元素的数量

* 如果在 React 中使用了该算法，那么展示 1000 个元素所需要执行的计算量将在十亿的量级范围

* 这个开销太过昂贵了，于是，React对这个算法进行了优化，**将其优化成了O(n)**

  * 同层节点之间相互比较，不会垮节点比较(一旦某个节点不同,那么包括其后代节点都会被替换)

    ![Snipaste_2022-09-02_15-53-43](E:\Typora-文件\Typora图片位置\Snipaste_2022-09-02_15-53-43.png)

  * 不同类型的节点，产生不同的树结构(当根节点为不同类型的元素时，React 会拆卸原有的树并且建立起新的树)

  * 开发中，可以通过key属性标识哪些子元素在不同的渲染中可能是不变的

* 在遍历列表时，总是会提示一个警告，让我们加入一个key属性，当子元素拥有 key 时，React 使用 key 来匹配原有树上的子元素以及最新树上的子元素。

  * 在最后位置插入数据 -- 这种情况，有无key意义并不大
  * 在前面插入数据 -- 这种做法，在没有key的情况下，所有的li都需要进行修改
  * 在中间插入元素 -- 新增2014, key为2016元素仅仅进行位移，不需要进行任何的修改

  ```jsx
  <ul>
    <li key="2015">Duke</li>
    <li key="2016">Villanova</li>
  </ul>
  
  <ul>
    <li key="2015">Duke</li>
    <li key="2014">Connecticut</li>
    <li key="2016">Villanova</li>
  </ul>
  ```

  



# Day05 作业布置

## 一. 完成课堂所有的代码





## 二. 什么是受控组件和非受控组件，如何使用？

* 受控组件

  * 在 React 中，可变状态通常保存在组件的 state 属性中，并且只能通过使用 setState()来更新
  * 我们将两者结合起来，使React的state成为“唯一数据源”
  * 渲染表单的 React 组件还控制着用户输入过程中表单发生的操作
  * 被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”

  ```jsx
  this.state = {
    message: ""
  }
  changeInput(event) {
    console.log(event.target.value)
    this.setState({ message: event.target.value })
  }
  
  render(){
     <input type="text" value={message} onChange={(event) => this.changeInput(event)} />
  }
  ```

* 非受控组件

  * 在受控组件中，表单数据是由 React 组件来管理的
  * 非受控组件中，表单数据将交由 DOM 节点来处理

  ```jsx
  this.messageRef.current.value
  
  // 在非受控组件中通常使用defaultValue来设置默认值
  render(){
      <input type="text" defaultValue={message} ref={this.messageRef} />
  }
  ```





## 三. 什么是高阶组件？高阶组件在React开发中起到什么作用？

* 高阶函数: (满足一下调教之一) -- filter、map、reduce都是高阶函数
  * 接受一个或多个函数作为输入
  * 输出一个函数
* 高阶组件: Higher-Order Components，简称为 HOC
  * 高阶组件是参数为组件，返回值为新组件的函数 -- 就是传入一个组件,对这个组件进行一些功能的增强,在返回出来新的组件
  * 注意: 首先 高阶组件 本身不是一个组件，而是一个函数 其次，这个函数的参数是一个组件，返回值也是一个组件
  * HOC 是 React 中用于复用组件逻辑的一种高级技巧。HOC 自身不是 React API 的一部分，它是一种基于 React 的组合特性而形成的设计模式

- 高级组件应用的场景
  - props的增强
  - 利用高阶组件来共享Context
  - 渲染判断鉴权
  - 生命周期劫持
  - ....



## 四. 什么是Fragment，有什么作用？

- Fragment 允许将子列表分组，而无需向 DOM 添加额外节点；
- 它的简写看起来像空标签  <> </>
- 如果我们需要在Fragment中添加key，那么就不能使用短语法



## 五. 什么是React的严格模式，在开发中有什么作用？

严格模式

- StrictMode 是一个用来突出显示应用程序中潜在问题的工具：
- 与 Fragment 一样，StrictMode 不会渲染任何可见的 UI；
- 它为其后代元素触发额外的检查和警告；

严格模式作用

- 识别不安全的生命周期：
- 使用过时的ref API
- 检查意外的副作用 这个组件的constructor会被调用两次； 这是严格模式下故意进行的操作，让你来查看在这里写的一些逻辑代码被调用多次时，是否会产生一些副作用； 在生产环境中，是不会被调用两次的；
- 使用废弃的findDOMNode方法 在之前的React API中，可以通过findDOMNode来获取DOM，不过已经不推荐使用了，可以自行学习演练一下
- 检测过时的context API 早期的Context是通过static属性声明Context对象属性，通过getChildContext返回Context对象等方式来使用Context的



## 六. React中如何实现过渡动画？常见的过渡动画组件有哪些？

- React社区为我们提供了react-transition-group用来完成过渡动画

常见的过渡动画组件

- Transition   在前端开发中，一般是结合CSS来完成样式，所以比较常用的是CSSTransition；
- CSSTransition   在前端开发中，通常使用CSSTransition来完成过渡动画效果
- SwitchTransition   两个组件显示和隐藏切换时，使用该组件
- TransitionGroup   将多个动画组件包裹在其中，一般用于列表中元素的动画；







# Day06 作业布置

## 一. 完成课堂所有的代码







## 二. React中编写CSS的方式有哪些？各自有什么优缺点？







## 三. styled-components有哪些技术特点？可以完成哪些功能？







## 四. 什么是redux？redux的核心思想是什么？核心的原则有哪些?(面试)







## 五. redux如何进行文件，每个文件是什么作用？







## 六. redux如何和react结合在一起？如何共享数据，如何进行action操作？

* connect函数
* 按照目前使用的方式总结一下







# Day07 作业布置

## 一. 完成课堂所有的代码

- 重点
  - redux进行异步操作 ---> 通过中间件 ---> redux-thunk
  - 工具redux-toolkit的使用
  - connect函数的实现原理

## 二. redux中如何进行异步的操作？和同步操作有什么区别？

- 通过中间件
  - redux-thunk
  - redux-saga
- redux中的同步操作
  - 执行了dispatch函数之后,对应的reducer函数收到action对象后立即得到执行,reducer执行完了之后,state立即就改变了,此时store.getState函数,取到的是最新的值
- redux的异步操作
  - 原则上redux并没有提供异步action的处理方案,异步action需要依赖第三方的中间件解决
  - dispatch一个异步函数,目标state不会立即响应,而是要看异步函数内部的逻辑,来决定state什么时候响应

## 三. redux中如何进行reducer的拆分？拆分的原理和本质是什么？

- 主要利用模块化的思想,将不同的数据拆分到不同的模块
- 每一模块都有自己的目录结构
  - reducer ---> 接受action对象,返回最新的state
  - constants ---> 定义常量数据
  - actoinCreator ---> 定义创建action对象的函数
  - index ---> 导出reducer
- store中的index文件
  - 合并reducer,导出store实例

## 四. 什么是Redux Toolkit？核心API有哪些？并且说出他们的作用。

- configureStore
  - 包装createStore,同时提供简化的配置选项和良好的默认值
  - 自动组合单独的slice reducer
  - 可以添加任何中间件
    - 默认包含redux-thunk,并启用Redux-DevTools调试工具
- createSlice 
  - 接受一个具有render函数的对象
  - 可以配置切片名称
  - 初始状态值
  - 自动 生成切片,并带有相应的actions
- createAsyncThunk
  - 接受一个动作类型字符和一个返回承诺的函数
  - 生成一个pending/fulfilled/rejected基于该承诺分配动作类型的Thunk

## 五. 总结Redux的使用步骤，包括原始Redux用法和RTK用法。（重要）

- 原始的Redux的使用步骤
  - 先从react-redux中导入Providre包裹根组件
  - 将导出的store绑定到Provider组件的store属性中
  - 创建store,目录结构
    - actionCreator ---> 创建action对象
    - constant  ---> 定义常量数据
    - reducer ---> 处理action对象,返回最新的state
    - index ---> 人口文件,创建store,使用中间件
  - 组件中的使用方式
    - 定义函数 ---> mapStateToProps ---> 将store中的数据映射要组件的props中
    - 定义函数 --->  mapDispatchToProps ---> 将dispatch的操作映射到props中
    - 从react-redux中导入高阶组件对要导出的组件进行包裹,并把定义的函数传入connect函数
    - 组件触发相应的事件,dispatch相应的对象,store中的数据改变,组件重新渲染
- RTK用法
  - 先从react-redux中导入Providre包裹根组件
  - 将导出的store绑定到Provider组件的store属性中
  - 创建store,目录结构:
    - index.js ---> 入口文件  ---> 创建和配置store ---> 主要是合并render
    - features ---> 要管理的数据模块
      - 使用createSliceAPI创建一个slice对象
      - name ---> 配置slice对象的名称
      - initialState ---> 定义初始值
      - reducer ---> 定义reduce函数的对象
      - 导出slice对象的actions---> 组件中使用或者自己内部使用,
      - 导出slice对象的reducer---> index文件合并reducer





# Day08 作业布置

## 一. 完成课堂所有的代码







## 二. React Router6的基本创建过程是什么？进行步骤总结。

* 安装react-router-dom --  **npm install react-router-dom**

* 选择路由模式 BrowserRouter使用**history模式** / HashRouter使用**hash模式**

  ```jsx
  <HashRouter>
      <App />
  </HashRouter>
  ```

* 通过Routes包裹所有的Route, 在其中匹配路由

* Route用于路径的匹配

  * path属性：用于设置匹配到的路径
  * element属性：设置匹配到路径后，渲染的组件  --  Router5.x使用的是component属性

* 路由跳转 -- Link组件 / NavLink组件

  * to属性 -- 用于设置跳转到的路径

* 路由重定向 -- Navigate

* Not Found页面配置 -- path="*"

  ```jsx
  <Link to="/home">首页</Link>
  <Link to="/about">关于</Link>
  <Routes>
      <Route path="/" element={<Navigate to="/home" />} />
      {/**Home页面*/}
      <Route path="/home" element={<Home />}>
        <Route path="/home" element={<Navigate to="/home/homebanner" />} />
        <Route path="/home/homebanner" element={<HomeBanner />} />
        <Route path="/home/homerecommend" element={<HomeRecommend />} />
      </Route>
      <Route path="/about" element={<About />}></Route>
      <Route path="*" element={<NotFount />}></Route>
  </Routes>
  ```





## 三. React Router6的路由嵌套如何配置？Outlet的作用是什么？

```jsx
// Home 页面
<Link to="/home/homebanner">轮播</Link>
<Link to="/home/homerecommend">推荐</Link>

<Outlet/>
```

* Outlet -- Outlet组件用于在父路由元素中作为子路由的占位元素, 类似于Vue中的 router-view





## 四. React Router6如何传递参数？如何在组件中获取参数？

* 路由参数传递有两种方式: 1. 动态路由的方式 2. search传递参数

* 动态路由

  ```jsx
  <Link to="/user/9978">用户</Link>
  <Route path="/user/:id" element={<User />}></Route>
  ```

  ```jsx
  // 获取动态路由参数 -- 需要通过 useParams 只能在函数式组件中使用
  import { useParams } from "react-router-dom";
  export function User() {
    const params = useParams()
    return (
      <div>
        <h4>User Page</h4>
        <h4>id: {params.id}</h4>
      </div>
    )
  }
  ```

* search传递参数

  ```jsx
  <Link to="/user?name=大大怪将军&age=19"">用户</Link>
  ```

  



## 五. 类组件无法直接使用navigate、location等参数，应该如何进行操作？

```jsx
import { useLocation, useNavigate, useParams, useSearchParams } from "react-router-dom";

function withRouter(WrapperComponent) {
  return function(props){
    // 1.导航
    const navigate = useNavigate()

    // 2.动态路由的参数: /detail/:id
    const params = useParams()

    // 3.查询字符串的参数: /user?name=why&age=18
    const location = useLocation();
    const [searchParams] = useSearchParams();
    const query = Object.fromEntries(searchParams);

    const router = {navigate, params, location, query}

    return <WrapperComponent {...props} router={router} />
  }
}
export default withRouter
```

```jsx
import React, { PureComponent } from 'react'
import withRouter from "../hoc/with_router"

export class About extends PureComponent {
  navigateTo(path) {
    const { navigate } = this.props.router
    navigate(path)
  }
  render() {
    const { query } = this.props.router
    return (
      <div>
        <h3>About Page</h3>
        <h4>name: {query.name}-age: {query.age}</h4>
      </div>
    )
  }
}
export default withRouter(About)
```



## 六. React Router6如何进行路由配置？如何配置路由的懒加载？

```js
// 在单独的router/index.js文件中

// 路由懒加载/按需加载/异步加载 ? 
// 这样暂时不会显示,因为是异步的要单独下载,需要加载一个loading动画React提供的Suspense组件
const Order = React.lazy(() => import("../page/Order"));
const User = React.lazy(() => import("../page/User"));

const router = [
    {
        path: '/',
        element: <Navigate to="/home" />,
    },
    {
        path: "/home",
        element: <Home />,
        children: []
    }
]
export default router
```

```jsx
<HashRouter>
  <Suspense fallback={<h4>Loading~~~~</h4>}>
    <App />
  </Suspense>
</HashRouter>
```





## 七. 什么是Hooks？和传统的函数式组件有什么区别？和类组件有什么区别？(面试)

* **Hook指的类似于useState、useEffect这样的函数, Hooks是对这类函数的统称**

* 首先需要了解函数式组件与类组件的优缺点

* 类组件可以定义自己的state,并且可以保存自己内部的状态

  * 函数式组件不能定义自己的状态的, 因为函数每次调用都会产生新的临时变量

* 类组件有自己的生命周期 -- 而函数式组件没有

* 类组件在状态改变是会重新执行render函数

  * 函数式组件时不会重新渲染的, 如果重新渲染, 整个函数会被重新执行, 相应的状态也会被重新赋值

* 同时类组件也有自己的缺点

  * 随着业务的增多,类组件会变得越来越复杂
  * 复用其中的状态也会很艰难,有时需要通过一些高阶组件

* **Hooks**可以让我们在不编写class的情况下使用state以及其他的React特性

  * Hook只能在函数组件中使用，不能在类组件
  * 通过Hook可以在函数式组件中 定义自己的状态 完成类似于class组件中的生命周期功能

  ```jsx
  // 类组件实现计数器
  import React, { PureComponent } from 'react'
  
  export class CounterClass extends PureComponent {
    constructor() {
      super()
      this.state = {
        counter: 100
      }
    }
    subCounter() {
      this.setState({counter: this.state.counter - 1})
    }
    addCounter() {
      this.setState({counter: this.state.counter + 1})
    }
    render() {
      const { counter } = this.state
      return (
        <div>
          类组件实现计数器
          <h2>counter: {counter}</h2>
          <button onClick={() => this.subCounter(1)}>-1</button>
          <button onClick={() => this.addCounter(1)}>+1</button>
        </div>
      )
    }
  }
  
  export default CounterClass
  ```

  ```jsx
  // Hooks实现计数器
  import React, { memo, useState } from 'react'
  const CounterHooks = memo(() => {
    let [counter, setCounter] = useState(100)
    return (
      <div>
        Hooks
        <h2>counter: {counter}</h2>
        <button onClick={e => setCounter(counter - 1)}>-1</button>
        <button onClick={e => setCounter(counter + 1)}>+1</button>
      </div>
    )
  })
  
  export default CounterHooks
  ```

  





# Day09 作业布置

## 一. 完成课堂所有的代码









## 二. 什么是Hooks？和传统的函数式组件有什么区别？和类组件有什么区别？









## 三. 总结常见的Hooks，以及说明它们的作用。（重点state、effect）









## 四. useEffect在使用上有哪里方式和注意事项？









## 五. useMemo和useCallback有什么区别？









## 六. 什么是闭包陷阱？如何解决出现的闭包陷阱？（面试题）









## 七. Redux中有哪些Hooks？如何使用对应的Hooks？









## 八. React18新增哪些Hooks，这些Hooks有什么作用？



##  



# Day10 作业布置

## 一. 完成课堂所有的代码

- 重点
  - redux中的hooks
  - 服务端渲染的概念
  - 项目的初始化和搭建过程

## 二. Redux中有哪些Hooks？如何使用对应的Hooks？

- useSelector
  - 可以将redux中的数据映射到组件中
  - 第一个参数是一个回调函数
    - 函数参数是state
    - 返回一个对象,对象中包含state中的数据
  - 第二个参数是showEqual
    - 作用 ---> 只有当前获取的对应数据改变后,对应的组件才会重新渲染
- useDispatch
  - 没有参数
  - 返回一个diapatch函数 ---> 可以传入action对象

## 三. React18新增哪些Hooks，这些Hooks有什么作用？

- useId
  - 用于生产横跨服务端和客户端的稳定的唯一的ID的同时避免hydration不匹配的hook
- useTransition
  - 降低某部分任务的更新优先级,先完成优先级较高的任务后执行
- useDeferredValue
  - 接受一个值,并返回该值的 新副本,该副本将在优先级较高的任务完成后执行

## 四. 项目初始化的流程包括哪些操作？需要进行哪些常见的配置？

- 项目初始化的流程
  - 使用React脚手架创建一个初始化的项目
  - 删除不需要的文件
  - 更换网站图标,更换网站的标题
  - 按不同的功能模块在src文件夹下完善项目的目录结构
  - 搭建基础的页面,配置路由,选择路由模式
  - 创建保存项目数据的store
  - 二次封装axios,配置BaseUrl,以便发送网络请求

- 常见的配置
  - 配置别名
  - 使用craco工具方便对webpack进行配置

## 五. 手动配置Redux，包括普通的方式和RTK的方式。

- 配置redux的普通方式
  - 每一个模块设置以下文件目录
    - index.js  ---> 文件入口
    - createActions.js  ---> 创建action对象
    - reducer.js ---> 定义初始化数据,处理提交的action对象
    - constants.js ---> 定义常量数据
- 配置redux的RTK方式
  - 使用configStore创建一个store
    - 传入对象类型,对象中是不同模块的reducer
  - 在不同的模块使用createSilce定义自己的初始化数据,reduce,action
- 将配置的store导出
- 在index.js文件中从react-redux导出Provider组件
- 用Provier组件包裹根组件,在store属性中传入我们自己创建的store

## 六. 完成Axios库的二次封装，并且说明封装的好处。

- 使用类进行封装
- 类封装的好处
  - 扩展性好

## 七.对SSR内容进行总结(SPA/SSR/同构/hydration)

- SPA
  - Single Page Application, 单页面应用
  - 一种Web应用程序,它只需要将单个页面夹加载到浏览器中
  - 特点
    - 一旦页面加载完成,SPA不会因为用户的操作而进行页面的重新加载或跳转
    - 利用路由机制实现页面内容的变换
  - 优点
    - 用户体验好、快、内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染，SPA 相对服务器压力小
    - 前后端职责分离，架构清晰，前后端进行交互逻辑，后端负责数据处理
  - 缺点
    - 初次加载耗时多：为实现单页 Web 的应用功能及显示效果，需要在加载页面的时候将JavaScript、CSS统一加载，部分页面按需加载
    - SEO难度较大：由于所有的内容都在一个页面中动态替换显示，所以在SEO上其有着天然的弱势。
    - 如果你使用了AJAX进行局部刷新，浏览过的内容就不能用后退按钮重现了。
- SSR
  - Server Side Rendering, 服务端渲染的简称
  - 在服务器端生成完整的HTML页面结构,返回给浏览器进行渲染
  - 特点
    - 在服务端生成html网页的dom元素
    - 客户端（浏览器）只负责显示dom元素内容
  - 优点
    - 有利于SEO，网站通过href的url将搜索引擎直接引到服务端，服务端提供优质的网页内容给搜索引擎。
  - 缺点
    - 需要消耗一定的服务器资源
- 同构应用
  - 一套代码既可以在服务端运行又可以在客户端运行,我们称为同构应用
  - 同构是一种SSR的形态,是现代SSR的一种表现形式
- hydration
  - SSR引申出来的概念
  - SSR ----> 服务端将生成好的HTML页面发送浏览器进行展示,这其中是没有js逻辑的,比如事件的绑定,也就是不能和用户进行交互的
  - 在服务端渲染的时候,UI框架(React/Vue)会记录SSR渲染的页面的内部特征,然后将这个特只能特征映射到我们要在浏览器展示的页面上,它会让我们的页面具有交互性,这个过程称之为Hydration





# Day11 作业布置

## 一. 完成上课所有的代码练习









## 二. 自己完成部分项目的样式（自己编写，不要拷贝我的）









## 三. 如何引入MUI库，并且课下尝试引入AntDesignUI库。

* 自己尝试







## 四. 从服务器请求的数据保存在redux和保存在页面中有什么区别？保存在redux中的使用流程是什么？

* 方式一：保存在页面中
* 方式二：保存在redux中







## 五. 首页区域封装的思路是什么？包括哪几部分？如何进行复用？















# Day12 作业布置

## 一. 完成上课所有的代码练习









## 二. 首页区域封装的思路是什么？包括哪几部分？如何进行复用？









## 三. 封装滚动的ScrollView，实现可以滚动到其中任意一个元素中。









## 四. 自己完成CSS样式的编写（多练习、多总结，做到任何样式都可以编写即可）







































































































































































































































































































































































































































































































































































































































































































































































































































































































































































