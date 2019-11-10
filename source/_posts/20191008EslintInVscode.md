---
title: "Vscode中使用Es-lint终极配置大全"
catalog: true
date: 2019-10-08
subtitle: ""
header-img: "Demo.png"
tags:
- 技术
catagories:
- 技术
---


在 vue项目中使用vscode编辑时，使用了如下这套配置，保存时就会根据既定vue项目中.eslintrc.js文件设置的既定规则自动校验并依据规则修复代码。

***

#### 需安装插件
主要是这两个插件：
ESLint
Prettier - Code formatter


#### vscode中setting.json中配置

```

{
  // vscode默认启用了根据文件类型自动设置tabsize的选项
  "editor.detectIndentation": false,
  // 重新设定tabsize
  "editor.tabSize": 2,
  // #每次保存的时候自动格式化 
  "editor.formatOnSave": true,
  // #每次保存的时候将代码按eslint格式进行修复
  "eslint.autoFixOnSave": true,
  // 添加 vue 支持
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "vue",
      "autoFix": true
    }
  ],
  //  #让prettier使用eslint的代码格式进行校验 
  "prettier.eslintIntegration": true,
  //  #去掉代码结尾的分号 
  "prettier.semi": false,
  //  #使用带引号替代双引号 
  "prettier.singleQuote": true,
  //  #让函数(名)和后面的括号之间加个空格
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
  // #这个按用户自身习惯选择 
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  // #让vue中的js按编辑器自带的ts格式进行格式化 
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      "wrap_attributes": "force-aligned"
      // #vue组件中html代码格式化样式
    }
  },
  // 格式化stylus, 需安装Manta's Stylus Supremacy插件
  "stylusSupremacy.insertColons": false, // 是否插入冒号
  "stylusSupremacy.insertSemicolons": false, // 是否插入分好
  "stylusSupremacy.insertBraces": false, // 是否插入大括号
  "stylusSupremacy.insertNewLineAroundImports": false, // import之后是否换行
  "stylusSupremacy.insertNewLineAroundBlocks": false,
  "window.zoomLevel": 0 // 两个选择器中是否换行
}
```

<br />

#### vue项目中.eslintrc.js文件常用个性化配置
<br />
```

// https://eslint.org/docs/user-guide/configuring

module.exports = {
  root: false,
  parserOptions: {
    parser: 'babel-eslint'
  },
  env: {
    browser: true
  },
  extends: [
    // https://github.com/vuejs/eslint-plugin-vue#priority-a-essential-error-prevention
    // consider switching to `plugin:vue/strongly-recommended` or `plugin:vue/recommended` for stricter rules.
    'plugin:vue/essential',
    // https://github.com/standard/standard/blob/master/docs/RULES-en.md
    'standard'
  ],
  // required to lint *.vue files
  plugins: ['vue'],
  // add your custom rules here
  rules: {
    // allow async-await
    'generator-star-spacing': 'off',
    // allow debugger during development
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    eqeqeq: 'off', // 不能始用==
    'no-unused-vars': 'off', // 消除未使用的变量
    'no-undef': 'off', // 未使用变量报错
    'no-unreachable': 'off' // 不能执行的代码检测
     //此处一下还可以根据个人习惯设置更多个性化内容
  }
}
```