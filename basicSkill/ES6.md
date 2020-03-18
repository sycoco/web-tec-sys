
### Object.create()
> Object.create()方法创建一个新对象，使用现有的对象来提供新创建的对象的__proto__。 
  + 
    ```
    const person = {
      isHuman: false,
      printIntroduction: function () {
        console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
      }
    };
    
    const me = Object.create(person);
    
    me.name = "Matthew"; // "name" is a property set on "me", but not on "person"
    me.isHuman = true; // inherited properties can be overwritten
    
    me.printIntroduction();
    // expected output: "My name is Matthew. Am I human? true"
    ```
> Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。
  + Object.assign(target, ...sources)
      ```
      const object1 = {
        a: 1,
        b: 2,
        c: 3
      };
      
      const object2 = Object.assign({c: 4, d: 5}, object1);
      
      console.log(object2.c, object2.d);
      ```
