##### promise
 > promise是一个容器，里面存放一个未来才会结束的事件，是个对象
 ```
    function timeout(ms) {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, ms, 'done');
      });
    }
    
    timeout(100).then((value) => {
      console.log(value);
    });
函数timeout是个Promise的实例，过了上面的毫秒数之后，实例的状态就会从pending改为resolved,触发then绑定的回调函数
```
> promise嵌套promise
```
   const p9 = new Promise(function(resolve, reject){setTimeout(() => reject(new Error('fail')), 3000)})
   const p10 = new Promise(function(resolve, reject){setTimeout(() => resolve(p9), 1000)});
   p10.then(res=>console.log('res', res)).catch(error => console.log('error', error))
   
```
    
