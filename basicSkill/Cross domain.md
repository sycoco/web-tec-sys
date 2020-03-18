## 什么是跨域？
### 跨域是指一个域下的文档或脚本试图去请求另一个域下的资源，这里跨域是广义的
> 广义的跨域

>+ 资源跳转： A链接、重定向、表单提交
>+ 资源嵌入： <link>、<script>、<img>、<frame>等dom标签，还有样式中background:url()、@font-face()等文件外链
>+ 脚本请求： js发起的ajax请求、dom和js对象的跨域操作等

> 什么是同源策略？
> 同源策略/SOP（Same origin policy）是一种约定，由Netscape公司1995年引入浏览器，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源。

### 同源策略限制以下几种行为
+ Cookie、LocalStorage 和 IndexDB 无法读取
+ DOM 和 Js对象无法获得
+ AJAX 请求不能发送


### 跨域解决方案
+ 通过jsonp跨域
+ document.domain + iframe跨域
+ location.hash + iframe
+ window.name + iframe跨域
+ 跨域资源共享（CORS）
+ nginx代理跨域
+ nodejs中间件代理跨域
+ WebSocket协议跨域




