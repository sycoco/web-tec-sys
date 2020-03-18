## 原文翻译
### JavaScript来自一门健全的语言，所以你可能觉得JavaScript中的this和其他面向对象的语言如java的this一样，是指存储在实例属性中的值。事实并非如此，在JavaScript中，最好把this当成哈利波特中的博格特的背包，有着深不可测的魔力。
> JavaScript中很多时候会用到this，下面详细介绍每一种情况。在这里我想首先介绍一下宿主环境这个概念。一门语言在运行的时候，需要一个环境，叫做宿主环境。对于JavaScript，宿主环境最常见的是web浏览器，浏览器提供了一个JavaScript运行的环境，这个环境里面，需要提供一些接口，好让JavaScript引擎能够和宿主环境对接。JavaScript引擎才是真正执行JavaScript代码的地方，常见的引擎有V8(目前最快JavaScript引擎、Google生产)、JavaScript core。
JavaScript引擎主要做了下面几件事情：

>+ 一套与宿主环境相联系的规则
>+ JavaScript引擎内核（基本语法规范、逻辑、命令和算法)
>+ 一组内置对象和API
>+ 其他约定

> 但是环境不是唯一的，也就是JavaScript不仅仅能够在浏览器里面跑，也能在其他提供了宿主环境的程序里面跑，最常见的就是nodejs。同样作为一个宿主环境，nodejs也有自己的JavaScript引擎--V8。根据官方的定义:
Node.js is a platform built on Chrome’s JavaScript runtime for easily building fast, scalable network applications

### global this
+ 在浏览器里，在全局范围内，this等价于window对象
+ 在浏览器里，在全局范围内，用var声明一个变量和给this或者window添加属性是等价的
+ 如果你在声明一个变量的时候没有使用var或者let(ECMAScript 6),你就是在给全局的this添加或者改变属性值
+ 在node环境里，如果使用REPL(Read-Eval-Print Loop，简称REPL:读取-求值-输出,是一个简单的，交互式的编程环境)来执行程序,this并不是最高级的命名空间，最高级的是global.
+ 在node环境里，如果执行一个js脚本，在全局范围内，this以一个空对象开始作为最高级的命名空间，这个时候，它和global不是等价的。
+ 在node环境里，在全局范围内，如果你用REPL执行一个脚本文件，用var声明一个变量并不会和在浏览器里面一样将这个变量添加给this
+ 但是如果你不是用REPL执行脚本文件，而是直接执行代码，结果和在浏览器里面是一样的(神坑)
+ 在node环境里，用REPL运行脚本文件的时候，如果在声明变量的时候没有使用var或者let，这个变量会自动添加到global对象，但是不会自动添加给this对象。如果是直接执行代码，则会同时添加给global和this

>上面的八种情况可能大家已经绕晕了，总结起来就是：在浏览器里面this是老大，它等价于window对象，如果你声明一些全局变量(不管在任何地方)，这些变量都会作为this的属性。在node里面，有两种执行JavaScript代码的方式，一种是直接执行写好的JavaScript文件，另外一种是直接在里面执行一行行代码。对于直接运行一行行JavaScript代码的方式，global才是老大，this和它是等价的。在这种情况下，和浏览器比较相似，也就是声明一些全局变量会自动添加给老大global，顺带也会添加给this。但是在node里面直接脚本文件就不一样了，你声明的全局变量不会自动添加到this，但是会添加到global对象。所以相同点是，在全局范围内，全局变量终究是属于老大的。


### function this
+ 无论是在浏览器环境还是node环境， 除了在DOM事件处理程序里或者给出了thisArg(接下来会讲到)外，如果不是用new调用，在函数里面使用this都是指代全局范围的this。
+ 除非你使用严格模式，这时候this就会变成undefined
+ 如果你在调用函数的时候在前面使用了new，this就会变成一个新的值，和global的this脱离干系


>函数里面的this其实相对比较好理解，如果我们在一个函数里面使用this，需要注意的就是我们调用函数的方式，如果是正常的方式调用函数，this指代全局的this，如果我们加一个new，这个函数就变成了一个构造函数，我们就创建了一个实例，this指代这个实例，这个和其他面向对象的语言很像。另外，写JavaScript很常做的一件事就是绑定事件处理程序，也就是诸如button.addEventListener(‘click’, fn, false)之类的，如果在fn里面需要使用this，this指代事件处理程序对应的对象，也就是button。

### prototype this
+ 你创建的每一个函数都是函数对象。它们会自动获得一个特殊的属性prototype，你可以给这个属性赋值。当你用new的方式调用一个函数的时候，你就能通过this访问你给prototype赋的值了。
+ 当你使用new为你的函数创建多个实例的时候，这些实例会共享你给prototype设定的值。对于下面的例子，当你调用this.foo的时候，都会返回相同的值，除非你在某个实例里面重写了自己的this.foo
+ 实例里面的this是一个特殊的对象。你可以把this想成一种获取prototype的值的一种方式。当你在一个实例里面直接给this添加属性的时候，会隐藏prototype中与之同名的属性。如果你想访问prototype中的这个属性值而不是你自己设定的属性值，你可以通过在实例里面删除你自己添加的属性的方式来实现
+ 或者你也能直接通过引用函数对象的prototype 来获得你需要的值
+ 通过一个函数创建的实例会共享这个函数的prototype属性的值，如果你给这个函数的prototype赋值一个Array，那么所有的实例都会共享这个Array，除非你在实例里面重写了这个Array，这种情况下，函数的prototype的Array就会被隐藏掉。
+ 给一个函数的prototype赋值一个Array通常是一个错误的做法。如果你想每一个实例有他们专属的Array，你应该在函数里面创建而不是在prototype里面创建
+ 实际上你可以通过把多个函数的prototype链接起来的从而形成一个原型链，因此this就会魔法般地沿着这条原型链往上查找直到找你你需要引用的值
+ 一些人利用原型链的特性来在JavaScript模仿经典的面向对象的继承方式。任何给用于构建原型链的函数的this的赋值的语句都会隐藏原型链上游的相同的属性
+ 我喜欢把被赋值给prototype的函数叫做方法。在上面的例子中，我已经使用过方法了，如logFoo。这些方法有着相同的prototype，即创建这些实力的原始函数。我通常把这些原始函数叫做构造函数。在prototype里面定义的方法里面使用this会影响到当前实例的原型链的上游的this。这意味着你直接给this赋值的时候，隐藏了原型链上游的相同的属性值。这个实例的任何方法都会使用这个最新的值而不是原型里面定义的这个相同的值
+  在JavaScript里面你可以嵌套函数，也就是你可以在函数里面定义函数。嵌套函数可以通过闭包捕获父函数的变量，但是这个函数没有继承this
+  在doIt里面的this是global对象或者在严格模式下面是undefined。这是造成很多不熟悉JavaScript的人深陷 this陷阱的根源。在这种情况下事情变得非常糟糕，就像你把一个实例的方法当作一个值，把这个值当作函数参数传递给另外一个函数但是却不把这个实例传递给这个函数一样。在这种情况下，一个方法里面的环境变成了全局范围，或者在严格模式下面的undefined
+ 一些人喜欢先把this捕获到一个变量里面，通常这个变量叫做self，来避免上面这种情况的发生


### object this
+ 在一个对象的一个函数里，你可以通过this来引用这个对象的其他属性。这个用new来新建一个实例是不一样的



