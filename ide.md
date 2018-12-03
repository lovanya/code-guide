# 代码规范管理和开发工具

## 代码规范管理

> 为了能让整个团队按照统一的规范编写出符合规范的代码，需要借助一些工具。  

1. 包管理工具  

    Node.js 自带的包管理工具为 npm，但是我们推荐使用 [Yarn](https://yarn.bootcss.com/)，相比于 npm 它有许多优点。
    但是要注意其 Node 版本支持: ^4.8.0 || ^5.7.0 || ^6.2.2 || >=8.0.0。

    由于国外很多站点访问较慢，可以是国内的淘宝镜像。
    ``` bash
    yarn config set registry https://registry.npm.taobao.org
    # or
    npm config set registry https://registry.npm.taobao.org
    ```
    

2. [ESLint](https://eslint.org/) 检查代码中的错误  
   
    如果你仅仅想让 ESLint 成为你项目构建系统的一部分，我们可以在项目根目录进行本地安装：

    ```bash
    yarn add eslint -dev
    ```

    如果想使 ESLint 适用于你所有的项目，我们建议使用全局安装，使用全局安装 ESLint 后，你使用的任何 ESLint 插件或可分享的配置也都必须在全局安装：

    ```bash
    yarn global add eslint
    ```  
    .eslintrc.js:
    ```javascript
    // http://eslint.org/docs/user-guide/configuring
    module.exports = {
      root: true,
      extends: ['plugin:prettier/recommended', 'plugin:vue/essential', '@vue/standard'],
      // required to lint *.vue files 使用 html参数
      plugins: ['prettier'],
      rules: {
        'prettier/prettier': 'error', // 开启 prettier 检查
        'generator-star-spacing': 'off', // 生成器函数*的前后空格
        'vue/no-parsing-error': [2, { 'x-invalid-end-tag': false }],
        'no-undef': 'off',
        semi: ['error', 'always'],
        'no-extra-semi': 'error', // 这个地方需要跟 prettier 的规则保持一致
        'space-before-function-paren': [
          'error',
          {
            anonymous: 'never',
            named: 'never',
            asyncArrow: 'always'
          }
        ],
        'no-dupe-keys': 2, // 在创建对象字面量时不允许键重复 {a:1,a:1}
        'no-console': 'error', // 禁止直接调用 console 系列函数
        'no-alert': 'error', // 禁止调用 alert 函数
        'no-debugger': 'error', // 禁止调用 debugger
        'no-implied-eval': 'error', // 在setTimeout(), setInterval() or execScript()中消除隐式eval的使用，如 setTimeout('alert("Hi!")', 100);
        'no-eval': 'error', // 禁止调用 eval 函数
        'no-empty': 'error',
        'no-unreachable': 2, // 禁止有执行不到的代码
        'nonblock-statement-body-position': ['error', 'below'], // 条件控制语句，执行部分必须另起一行
        curly: 'error', // if while 等条件控制语句后面必须有大括号
        'no-labels': [2, { allowLoop: false, allowSwitch: false }], // 禁止使用label语句，以避免无限循环
        'no-else-return': 2, // 如果if语句里面有return,后面不能跟else语句
        'no-extra-parens': 2, // 禁止非必要的括号
        radix: 2, // parseInt必须指定第二个参数
        'no-restricted-syntax': [
          // 自定义规则，不允许直接调用 setTimeout， setInterval， execScript
          'error',
          {
            selector: "CallExpression[callee.name='setTimeout']",
            message: 'Unexpected setTimeout.'
          },
          {
            selector: "CallExpression[callee.name='setInterval']",
            message: 'Unexpected setInterval.'
          },
          {
            selector: "CallExpression[callee.name='execScript']",
            message: 'Unexpected execScript.'
          }
        ]
      }
    };

    ```
3. [EditorConfig](https://editorconfig.org/) 统一的代码风格工具
   
    将配置文件 .editorconfig 放到项目的根目录下
    .editorconfig:
    ```bash
    # EditorConfig is awesome: https://EditorConfig.org

    # top-most EditorConfig file
    root = true

    [*]
    # Set default charset
    charset = utf-8

    # Tab indentation
    indent_style = space
    indent_size = 2

    # Unix-style newlines with a newline ending every file
    end_of_line = lf
    insert_final_newline = true
    
    # remove any whitespace characters preceding newline characters
    trim_trailing_whitespace = true
    ```

4. [Prettier](https://prettier.io/) 格式化代码的工具
    Install with yarn:
    ```bash
    yarn add prettier --dev --exact
    # or globally
    yarn global add prettier
    ```
    .prettierrc.js:
    ```javascript
    // prettier.config.js or .prettierrc.js
    module.exports = {
      printWidth: 100,
      singleQuote: true, // 这个地方需要跟 eslint 的规则保持一致
      semi: true // 这个地方需要跟 eslint 的规则保持一致
    };
    ```
ESlint 和 Prettier 我们都选择在项目中安装，这样不管能避免其他成员没有全局安装相应的工具。

## 开发工具

我们选择 [Visual Studio Code](https://code.visualstudio.com/) 作为前端开发的工具。
`Ctrl + Shift + X` 分别搜索插件  ESLint、Vetur、Prettier - Code formatter、EditorConfig for VS Code 安装，在编辑器首选项配置中修改配置

```json
"vetur.format.defaultFormatter.html": "prettier", 
"eslint.autoFixOnSave": true,  //保存时使用自动格式化
"eslint.validate": [   //验证文件类型
  "javascript",
  "javascriptreact",
  "vue",
  "html",
  "jsx",
  {
    "language": "html",
    "autoFix": true
  },
  {
    "language": "vue",
    "autoFix": true
  }
],
"editor.formatOnSave": true,  //保存时自动格式化
```
WebStorm 可以参考这篇[博客](https://www.godblessyuan.com/2018/04/%E6%A2%B3%E7%90%86%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E4%BD%BF%E7%94%A8eslint%E5%92%8Cprettier%E6%9D%A5%E6%A3%80%E6%9F%A5%E5%92%8C%E6%A0%BC%E5%BC%8F%E5%8C%96%E4%BB%A3%E7%A0%81%E9%97%AE%E9%A2%98.html)进行配置

为了更有效地开发项目，推荐大家为 VSCode 安装一些插件：

- Auto Close Tag
- Auto Close Tag
- Bracket Pair Colorizer
- Document This
- Git History
- Git Project Manager
- GitLens — Git supercharged
- HTML Snippets
- HTML CSS Support
- Image preview
- Indenticator
- JavaScript (ES6) code snippets
- open in browser
- Path Intellisense
- TODO Highlight
- VS Color Picker
- Vue 2 Snippets
- VueHelper
