
### Array.prototype.includes
> Array.prototype.includes用法都容易和简单。它是一个替代indexOf，开发人员用来检查数组中是否存在值，indexOf是一种尴尬的使用，因为它返回一个元素在数组中的位置或者-1当这样的元素不能被找到的情况下。所以它返回一个数字，而不是一个布尔值。开发人员需要实施额外的检查。在ES6，要检查是否存在值你需要做一些如下图所示小技巧，因为他们没有匹配到值，Array.prototype.indexOf返回-1变成了true（转换成true），但是当匹配的元素为0位置时候，该数组包含元素，却变成了false
  + 使用ES6的indexOf时
    ```
    let arr = ['react', 'angular', 'vue']
      
      // WRONG
      if (arr.indexOf('react')) { // 0 -> evaluates to false, definitely as we expected
        console.log('Can use React') // this line would never be executed
      }
      
      // Correct
      if (arr.indexOf('react') !== -1) {
        console.log('Can use React')
      }
    ```
  + 在ES7中使用includes代码如下:
      ```
      let arr = ['react', 'angular', 'vue']
      
      // Correct
      if (arr.includes('react')) {
        console.log('Can use React')
      }
      ```
  + 开发者还能在字符串中使用includes:
      ```
      let str = 'React Quickly'
      
      // Correct
      if (str.toLowerCase().includes('react')) {  // true
        console.log('Found "react"')  
      }
      ```

### Exponentiation Operator(求幂运算)
> 求幂运算大多数是为开发者做一些数学计算，对于3D，VR，SVG还有数据可视化非常有用。在ES6或者早些版本，你不得不创建一个循环，创建一个递归函数或者使用Math.pow,如果你忘记了什么是指数,当你有相同数字（基数）自相相乘多次（指数）。例如，7的3次方是7*7*7
  + 所以在ES6/2015ES，你能使用Math.pow创建一个短的递归箭头函数
    ```
    calculateExponent = (base, exponent) => base*((--exponent>1)?calculateExponent(base, exponent):base)
        console.log(calculateExponent(7,12) === Math.pow(7,12)) // true
        console.log(calculateExponent(2,7) === Math.pow(2,7)) // true
    ```
  + 现在在ES7 /ES2016，以数学向导的开发者可以使用更短的语法:
    ```
    let a = 7 ** 12
    let b = 2 ** 7
    console.log(a === Math.pow(7,12)) // true
    console.log(b === Math.pow(2,7)) // true
    ```
