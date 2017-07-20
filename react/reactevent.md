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
