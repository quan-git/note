# 核心思想
```
核心思想 : 封装组件，各个组件维护自己的状态和UI，当状态变更，自动重新渲染整个组件。
基于这种方式的一个直观感受就是不再需要不厌其烦地来回查找某个DOM元素，然后操作DOM去
更改UI。
```

# 使用
```
页面中引入CDN(注意cdn的版本和这三个顺序)
<script src="http://cdn.bootcss.com/react/15.6.1/react.js"></script>
<script src="http://cdn.bootcss.com/react/15.6.1/react-dom.js"></script>
<script src="http://cdn.bootcss.com/babel-core/5.8.38/browser.js"></script>

react.js, 是react是核心库文件. react-dom.js, 是提供与DOM相关的功能, Browser.js的作
用是将JSX语法转为Javascript语法.
```
> 组件
```
应用都是建立在组件上,组件有俩个核心一个是state是组件的配置属性,在组建内部是不变的,在调用组建时
传入不同的属性来定制显示
```
> jsx
```
JSX是 React 一种特殊的语法，看起来像 HTML 和 JS 混杂在一起，是一种类XML语法。
传统MVC架构是将模板放到其他地方，比如script标签或者模板文件，再在JS中引用模板。而React认为，
组件才是王道。但是组件和模板是紧密相连的，组件模板和组件逻辑分离让问题复杂化了。于是就引入JSX，
把HTML模板直接嵌入JS代码中，这样就做到了模板与组件相关联。但是需要工具将JSX编译输出成JS代码才能使用。
```
> Virtual DOM
```
当组件 state 有更改时，React会自动调用组件的 render()方法重新渲染组件的UI。当然如果真的这样大面积
的操作DOM，性能是一个很大的问题，所以React实现了一个 虚拟DOM ，组件的DOM结构映射到这个虚拟DOM上，
React在这个虚拟DOM上实现了一个diff算法，当要更新组件时，会通过diff寻找到要变更的DOM节点，再把这个
合格修改更新到浏览器实际的DOM节点上，所以实际上不是重新渲染整个DOM树。虚拟DOM 是一个纯粹的JS数据结构，
性能比原生DOM快很多。
```
# 应用
> ReactDOM.reader()
```
用于将模板转为html语言并指定插入dom节点
```
# 设置标签样式
> 第一种设置css样式
```
render:function(){
return 
<div className></div>  //注意这里设置类名是className
}
```
> 第二种设置行内样式
```
render:function(){
return 
<div style={{width:'100px',height:'100px'}}></div>
}
```
> 第三种
```
render:function(){
return
var b={width:'100px',height:'100px'};
<div style={b}>
}
```
```
<script type="text/babel">   //这里的type必须为text/babel凡是有JSX语法都要这样写它解析JSX语法
   ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
  );
</script>
```
> react语法
```
<div id="example">
        <script type="text/babel">    //可以写在标签的任意位置
                var CommentBox = React.createClass({    //名字首字母必须大写一区分标签和jsx,在组件里注释无效
                    render: function(){
                        return (                       //只能返回一个元素不论有几个子元素
                           <div className="commentBox">
                            Hello world ! update!!!.
                            </div>
                        );
                    }
                })            //花括号后面不要加冒号
                ReactDOM.render(<CommentBox />, document.getElementById('example'));
        </script>
    </div>
```
> html和js混搭
```
<div id="example">
        <script type="text/babel">
                var names = ['ZhangShuai', 'WangSiqi', 'WangTongtong', 'LiRui'];
                ReactDOM.render(<div>{names.map(function(name){       //花括号里写js代码,ReactDOM可以是标签也是组件
                   return <h1>Hello, {name}!</h1>
                })}</div>,
                     document.getElementById('example'));
        </script>
    </div>
```


>  jsx可以接收一个数组,会展开数组的所有成员
```
 <div id="example">
        <script type="text/babel">
                var arr = [
                    <h1>欢迎来到北京菜鸟在线</h1>
                    <h2>我们现在学习是的React的语法知识</h2>
                ];
                ReactDOM.render(<div>{arr}</div>, document.getElementById('example'));
        </script>
    </div>
    
```
> 组件
```
   <div id="example">
        <script type="text/babel">
                var HMessage = React.createClass({
                    render: function(){
                        return <h1>Hello {this.props.name }</h1>
                    }
                });
                ReactDOM.render(<HMessage name="Joho" />, //注意给组件添加属性的时候class属性要写成className,for要写成htmlFor
                     document.getElementById('example'));
        </script>
    </div>
```
> this.props.children
```
    div id="example">
        <script type="text/babel">
            var NoteList = React.createClass({
                render: function(){
                    return (
                        <ol>
                        {
                            React.Children.map(this.props.children, function(child){  //this.props可以访问属性
                                return <li>{child}</li>
                            })
                        }
                        </ol>
                    );
                }
            });

            ReactDOM.render(
                <NoteList>
                <span>hello</span>    //写在模板标签中间可以是key,value也可以是标签但是写的格式不相同
                <span>world</span>
                </NoteList>,
                document.body
            );
        </script>
    </div>
    
```
  
>  属性可以接受任意值
```
   <div id="example">
        <script type="text/babel">
            var data = "BeiJing Cainiao";
            var Mytitle = React.createClass({
                propTypes: {                //因为属性可以接收任何值所以用这种机制来限制属性类型这里设置必须是字符串如果不是会在控制台
                    title: React.PropTypes.string.isRequired 输出错误效果显示
                }.
                render: function(){
                    return <h1>{this.props.title}</h1>
                }
            });
            ReactDOM.render(
                <Mytitle title={data} />.
                document.getElementById("example")
            );
        </script>
    </div>
```
    
    
>getDefaulteProp
    
    
```
    var data = "BeiJing Cainiao";
    var Mytitle = React.createClass({
        getDefaultProps: function(){     //用来设置属性默认值
           return{
                title: "HTML5"
            };
        },
        render: function(){
            return <h1>{this.props.title}</h1>
        }
    });
    ReactDOM.render(
        <Mytitle />
        document.getElementById("example")
    );
```
    
    
>this.state

```
 <div id="example">
        <script type="text/babel">
            var LikeButton = React.createClass({
                getInitialState: function(){    //用于定义初始化状态也就是一个对象这个对象可以通过this.state属性修改状态
                    return {liked: false};
                },
                handleClick: function(){        //注册点击事件并该变this.state.liked的值
                    this.setState({liked: !this.state.liked});
                },
                render: function(){
                    var text = this.state.liked ? 'like' : 'haven\'t liked';
                    return(
                        <p onClick={this.handleClick}>
                            You {text} this. Click to toggle.
                        </p>
                    );
                }
            });
            ReactDOM.render(
                <LikeButton />,
                document.getElementById('example')
            );
        </script>
    </div>
```
  
