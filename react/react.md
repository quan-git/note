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
