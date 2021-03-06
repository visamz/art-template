# artTemplate 简洁语法版

## 使用

引用简洁语法的引擎版本，例如：
```js
<script src="dist/template.js"></script>
```   
 [下载](https://raw.github.com/visamz/art-template/master/dist/template.js)

## 表达式

`{{` 与 `}}` 符号包裹起来的语句则为模板的逻辑表达式。

### 输出表达式

对内容编码输出：
```html
{{content}}
```
不编码输出：
```html
{{#content}}
``` 
编码可以防止数据中含有 HTML 字符串，避免引起 XSS 攻击。

### 条件表达式
```html
{{if admin}}
    <p>admin</p>
{{else if code > 0}}
    <p>master</p>
{{else}}
    <p>error!</p>
{{/if}}
```
### 遍历表达式

无论数组或者对象都可以用 each 进行遍历。
```html
{{each list as value index}}
    <li>{{index}} - {{value.user}}</li>
{{/each}}
```
亦可以被简写：
```html
{{each list}}
    <li>{{$index}} - {{$value.user}}</li>
{{/each}}
```
### 模板包含表达式

用于嵌入子模板。
```html
{{include 'template_name'}}
```
子模板默认共享当前数据，亦可以指定数据：
```html
{{include 'template_name' news_list}}
```
## 辅助方法

使用`template.helper(name, callback)`注册公用辅助方法：

```js
template.helper('dateFormat', function (date, format) {
    // ..
    return value;
});
```

模板中使用的方式：
```html
{{time | dateFormat:'yyyy-MM-dd hh:mm:ss'}}
```
支持传入参数与嵌套使用：
```html
{{time | say:'cd' | ubb | link}}
```
##	演示例子

*	[基本例子](https://visamz.github.io/art-template/demo/basic.html)
*	[不转义HTML](https://visamz.github.io/art-template/demo/no-escape.html)
*	[在javascript中存放模板](https://visamz.github.io/art-template/demo/compile.html)
*	[嵌入子模板(include)](https://visamz.github.io/art-template/demo/include.html)
*	[访问外部公用函数(辅助方法)](https://visamz.github.io/art-template/demo/helper.html)

----------------------------------------------

本文档针对 artTemplate v3.0.0+ 编写