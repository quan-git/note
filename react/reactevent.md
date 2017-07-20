# 事件处理
> 合成事件和原生事件 ?


> 自动绑定上下文和事件委托 ?


> 什么是原生事件 ?
# 点击事件
```
<script type="text/babel">
var HelloMessage = React.createClass({
  getInitialState: function() {
    return {value: 'Welcome to H5!'};
  },
  handleChange: function(event) {       //通过点击事件改变State的值来触发页面的渲染
    this.setState({value: '菜鸟教程'})
  },
  render: function() {
    var value = this.state.value;
    return <div>
            <button onClick={this.handleChange}>按钮</button>
            <h4>{value}</h4>
           </div>;
  }
});
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);
```
# 父组件
```
<script type="text/babel">
    var Content = React.createClass({     //子组件
        render: function() {
        return  <div>
                  <button onClick = {this.props.updateStateProp}>按钮</button>
                  <h4>{this.props.myDataProp}</h4>
               </div>
      }
    });
    var HelloMessage = React.createClass({   //父组件
       getInitialState: function() {
        return {value: 'Hello HTML5!'};
      },
      handleChange: function(event) {
        this.setState({value: '菜鸟在线'})
      },
      render: function() {
        var value = this.state.value;
        return <div>
                <Content myDataProp = {value}                 //这里调用了子组件并为其传prop值
                  updateStateProp = {this.handleChange}></Content>
               </div>;
      }
    });
    ReactDOM.render(
      <HelloMessage />,
      document.getElementById('example')
    );
    </script>
 ```
 
# 表单事件
 
 ```
    <script type="text/babel">
    var FormInput = React.createClass({
        submitHandler: function(event){
            event.preventDefault();
            var helloTo = ReactDOM.findDOMNode(this.refs.helloTo).value; //这里寻找所对应的表单并获取其值,refs是固定的
            alert(helloTo);
        },
        render: function(){
            return <form onSubmit={this.submitHandler}>
                <input type="text" ref="helloTo" defaultValue="Hello World!"/> //这里的ref是不可变的他与寻找的refs是对应的
                <br/>
                <button type="submit">Submit</button>
            </form>;
        }
    });
    ReactDOM.render(<FormInput></FormInput>, document.body);
 </script>
 ```
# React Components生命周期
```
React组件拥有简洁的生命周期API它仅仅提供你所需的方法
```

> React Components生命周期有三种状态:
```
Mounted:React Component被render解析,生成对应的DOM节点,并插入浏览器的DOM结构的过程这个过程结束就是这个组
        件被Mounted插入真实dom
Update:被mounted的React Component被重新render的过程 重新渲染
Unmounted:一个被mounted的React Component对应的DOM节点被从DOM结构中移除的这样一个过程。 已移除真实的DOM
```

> React为每个状态提供了俩种处理函数:
```
以will开头是在进入状态之前调用,did开头进入状态后调用
```

> 种5处理函数
```
1.组件加载:componentWillMount:
componentWillMount会在组件render之前执行，并且永远都只执行一次。由于这个方法始终只执行一次，所以如果在这里
定义了setState方法之后，页面永远都只会在加载前更新一次。

2.组件加载:componentDidMount
这个方法会在组件加载完毕之后立即执行。在这个时候之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()
来进行访问。如果你想和其他JavaScript框架一起使用，可以在这个方法中执行setTimeout, setInterval或者发送AJAX
请求等操作(防止异部操作阻塞UI)

3.组件更新:componentWillReceiveProps:
在组件接收到一个新的prop时被执行。这个方法在初始化render时不会被调用。旧的props可以通过this.props来获取。在
这个函数内调用this.setState()方法不会增加一次新的render.

4.组件更新:shouldComponentUpdate
返回一个布尔值。在组件接收到新的props或者state时被执行。在初始化时或者使用forceUpdate时不被执行。可以在你确认
不需要更新组件时使用。

5.

```
> 实例化 Mounted
```
<script type="text/babel">
      class Hello extends React.Component{   
        constructor(props){       //constructor(props, context) 构造器准许你设置实例的属性以及组件的姿态.
          super(props);
          alert("aaaaa")
        }
        componentWillMount(){      //componentWillMount该方法会在完成首次渲染之前被调用. 这也是在 render 方法调用彰可以修改组件 stats 的                                      最后一次机会. 它的存在仅仅是为了体现生命周期完整性, 是 createClass 的遗留物, 现在已经被 constructor                                      替代.
          alert('ComponentWillMount')
        }
        render(){                  //render在这里分创建一个虚拟 DOM, 用来表示组件的输出. 对于一个组件来说, render 是唯一一个必需的方法, 并                                      且有我特定的规则. render 方法需要满足下面几点:
          alert('render');
        return (
          <div>
            <h1>hello world!</h1>
          </div>
        )
        }
        componentDidMount(){        //componentDidMount在 render 方法成功调用并且真实的 DOM 已经被渲染之后, 可以在 componentDidMount                                         内部通过 ReactDOM.findDOMNode(this) 方法或是使用 ref 来访问它.
          alert("DidMount!")
        }
      }
      ReactDOM.render(<Hello />,
      document.getElementById('root'));
      </script>
```
