# 建立，上传，删除分支步骤

### 1.从别人的网站上 `clone` 到本地

```js
git clone git@github.com:newming/06-demo.git 16-demo
```

### 2.跳转到新建的文件夹

```js
cd 16-demo
```

### 3.删除仓库 `.git`

```js
rm -rf .git
```

### 4.远端 github 上创建一个仓库 `16-demo`


### 5.初始化仓库

```js
git init
```

### 6.全部添加

```js
git add .
```

### 7.描述

```js
git commit -m'add'
```

### 8.上传

```js
git push
```
```js
git remote add origin git@github.com:happyzero123/16-demo.git
```
```js
git push
```
```js
git push --set-upstream origin master
```

### 9.找到`webpack.config.js`里的

```js
module.exports = { output : {  publicPath : "/build/", }  }
```

### 将路径/build/改为 . /build/

```js
module.exports = { output : {  publicPath : "./build/", }
}
```

### 10.在`.gitignore ` 里删除 build


### 11.打包

```js
npm run build
```

### 12.建立分支

```js
git checkout -b gh-pages
```

### 13.查看当前分支

```js
git branch
```

### 14.删除分支上多余文件， 只留下`index.html`,`README.md`,`404.html`,`.gitignore`,`build`

```js
rm -r src package.json webpack.config.js .babelrc
```

### 15.分支上传至远端仓库上

```js
git push origin gh-pages
```

### 16.切换分支

当前所在位置为 gh-pages 分支， 要想回到主分支 master ，执行
```js
git checkout master
```

### 17.删除分支

#### 在客户端必须把分支切换到 master 主分支 ，现在想要删除  gh-pages 分支,执行

```js
git branch -D gh-pages
```

#### 如果想要在客户端删除 github 上的 gh-pages 分支,执行

```js
git push origin :gh-pages
```
