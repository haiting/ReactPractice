# ReactPractice
React 入门实例教程
react介绍：
React 起源于 Facebook 的内部项目，因为该公司对市场上所有 <a href="http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html" target="_blank">JavaScript MVC 框架</a> 框架，都不满意，就决定自己写一套，用来架设 <a href="https://instagram.com/" target="_blank">Instagram</a> 的网站。做出来以后，发现这套东西很好用，就在2013年5月<a href="http://facebook.github.io/react/blog/2013/06/05/why-react.html" target="_blank">开源</a>了。
安装
React Demos 已经自带 React 源码，不用另外安装，只需把这个库拷贝到你的硬盘就行，也可以到官网下载。

```
    $ git clone https://github.com/haiting/ReactPractice.git
```

如果你没安装 git,直接下载<a href="https://github.com/ruanyf/react-demos/archive/master.zip" target="_blank">zip 压缩包</a>
下面要讲解的12个例子在各个 Demo 子目录，每个目录都有一个 index.html 文件，在浏览器打开这个文件（大多数情况下双击即可），就能立刻看到效果。

需要说明的是，React 可以在浏览器运行，也可以在服务器运行，但是本教程只涉及浏览器。一方面是为了尽量保持简单，另一方面 React 的语法是一致的，服务器的用法与浏览器差别不大。Demo13 是服务器首屏渲染的例子，有兴趣的朋友可以自己去看源码。
一、HTML 模板

```
    <!DOCTYPE html>
    <html>
      <head>
        <script src="../build/react.js"></script>
        <script src="../build/react-dom.js"></script>
        <script src="../build/browser.min.js"></script>
      </head>
      <body>
        <div id="example"></div>
        <script type="text/babel">
          // ** Our code goes here! **
        </script>
      </body>
    </html>
```
上面代码有两个地方需要注意。首先，最后一个 "script" 标签的 type 属性为 text/babel 。这是因为 React 独有的 JSX 语法，跟 JavaScript 不兼容。凡是使用 JSX 的地方，都要加上 type="text/babel" 。

其次，上面代码一共用了三个库： react.js 、react-dom.js 和 Browser.js ，它们必须首先加载。其中，react.js 是 React 的核心库，react-dom.js 是提供与 DOM 相关的功能，Browser.js 的作用是将 JSX 语法转为 JavaScript 语法，这一步很消耗时间，实际上线的时候，应该将它放到服务器完成。
二、ReactDOM.render()
    ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。

```
    ReactDOM.render(
        <h1>Hello,React framework!</h1>,
        document.getElementById('demo2')
    );
```

先写HTML元素标签，标签包着的是需要写的内容，逗号不要漏，然后获取需要把内容渲染过去的元素
    上面代码将一个 h1 标题，插入 demo2 节点,代码结果如下

```
    <p id="demo2">
        <h1 data-reactroot="">Hello,React framework!</h1>
    </p>
```
三、JSX 语法
    上一节的代码， HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写

```
    var namesArr = ['React', 'FrontEnd', 'Framework', 'Javascript'];
    ReactDOM.render(
        <ol>
          {
            namesArr.map(function (name) {
              return <li>Hello,{name}!</li>
            })
          }
        </ol>,
        document.getElementById('demo3')
      );
```

上面代码体现了JSX的与本语法规则：遇HTML标签（以 < 开头），就用HTML规则解释；
    遇到代码块（以 { 开头），就用JavaScript规则解释。代码运行结果如下：

```
    <div id="demo3">
        <ol data-reactroot="">
            <li><!-- react-text: 3 -->Hello,<!-- /react-text --><!-- react-text: 4 -->React<!-- /react-text --><!-- react-text: 5 -->!<!-- /react-text -->
            </li>
            <li><!-- react-text: 7 -->Hello,<!-- /react-text --><!-- react-text: 8 -->FrontEnd<!-- /react-text --><!-- react-text: 9 -->!<!-- /react-text -->
            </li>
            <li><!-- react-text: 11 -->Hello,<!-- /react-text --><!-- react-text: 12 -->Framework<!-- /react-text --><!-- react-text: 13 -->!<!-- /react-text -->
            </li>
            <li><!-- react-text: 15 -->Hello,<!-- /react-text --><!-- react-text: 16 -->Javascript<!-- /react-text --><!-- react-text: 17 -->!<!-- /react-text -->
            </li>
        </ol>
    </div>
```

JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员

```
    var htmlArr = [
        <li>Hello, React!</li>,
        <li>React is awesome!</li>
    ]
    ReactDOM.render(
        <ol>
          {htmlArr}
        </ol>,
        document.getElementById('demo3-1')
    )
```

上面代码的arr变量是一个数组，结果 JSX 会把它的所有成员，添加到模板，运行结果如下。

```
    <div id="demo3-1">
        <ol data-reactroot="">
            <li>Hello, React!</li>
            <li>React is awesome!</li>
        </ol>
    </div>
```

四、组件
    React 允许将代码封装成组件，然后像插入普通HTML标签一样，在网页中插入这个组件。

```
    React.createClass 方法用于生成一个组件软件。

    var HelloWordValue = React.createClass({
        render: function () {
          return <h1>Hello, {this.props.value}</h1>;
        }
    })
    ReactDOM.render(
        <HelloWordValue value = 'study React'/>,
        document.getElementById('demo4')
    )
```

上面代码中，变量 HelloWordValue 就是一个组件。模板插入 <HelloWordValue />时,会自动生成 HelloWordValue 的一个实例。所有的组件类都必须有自己的 ```render ``` 方法,用于输出组件。
    （下文的"组件"都指组件类的实例）。
    注意：组件类的第一个字母必须大写，否则会报错。
         组件类只能包含一个顶层标签，否则会报错。

组件的用法与原生的HTML标签完全一致，可以任意添加属性。

```
    比如 <HelloWordValue value = 'study React'/>,就是HelloWordValue 组件加入一个 value属性，值为 study React。
```
属性获取：组件的属性通过组件类的 this.props 对象上获取。运行结果：
```
    <div id="demo4">
        <h1 data-reactroot=""><!-- react-text: 2 -->Hello, <!-- /react-text --><!-- react-text: 3 -->study React<!-- /react-text -->
        </h1>
    </div>
```

五、this.props.children
    this.props 对象的属性与组件的属性一一对应，但是有一个例外，就是 this.props.children 属性。它表示组件的所有子节点

```
    var NodeList = React.createClass({
      render: function () {
        return (
          <ol>
            {
              React.Children.map(this.props.children, function (name) {
                return <li>{name}</li>;
              })
            }
          </ol>
        )
      }
    })

    ReactDOM.render(
      <NodeList>
        <span>this.props.children</span>
        <span>this.props.children</span>
        <span>this.props.children</span>
      </NodeList>,
      document.getElementById('demo5')
    );
```
这里需要注意， this.props.children 的值有三种可能：如果当前组件没有子节点，它就是 undefined ;如果有一个子节点，数据类型是 object ；如果有多个子节点，数据类型就是 array 。所以，处理 this.props.children 的时候要小心。

React 提供一个工具方法 React.Children 来处理 this.props.children 。我们可以用 React.Children.map 来遍历子节点，而不用担心 this.props.children 的数据类型是 undefined 还是 object。更多的 React.Children 的方法，请参考<a href="https://facebook.github.io/react/docs/top-level-api.html#react.children" target="_blank">官方文档</a>。

六、PropTypes
    组件的属性可以接受任意值，字符串、对象、函数等等都可以。有时，我们需要一种机制，验证别人使用组件时，提供的参数是否符合要求。
    组件类的PropTypes属性，就是用来验证组件实例的属性是否符合要求

```
    var PageTitle = React.createClass({
      propTypes: {
        title: React.PropTypes.string.isRequired,
      },
      render : function () {
        return <h1>{this.props.title}</h1>;
      }
    });
```
上面的PageTitle组件有一个title属性。PropTypes 告诉 React，这个 title 属性是必须的，而且它的值必须是字符串。
```
    var titleText = 123;
    ReactDOM.render(
      <PageTitle title={titleText}/>,
      document.getElementById('demo6')
    );
```

现在，我们设置 title 属性的值是一个数值。title属性就通不过验证了。控制台会显示一行错误信息。
更多的PropTypes设置，可以查看<a href="http://facebook.github.io/react/docs/reusable-components.html" target="_blank">官方文档</a>。

getDefaultProps 方法可以用来设置组件属性的默认值。

```
    var DefaultTitle = React.createClass({
      getDefaultProps: function () {
        return {
          title: 'Hello DetfaultProps'
        };
      },
      render: function () {
        return <h1>{this.props.title}</h1>;
      }
    });

    ReactDOM.render(
      <DefaultTitle/>,
      document.getElementById('demo6-1')
    );
```

七、获取真实的DOM节点
组件并不是真实的 DOM 节点，而是存在于内存之中的一种数据结构，叫做虚拟 DOM （virtual DOM）。只有当它插入文档以后，才会变成真实的 DOM 。根据 React 的设计，所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上，这种算法叫做 <a href="http://calendar.perfplanet.com/2013/diff/" target="_blank">DOM diff</a> ，它可以极大提高网页的性能表现。

但是，有时需要从组件获取真实 DOM 的节点，这时就要用到 ref 属性

```
    var MyComponent = React.createClass({
      handleClick: function () {
        this.refs.myTextInput.focus();
      },
      render: function () {
        return (
          <div>
            <input type="text" ref="myTextInput" />
            <input type="button" value="Focus on the text input" onClick={this.handleClick} />
          </div>
        );
      }
    });
    ReactDOM.render(
      <MyComponent />,
      document.getElementById('demo7')
    );
```

上面代码中，组件 MyComponent 的子节点有一个文本输入框，用于获取用户的输入。这时就必须获取真实的 DOM 节点，虚拟 DOM 是拿不到用户输入的。为了做到这一点，文本输入框必须有一个 ref 属性，然后 this.refs.[refName] 就会返回这个真实的 DOM 节点。

需要注意的是，由于 this.refs.[refName] 属性获取的是真实 DOM ，所以必须等到虚拟 DOM 插入文档以后，才能使用这个属性，否则会报错。上面代码中，通过为组件指定 Click 事件的回调函数，确保了只有等到真实 DOM 发生 Click 事件之后，才会读取 this.refs.[refName] 属性。

React 组件支持很多事件，除了 Click 事件以外，还有 KeyDown 、Copy、Scroll 等，完整的事件清单请查看<a href="http://facebook.github.io/react/docs/events.html#supported-events" target="_blank">官方文档</a>。

八、this.state
组件免不了要与用户互动，React 的一大创新，就是将组件看成是一个状态机，一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染 UI

```
  var LikeComponentButton = React.createClass({
      getInitialState: function () {
        return {liked: false};
      },
      handleClick: function (event) {
        this.setState({liked: !this.state.liked});
      },
      render: function () {
        var text = this.state.liked? 'like': 'have\'t liked';
        return (
          <p onClick={this.handleClick}>
            You {text} this. Click to toggle.
          </p>
        );
      }
    });

    ReactDOM.render(
      <LikeComponentButton />,
      document.getElementById('demo8')
    )  
```

上面代码是一个 LikeButton 组件，它的 getInitialState 方法用于定义初始状态，也就是一个对象，这个对象可以通过 this.state 属性读取。当用户点击组件，导致状态变化，this.setState 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。

由于 this.props 和 this.state 都用于描述组件的特性，可能会产生混淆。一个简单的区分方法是，this.props 表示那些一旦定义，就不再改变的特性，而 this.state 是会随着用户互动而产生变化的特性。

九、表单
用户在表单填入的内容，属于用户跟组件的互动，所以不能用 this.props

```
   var InputBox = React.createClass({
      getInitialState: function () {
        return {value: 'input Form'};
      },
      handleChange: function (event) {
        this.setState({value: event.target.value});
      },
      render: function () {
        var value = this.state.value;
        return (
          <form>
            <input type="text" value={value} onChange={this.handleChange} />
            <p>{value}</p>
          </form>
        );
      }
    });

    ReactDOM.render(
      <InputBox />,
      document.getElementById('demo9')
    ); 
```

上面代码中，文本输入框的值，不能用 this.props.value 读取，而要定义一个 onChange 事件的回调函数，通过 event.target.value 读取用户输入的值。textarea 元素、select元素、radio元素都属于这种情况，更多介绍请参考<a href="http://facebook.github.io/react/docs/forms.html" target="_blank">官方文档</a>。

十、组件的生命周期
组件的<a href="https://facebook.github.io/react/docs/working-with-the-browser.html#component-lifecycle" target="_blank">生命周期</a>分成三个状态：

```
.Mounting：已插入真实 DOM
.Updating：正在被重新渲染
.Unmounting：已移出真实 DOM
```

React 为每个状态都提供了两种处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用，三种状态共计五种处理函数。

```
.componentWillMount()
.componentDidMount()
.componentWillUpdate(object nextProps, object nextState)
.componentDidUpdate(object prevProps, object prevState)
.componentWillUnmount()
```

此外，React 还提供两种特殊状态的处理函数。

```
.componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
.shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用
```

这些方法的详细说明，可以参考<a href="http://facebook.github.io/react/docs/component-specs.html#lifecycle-methods" target="_blank">官方文档</a>。

例子：
