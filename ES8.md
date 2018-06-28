
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

