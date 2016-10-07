# 深入服务器端
## 简单介绍
```js
×          http协议         
客户端    <--------->     服务器端 (Linux系统)
  ||                1.存储网页  网络服务器 nginx
  ||                2.存储数据  数据库  mongodb
用户能看到的
```
###### http协议参考资料：跟着peter学英语 / haoqicat.com. ( 自学 )
#### Linux系统：
###### 市面上有:
- Redhat   ( 企业级服务器，太复杂，不推荐 )；
- centerOs ( Redhat简易版，不推荐 )；
- Ubuntu  ( 创业最流行用，由南非开发的，原意为互相帮助，推荐 )；
- deepin 深度   ( Ubuntu 的建议版，推荐 )；

##### 微信开发 ： H5 + JS


#### In Order to use server
###### you will install Ubuntu linux Os and you will use command line to run it.
## 部署项目(deploy)
```js
×        请求requset
开发机   <----------->    服务器
×        响应response
```
#### 1. 上传代码：ssh/git/github
```js
scp -r express-api 用户名@IP号:
```
注意： scp必须在自己的开发机器上执行；
#### 2. 登陆到服务器上：
```js
ssh 用户名@IP号
输入密码×××××××
```
#### 3. 安装（软件）服务器 server：
```js
sudo apt-get install nginx
```
- sudo ：使用管理员权限；
- apt-get install ：安装软件；
- nginx ：被安装的软件；

#### 4. 配置服务器nginx:
##### 跳转到nginx的配置区域
```js
cd /etc/nginx/  
```

##### 打开添加新网站的配置文件夹
```js
cd sites-enabled/
```
#### 5. 使用vim修改. 创建配置文件
```js
sudo vim express.conf
```
conf:配置；
##### 查看：
```js
cat express.conf
```
##### 附录：
```js
server {
  listen 80 default;
  server_name xiaoxiao.com;
  root /home/liyuexi/xiaoxiao/express-api; //原码位置
}
```

##### 修改配置后要重启服务器
```js
sudo service nginx reload  //重新加载配置文件
```
#### 5. 用设置的域名去访问网站

##### 查看报错信息
```js
sudo nginx -t
```
##### 查看所在位置
```js
pwd
```


## 局域网内模拟部署过程
#### 第一步. 组队
#### 第二步. 查看自己IP号
```js
ifconfig
```
#### 第三步. ping一下队友的IP
确认自己的机器能不能联通目标服务器
```js
ping 192.168.1.125
```

#### 第四步. 安装ssh server
开放自己的机器让队友登陆开放自己的机器让队友登陆
```js
sudo apt-get install openssh-server
```

#### 第五步. ssh 登陆
```js
ssh liyuexi@192.168.1.125
输入队友密码：××××××
```
#### 第六步. 上传代码
上传自己的代码到对方的电脑
```js
scp -r express-api liyuexi@192.168.1.125:xiaoxiao/
```
- scp 是基于 ssh 的；
- 必须有最后的冒号“：”；
- scp 必须在自己的开发机器上执行

#### 第七步.  配置 nginx
##### 1. 下载文件
从liyuexi上下载20160926.pdf文件从liyuexi上下载20160926.pdf文件
```js
scp liyuexi@192.168.1.125:20160926.pdf .
```

###### 注意 ： 最后的"." 可以用文件夹替代；
##### 2. 跳转到nginx的配置区域
```js
cd /etc/nginx/
```
##### 3. 打开添加新网站的配置文件夹
```js
cd sites-enabled/
```
##### 4. 使用vim 来修改配置文件
```js
sudo vim express.conf
```
##### 5.修改或添加内容在express.conf里
```js
server {
  listen 80 default;
  server_name xiaoxiao.com;
  root /home/liyuexi/xiaoxiao/express-api;
}
```
##### 6.修改配置后要重启服务器
```js
sudo service nginx reload //重新加载配置文件
```
#### 第八步. 用设置的域名去访问网站


## DNS
##### 可以将IP号和域名绑定
#### 设置本地的DNS
在自己的开发机器上操作
```js
sodo vim /etc/hosts/
```
打开文件后写服务器的IP号和域名
```js
192.168.1.125   xiaoxiao.com
```
## 配置公钥（不需要密码登陆）
```js
开发机                     服务器
公钥 id_rsa.pub          id_rsa.pub
私钥 id_rsa            ~/.ssh/authorized—keys
```
#### 1.生成ssh  key
在自己的开发机上执行
```js
cd ~
cd .ssh
ls
//没有公钥可以创建公钥，执行
ssh-keygen
```
#### 2.拷贝公钥
在自己的开发机上执行
```js
vim id_rsa.pub //打开后进行拷贝
```
#### 3.登陆服务器
在自己开发机上执行
```js
ssh liyuexi@xiaoxiao.com
```
#### 4.粘贴
转到服务器上执行
```js
cd .ssh
ls
//新建文件夹
sudo vim authorized_keys
```
打开文件后把拷贝的公钥粘贴到文件夹上保存，退出,回到自己的开发机上登陆
###### 注意：粘贴过程千万别多空格和回车
```js
ssh liyuexi@xiaoxiao.com //此时登陆不需要密码了
```
# Express
#### 什么是Express ?
nodejs 技术的Web应用框架
`React` 是一个前端框架，
`Express` 是后台框架。
数据库 database
#### 登陆时后台操作
###### 代码
1. 查询数据库
2. 把数据插入html模板

官网 ： https://expressjs.com
#### 动手express写代码
初始化
```js
npm init
```
安装express
```js
npm install --save express
```
- console 本意是控制台
- console 前台运行就是chrome devtools的console
- console 后台运行就是命令行界面
http 请求 = Verb + Path
http 请求 = get/post/... + /about
###### express的代码是要在服务器上运行的
```js
app.get('/', function (req, res) {
  res.send('Hello Express')
})  // 接收请求
app.post('/ppp', function (req, res) {
  res.send('Hello ppp')
})
```
- get请求：只读
- post请求：编译

## 路由
#### 什么是路由？router
##### 代码
1. 路由代码
2. 其他代码

###### 路由基本意思：
根据http请求，来决定让哪个页面要显示
###### 路由拓展意思：
根据http请求，来决定让哪一段代码要执行

#### 读取请求参数
requset = Verb + Path
参数（parameters)作为path来传入后台，
这样可以实现前台数据传入后台代码中。



## CURL 小教程
```js
 curl --request GET localhost:3000/xiaoxiao
 ```
 ```JS
 curl --request POST localhost:3000/xiaoxiao
 ```
