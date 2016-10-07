# Mongoose 使用
### 1.确保有数据 req.body.title
### 2.建立代码和数据库的链接
```js
mongoose.connect('mongodb://localhost:27017/ex-api');  //连接数据库
var db = mongoose.connection;
db.on('error', console.log);
db.once('open', function() {
  console.log('success!!!!'); //打印 success!
})
```
### 3.创建 Schema 在models/post.js
```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
const PostSchema = new Schema(
  {
    name:String
  }
)


```
### 4.创建 model
```js
module.exports = mongoose.model('Post',PostSchema);
```
### 5.导入 Post model
```js
// 在index.js里
var Post = require('./models/post')
```
### 6.实例化Post model 得到 post 这个对象
```js
var post = new Post({name:req.body.name})
```
### 7.保存 post 到数据库
```js
post.save(function(err){
  if(err) console.log(err);
  console.log('POST/posts   save');
})
```
### 8.重定向,redireact
<img src="/home/xiaoxiao/桌面/深度截图20161004193526.png">
```js
res.redirect('/posts')//重定向：让浏览器自动发出第二次请求到/posts下
```
```js
 res.redirect('https://www.baidu.com')//重定向：让浏览器自动发出第二次请求到百度上
```
## server 端先告一段落
-------
# 前后端分离的架构
## 后台只负责 json 数据，不负责 html && css
## 前后台沟通的数据格式是 json
## 前台请求数据的方式是发 Ajax 请求
### 第一步，搭建 React-Webpack 开发环境
### 第二步，了解跨域请求问题
## 同源策略
## 浏览器发出 http 请求
<img/>
## 违背了同源策略 (same origin policy)
```js
localhost:8080                      localhost:3000
                       API
React              ----------->       Express API
```
## 客户端和服务器端域名相同，同时端口也要相同
#### 为什么客户端可以访问 api.github.com/xxxx ？
#### 原因就是 github 关闭了同源策略
### http 报头 (header)
#### Access-Control-Allow-Origin 访问权限允许源头
```js
Access-Control-Allow-Origin: *
```
### 以 github 为例
```js
curl -i https://api.github.com/users/happyzero123
```
如果只想看到 header 就用 curl -I
```js
curl -I https://api.github.com/users/happyzero123

输出结果如下：
```js
Access-Control-Allow-Origin: *
```
### 取消 Express 同源策略
#### 服务器端设置
```js
Access-Control-Allow-Origin: *
```
*CORS*<br>
Cross Orign resource share<br>
跨域资源共享
#### 首先要下载 cors 包
```js
npm i --save cors
```
#### 在服务器端 index.js 里执行如下代码：
```js
//关闭同源策略，开放CORS
var cors = require('cors');
app.use(cors());
```
