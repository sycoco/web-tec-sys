
### 入口(entry)
> 入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。
  + webpack.config.js
    ```
    module.exports = {
     entry: './path/to/my/entry/file.js'
    };
    ```

### 出口(output)
> output 属性告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 ./dist。基本上，整个应用程序结构，都会被编译到你指定的输出路径的文件夹中。你可以通过在配置中指定一个 output 字段，来配置这些处理过程：
  + webpack.config.js
    ```
    const path = require('path');
    
    module.exports = {
      entry: './path/to/my/entry/file.js',
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'my-first-webpack.bundle.js'
      }
    };
    ```
    
### loader
> 入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。loader 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后你就可以利用 webpack 的打包能力，对它们进行处理。
  + webpack.config.js
    ```
    const path = require('path');
    
    const config = {
      output: {
        filename: 'my-first-webpack.bundle.js'
      },
      module: {
        rules: [
          { test: /\.txt$/, use: 'raw-loader' }
        ]
      }
    };
    
    module.exports = config;
    ```
    
    
    
### 插件(plugins)
> loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。插件接口功能极其强大，可以用来处理各种各样的任务。想要使用一个插件，你只需要 require() 它，然后把它添加到 plugins 数组中。多数插件可以通过选项(option)自定义。你也可以在一个配置文件中因为不同目的而多次使用同一个插件，这时需要通过使用 new 操作符来创建它的一个实例。
  + webpack.config.js
    ```
    const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
    const webpack = require('webpack'); // 用于访问内置插件
    
    const config = {
      module: {
        rules: [
          { test: /\.txt$/, use: 'raw-loader' }
        ]
      },
      plugins: [
        new webpack.optimize.UglifyJsPlugin(),
        new HtmlWebpackPlugin({template: './src/index.html'})
      ]
    };
    
    module.exports = config;
    ```
### 模式(mode)
> 提供 mode 配置选项，告知 webpack 使用相应模式的内置优化。
  + webpack.config.js
    ```
    module.exports = {
      mode: 'production'
    };
    ```
