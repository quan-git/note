> getInitialState
```
Initial:最初的,字首的
在组件挂载之前调用一次返回值将会作为this.state的初始值
getInitialState: function() {
    return {liked: false};
  }
 ```
 >getDefaultProps
 ```
 在组件类创建的时候调用一次，然后返回值被缓存下来,设置props的默认值
 getDefaultProps : function () {
    return {
      title : 'Hello World'
    };
  }
  ```
  >propsTyps
  ```
  propTypes 对象允许验证传入到组件的props,验证传入的props是否符合要求
   propTypes: {
                    title: React.PropTypes.string.isRequired,
                }
  ```
  #组件的生命周期
  ```
  三个状态:
  Mountint:已插入真实DOM
  Updating:正在被重新渲染
  Unmounting:已移除真实DOM
  
  
  react为每个状态提供了俩种处理函数,will函数进入状态前调用,did函数进入状态之后调用三种状态共计五种处理函数
  mount:登上,安装
  componentWillMount():已插入真实dom之前
  componentDidMount():已插入真实dom之后
  componentWillUpdate(object nextprps,object nextState):组件更新之前
  componentDidUpdate(objcet nextprops ,object nextState):组件更新之后
  componentWillUnmount():移除之前
  
  
  倆种特殊状态处理函数:
  componentWillReceiveProps(object nextProps):已加载组件收到新的参数时调用
  shouldComponentUpdate(object nextProps,objct nextState):组件判断是否重新渲染时调用
