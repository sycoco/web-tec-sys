###ES6
####Module 语法
* export命令用于规定模块的对外接口
```
let firstName = 'shaying'
let myAge = '24'
export = {firstName ,myAge}
```
***
```
let a = 'adc'
export {a as b}
```

* export命令除了输出变量，还可以输出函数或类
```
export function test (a,b) {return a*b}
```
* import命令用于输入其他模块提供的功能,import命令是编译阶段执行的，在代码运行之前
* import后面的from指定模块文件的位置，可以是相对路径，也可以是绝对路径，.js后缀可以省略。如果只是模块名，不带有路径，那么必须有配置文件，告诉 JavaScript 引擎该模块的位置。
```
import {firstName, lastName, year} from './profile.js'
import { lastName as surname } from './profile.js'
```
* export default命令，为模块指定默认输出。可以用任意名称指向export-default.js输出的方法，这时就不需要知道原模块输出的函数名。需要注意的是，这时import命令后面，不使用大括号。
```
export default function () {
  console.log('foo');
}
```
