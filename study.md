# webpack

## 入口

在config.js中使用entry的json对象来表示入口

```javascript
module.exports = {
  entry: './path/to/my/entry/file.js',
};
```

## 出口

在config文件中用output表示出口，他有两种方式

```js
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js',
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist',
  },
};

// 写入到硬盘：./dist/app.js, ./dist/search.js
```

或者可以直接写输出的文件名，默认输出到/dist下

## loader

将不能变成js的内容加载，主要有css-loader，style-loader

```js
module.exports = {
  module: {
    rules: [
      {
        //匹配所有.css后缀的文件
        test: /\.css$/,
        use: [
          // [style-loader](/loaders/style-loader)
          { loader: 'style-loader' },
          // [css-loader](/loaders/css-loader)
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          },
          // [sass-loader](/loaders/sass-loader)
          { loader: 'sass-loader' }
        ]
      }
    ]
  }
};
```

## 插件

插件目的在于解决 [loader](https://webpack.docschina.org/concepts/loaders) 无法实现的**其他事**。

webpack **插件**是一个具有 apply 方法的 JavaScript 对象。`apply` 方法会被 webpack compiler 调用，并且在__整个__编译生命周期都可以访问 compiler 对象。

使用插件必须要new一个实例对象

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 访问内置的插件
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
      },
    ],
  },
  plugins: [
    new webpack.ProgressPlugin(),
    new HtmlWebpackPlugin({ template: './src/index.html' }),
  ],
};
```