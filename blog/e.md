
# 从客户端操作数据库
### 前天 mongodb ：用数据库自己的命令进行增删改查
### 昨天 mongoose : 用 js 代码来操作数据库的增删改查
### 今天 Express : 在客户端操作数据库的增删改查

#### 通过不同的 requset 来实现CRUD

```js
^          requset
   Verb                 Path

get  (只读)             /about
post (新建，编写)        /posts
put  (更新)                 
delete (删除)
```

## REST架构
```js
GET/posts                读取所有文章
POST/posts               新建一篇文章
PUT/posts/:post_id       更新一篇文章
DELETE/posts/:post_id    删除特定一篇文章
GET/posts/:post_id       读取特定一篇文章
```
## Express路由控制 + Mongoose
### 第一个任务，实现 express 路由
#### express 路由 ：跑在服务器上响应/接收客户端发出的 requset 请求，决定哪部分后台代码要被执行

### 第二个任务，学会用 curl 调试 API
调试 PUT 显示更新内容
```js
curl --requset PUT localhost:3000/posts/34
```
调试 GET 读取一篇文章
```js
curl --requset GET localhost:3000/posts/34
```
调试 GET 读取所有文章
```js
curl --requset GET localhost:3000/posts
```
调试 POST 新建一篇文章
```js
curl --requset POST localhost:3000/posts/34
```
调试 DELETE 删除一篇文章
```js
curl --requset DELETE localhost:3000/posts/34
```

```js
客户端                  服务器
react                 express
            json
  js      <--------->    js
```
#### 模拟测试器  Advanced REST client
#### 命令行模拟测试器 curl
```js
curl -H "Content-Type: application/json" -X POST -d '{"title":"myTitle","content":"myContent"}'

```
### 第三个任务，获取提交数据
#### req.body
### 第四个任务，connect 数据库 monngodb,monngoose
## API
1. API 是由当前程序提供出来的
2. 提供给另外一个程序的开发者来使用的
3. 作为前端开发者我们所说的是web API
#### API 本身就是一个请求
#### verb   +   path
#### API 的请求结果就是 json 数据     
