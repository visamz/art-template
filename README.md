# This repo is a backup of [art-template v3.1.3](https://github.com/aui/art-template/tree/3.1.0) 
## artTemplate

新一代 javascript 模板引擎

##   目录

*	[特性](#特性)
*	[快速上手](#快速上手)
*	[模板语法](#模板语法)
*	[下载](#下载)
*	[方法](#方法)
*	[NodeJS](#nodejs)
*	[使用预编译](#使用预编译)
*	[更新日志](#更新日志)
*	[授权协议](#授权协议)

##	特性

1.	性能卓越，执行速度通常是 Mustache 与 tmpl 的 20 多倍（[性能测试](https://visamz.github.io/art-template/test/test-speed.html)）
2.	支持运行时调试，可精确定位异常模板所在语句（[演示](https://visamz.github.io/art-template/demo/debug.html)）
3.	对 NodeJS Express 友好支持
4.	安全，默认对输出进行转义、在沙箱中运行编译后的代码（Node版本可以安全执行用户上传的模板）
5.	支持`include`语句
6.	可在浏览器端实现按路径加载模板（[详情](#使用预编译)）
7.	支持预编译，可将模板转换成为非常精简的 js 文件
8.	模板语句简洁，无需前缀引用数据，有简洁版本与原生语法版本可选
9.	支持所有流行的浏览器

## 快速上手

### 编写模板

使用一个`type="text/html"`的`script`标签存放模板：
```html
<script id="test" type="text/html">
<h1>{{title}}</h1>
<ul>
    {{each list as value i}}
        <li>索引 {{i + 1}} ：{{value}}</li>
    {{/each}}
</ul>
</script>
```
### 渲染模板
```js
var data = {
    title: '标签',
    list: ['文艺', '博客', '摄影', '电影', '民谣', '旅行', '吉他']
};
var html = template('test', data);
document.getElementById('content').innerHTML = html;
```

[演示](https://visamz.github.io/art-template/demo/basic.html)

##	模板语法

有两个版本的模板语法可以选择。

###	简洁语法

推荐使用，语法简单实用，利于读写。
```html
{{if admin}}
    {{include 'admin_content'}}
    
    {{each list}}
        <div>{{$index}}. {{$value.user}}</div>
    {{/each}}
{{/if}}
```
[查看语法与演示](https://visamz.github.io/art-template/doc/syntax-simple.html)

###	原生语法
```html
<% if (admin){ %>
    <% include('admin_content') %>

    <% for (var i=0;i<list.length;i++) { %>
        <div><%=i%>. <%=list[i].user%></div>
    <% } %>
<% } %>
```
[查看语法与演示](https://visamz.github.io/art-template/doc/syntax-native.html)

##	下载

* [template.js](https://raw.github.com/visamz/art-template/master/dist/template.js) *(简洁语法版, 2.7kb)* 
* [template-native.js](https://raw.github.com/visamz/art-template/master/dist/template-native.js) *(原生语法版, 2.3kb)*

## 方法

###	template(id, data)

根据 id 渲染模板。内部会根据`document.getElementById(id)`查找模板。

如果没有 data 参数，那么将返回一渲染函数。

###	template.`compile`(source, options)

将返回一个渲染函数。[演示](https://visamz.github.io/art-template/demo/compile.html)

###	template.`render`(source, options)

将返回渲染结果。

###	template.`helper`(name, callback)

添加辅助方法。

例如时间格式器：[演示](https://visamz.github.io/art-template/demo/helper.html)

###	template.`config`(name, value)

更改引擎的默认配置。

字段 | 类型 | 默认值| 说明
------------ | ------------- | ------------ | ------------
openTag | String | `'{{'` | 逻辑语法开始标签
closeTag | String | `"}}"` | 逻辑语法结束标签
escape | Boolean | `true` | 是否编码输出 HTML 字符
cache | Boolean | `true` | 是否开启缓存（依赖 options 的 filename 字段）
compress | Boolean | `false` | 是否压缩 HTML 多余空白字符

## 授权协议

Released under the MIT, BSD, and GPL Licenses

============

* [所有演示例子](https://visamz.github.io/art-template/demo/index.html) 
* [引擎原理](http://cdc.tencent.com/?p=5723)

