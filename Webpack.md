
### 入口(entry)
> 入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。
  + webpack.config.js
    ```
    module.exports = {
     entry: './path/to/my/entry/file.js'
    };
    ```
