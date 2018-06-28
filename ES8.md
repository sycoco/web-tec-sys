
### Object.values/Object.entries
> 在ES8 /ES2017之前，Javascript开发者需要迭代一个对象的自身属性时候不得不用Object.keys，通过迭代且使用obj[key]获取value值返回一个数组：
  + 
    ```
    let obj = {a: 1, b: 2, c: 3}
    Object.keys(obj).forEach((key, index)=>{
      console.log(key, obj[key])
    })
    ```
  + 而使用ES6/ES2015 中for/of稍微好点：
    ```
    let obj = {a: 1, b: 2, c: 3}
    for (let key of Object.keys(obj)) {
      console.log(key, obj[key])
    }
    ```
  + ·Object.entries·，在另一方面，将会返回对象自身可迭代属性key-value对数组（作为一个数组），他们（key-value）分别以数组存放数组中。
    ```
    let obj = {a: 1, b: 2, c: 3}
    JSON.stringify(Object.entries(obj))
    "[["a",1],["b",2],["c",3]]"
    ```
  + 我们可以使用ES6/ES2015解构（需要深入了解解构请点击这篇文章和课程）,从这嵌套数组中分别声明key和value
      ```
      let obj = {a: 1, b: 2, c: 3}
      Object.entries(obj).forEach(([key, value]) => {
       console.log(`${key} is ${value}`)
      })
      // a is 1, b is 2, c is 3
 
      ```
  + 我们同样使用ES6for/of（毕竟全部都是数组）遍历Object.entries返回来的结果值。
        ```
        let obj = {a: 1, b: 2, c: 3}
        for (let [key, value] of Object.entries(obj)) {
          console.log(`${key} is ${value}`)
        }
        // a is 1, b is 2, c is 3
  
        ```
### String padding(字符串填充)
> String.prototype.padStart 和 String.prototype.padEnd在javascript字符操作是一个不错的体验，帮助避免依赖而外的库。
  padStart()在开始部位填充，返回一个给出长度的字符串，填充物给定字符串，把字符串填充到期望的长度。从字符串的左边开始（至少大部分西方语言），一个经典例子是使用空格创建列：
  + 两个参数
    ```
    console.log('react'.padStart(10, '_'))         // "_____react"
    console.log('backbone'.padStart(10, '*'))         // "**backbone"
    console.log('react'.padEnd(10, ':-)'))         // "react:-):-" is 10
    console.log('backbone'.padEnd(10, '*'))         // "backbone**" is 10
    ```
### Object.getOwnPropertyDescriptors
> Object.getOwnPropertyDescriptors允许创建真实的对象浅副本并创建子类,它通过给开发者描述符来做到这一点.在Object.create(prototype, object)放入描述符后，返回一个真正的浅拷贝
  + 
    ```
       Object.create(
         Object.getPrototypeOf(obj),
         Object.getOwnPropertyDescriptors(obj)
       )
     ```
  + 或者你可以合并两个对象target和source如下：
    ```
    Object.defineProperties(
      target,
      Object.getOwnPropertyDescriptors(source)
    )
    ```
### 函数参数列表和调用中的尾逗号（Trailing commas）
> 尾逗号主要有用在使用多行参数风格（典型的是那些很长的参数名），开发者终于可以忘记逗号放在第一位这种奇怪的写法。自从逗号bugs主要原因就是使用他们。而现在你可以到处使用逗号，甚至最后参数都可以。
### 异步函数（Async Functions）
> 异步函数（或者async/await）特性操作是Promise最重要的功能。所以你大概进一步阅读他们或者看一个进修视频课程来。这种想法是为了在写异步代码中简化它，因为人类大脑最讨厌这种平行非序号思维了。它只是不会演变这种方式。
  对于我个人来说，我不喜欢Promise，就仅仅相比callback显得特别冗余。所以我从来没有使用过它，幸运的是，在ES8，异步函数是那么给力。开发者定义一个asyc函数里面不包含或者包含await 基于Promise异步操作。在这引擎之下一个异步函数返回一个Promise，无论无何你在任何地方不会看到这样的一个词（注：Promise）(当然了，你非的自己使用)。
  + 例如，在ES6中我们可以使用Promise，Axios库向GraphQL服务器发送一个请求：
    ```
    axios.get(`/q?query=${query}`)
      .then(response => response.data)
      .then(data => {
        this.props.processfetchedData(data) // Defined somewhere else
      })
      .catch(error => console.log(error))
    
    ```
  + 任何一个Promise库都能兼容新的异步函数，我们可以使用同步try/catch做错误处理。
    
    ```
    async fetchData(url) => {
      try {
        const response = await axios.get(`/q?query=${query}`)
        const data = response.data
        this.props.processfetchedData(data)
      } catch (error) {
        console.log(error)
      }
    }
   
    ```
  + 异步函数返回一个Promise，所以我们像下面可以继续执行流程:
    ```
    async fetchData(query) => {
      try {
        const response = await axios.get(`/q?query=${query}`)
        const data = response.data
        return data
      } catch (error) {
        console.log(error)
      }
    }
    fetchData(query).then(data => {
      this.props.processfetchedData(data)
    })
    ```
