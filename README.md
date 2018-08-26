# INSTALLATION

## Install Webpack
```sh
npm install --save-dev webpack webpack-cli webpack-dev-server
```
## Install Babel
```sh
npm install --save-dev babel-core babel-loader babel-preset-env babel-preset-stage2 babel-preset-react
```
## Install React
```sh
npm install --save react react-dom
```
## Install Webpack Plugins
```sh
npm install --save-dev html-webpack-plugin clean-webpack-plugin
```
## Create .babelrc file
```json
{
    "presets": ["env","react","stage-2"]
}
```
## Create webpack.config.js
```javascript
const path = require('path');
const CleanWebpackPlugin = require('clean-webpack-plugin');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname,'dist'),
        filename: 'bundle.js',
        publicPath: '/'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    },
    plugins: [
        new CleanWebpackPlugin(['dist']),
        new HtmlWebpackPlugin({
            title: 'React Application',
            template: './src/public/index.html'
        })
    ]
}
```

## Update package.json
```json
...
  "scripts": {
    "start": "webpack-dev-server --open --mode development --hot",
    "build": "webpack --mode production"
  },
...
```

## Create index.html
```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
        <div id="root"></div>
    </body>
    </html>
```

## Create index.js
```javascript
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<h1>Hello React</h1>,document.getElementById('root'))
```