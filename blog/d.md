# 我是D页面

```js
componentDidMount(){
  getJson()
    .then( (recData) => {
      // console.log(recData.getJson);
      this.setState({
        data:recData.getJson,
        wait:false
      })
    });
}
```
