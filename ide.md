# 代码规范管理和开发工具

## 代码规范管理

> 为了能让整个团队按照统一的规范编写出符合规范的代码，需要借助一些工具。  

1. 包管理工具  

    Node.js 自带的包管理工具为 npm，但是我们推荐使用 [Yarn](https://yarn.bootcss.com/)，相比于 npm 它有许多优点。
    但是要注意其 Node 版本支持: ^4.8.0 || ^5.7.0 || ^6.2.2 || >=8.0.0。

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
    module.exports = {
      root: true,
      extends: ['plugin:prettier/recommended', 'plugin:vue/essential', '@vue/standard'],
      rules: {
        'prettier/prettier': 'error',
        // allow async-await
        'generator-star-spacing': 'off',
        // allow debugger during development
        'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
        'vue/no-parsing-error': [2, { 'x-invalid-end-tag': false }],
        'no-undef': 'off',
        semi: ['error', 'always'], // 这个地方需要跟 prettier 的规则保持一致
        'no-extra-semi': 'error' //去掉额外的分号
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
`Ctrl + Shift + P` 分别搜索插件  ESLint、Vetur、Prettier - Code formatter、EditorConfig for VS Code 安装，在编辑器首选项配置中修改配置

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
