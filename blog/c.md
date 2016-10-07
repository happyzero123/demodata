# mongoose
### mongoose 作用：
### 把数据转化成js对象，以便我们可以用js代码来读取MongoDB的数据

### 第一步，确保 mongodb 启动
###### 也就是确保 mongo shell 可以用
```js
mongod --dbpath ~/data/db
```
### 第二步，js代码中连接 mongodb
```js
mongoose.connect('mongodb://localhost:27017/api');
```

每个项目中只需要一个数据库就够了，因为一个数据库中可以创建多个 collection 集合
```js
数据库(database)--->  集合(collection)  --->   文档(document)/记录(record)
```

### 第三步，建立数据 Schema
#### Schema 概要
##### 描述数据结构
```js
 mongoose.Schema({
      name: String,
      password:String,
      age:String
  },
  {timestamps:true})//数据结构
```
##### 描述记录（文档）结构
**规定**
1. 这个记录中有几个字段(field)
2. 每个字段名字(name,age...)
3. 以及字段类型(Sting,Number)

### 第四步，了解 model 模型的概念
#### 官网：http://mongoosejs.com/docs/models.html
model  是MVC之中的M
```js
Model          View          Controller
模型            视图             控制器
```

#### model 通常都会写成一个类存放所有和数据直接相关的代码
```js
var user = mongoose.model('user', userSchema)//面向对象，user 是实际记录（文档）的名字
```
解析：
- 第一个参数：模型对应的集合名称的单数；
- 第二个参数：一条数据记录（文档）的结构；

### 第五步，学会用 js 代码来增删查改
#### CRUD
```js
Create       Read      Update       Delete
  增          查          改           删
```
#### Create 增
```js
db.once('open', function() {
  var userSchema = mongoose.Schema({
      name: String,
      password:String,
      age:String
  },
  {timestamps:true})//数据结构

  var user = mongoose.model('user', userSchema)//面向对象，ppp是实际记录（文档）的名字
  var kitty = new user({ name: '张小晓',password:'xiaoxiao',age:'22岁' })//实例化对象
  kitty.save()
})
```
#### Read 查
```js
user.find().exec(function(err, line) {
     // 异步执行,exec立即执行
  console.log(line);
});
```
Model.findOne()只返回单个文档
```js
Model.findOne({ age: 5}, function (err, doc){
  // doc 是单个文档
});
```
#### Update 改
```js
user.findById({_id: '57ecd36a2fd723346f458d6b'},function(err,line){
  line.name='xx'
  line.save(function(err){
    console.log('更新了');
    user.find().exec(function(err, line) {
       // 异步执行,exec立即执行
       console.log(line);

     });
  })
```
#### Delete 删
```js
user.findById({_id: '57ecd36a2fd723346f458d6b'},function(err,line){
  line.remove(function(err){
   console.log('删除了！');
   user.find().exec(function(err, line) {
      // 异步执行,exec立即执行
      console.log(line);
    });
  })
})
```
## 路由与 mongodb 

```js                             
    路由                          mongodb
app.get('/')                     remove()
                                  find()
app.post('/')                    update()
                                  save()
```
