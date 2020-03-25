##### hook
 > 不使用class的前提下，使用state以及react其他属性
 >1.解决在组件之间复用状态逻辑很难的问题，React 需要为共享状态逻辑提供更好的原生途径
 ```
    import React, { useState } from 'react';
    
    function Example() {
      // 声明一个新的叫做 “count” 的 state 变量
      const [count, setCount] = useState(0);
    
      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => setCount(count + 1)}>
            Click me
          </button>
        </div>
      );
    }
```
    
