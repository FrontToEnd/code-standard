---
theme: unicorn
colorSchema: 'light'
layout: center
---

# 前端代码编写规范

---
layout: new-section
---

# 目录

- 主要规范
- 借助工具
- 代码审查

---
layout: cover
---

# 主要规范

前端编码规范共分为四个部分，分别是：JavaScript、CSS、HTML、Vue。

规范的目的旨在多人协同开发中尽可能的按照规范的要求进行编码，保证前后编码规范要保持一致。

---
layout: cover
---

# JavaScript

针对于JavaScript，我们需要遵循：

- 所有代码必须采用ES6+语言规范进行编写。
- 命名规范。所有单词必须要全拼，不允许单词缩写。也不允许出现单词拼写错误。约定俗成的单词缩写除外。常量必须全部大写，且以下划线分割。变量名、方法名要驼峰命名，类名要首字母大写。自定义组件名要首字母大写。js或ts文件要采取驼峰命名。
    
    ```jsx
    // Good
    const THIS_IS_CONSTANT = 'constant';
    let thisIsVariable = 'variable';
    const handleChange = () => {};
    class EventEmitter {}
    ```

---
layout: cover
---

# JavaScript
    
- 格式规范。注释格式使用[JSDOC](https://jsdoc.app/)规范编写。缩进统一为两个空格。语法的token之间需要有空格。
    
    ```jsx
    // Good
    
    /**
    * @description 这是多行注释
    */
    if (flag) {
    	// todo
    }
    ```
    
- 使用===不要使用==。杜绝隐式转换带来的bug。
- 全面使用Typescript。让静态类型检查帮助代码更加健壮。

---
layout: cover
---

# CSS

针对于CSS，我们需要遵循：

- 命名规范。class命名全部小写，单词以中划线分割。单词不允许缩写，必须全拼。命名遵循BEM规范。禁止以id来声明样式。禁止使用通配符*来声明样式。
    
    ```css
    /* good */
    .aside-header-active {}
    
    /* bad */
    * {}
    #container {}
    ```

---
layout: cover
---

# CSS
    
- 格式规范。统一采用2个空格进行缩进。选择器与大括号之间必须有空格。
    
    ```css
    /* good */
    .selector {
      margin: 0;
      padding: 0;
    }

    /* bad */
    .selector{
      margin:0;
      padding:0;
    }
    ```

---
layout: cover
---

# CSS
    
- 属性规范。在可以使用缩写的情况下，使用属性缩写。除了覆盖第三方样式以外，不允许对属性添加!important。不允许随意添加z-index。
    
    ```css
    /* good */
    .post {
      font: 12px/1.5 arial, sans-serif;
    }
    
    /* bad */
    .post {
      font-family: arial, sans-serif;
      font-size: 12px;
      line-height: 1.5;
    }
    ```
    
---
layout: cover
---

# CSS   

- 单位规范。长度为 0 时须省略单位。calc()函数的数值与运算符直接须添加空格，否则视为语法错误。
    
    ```css
    /* good */
    .header {
    	margin: 0 10px;
    }
    
    /* bad */
    .header {
    	margin: 0px 10px;
    }
    ```

---
layout: cover
---

# CSS
    
- 颜色规范。尽量使用16进制色值。如果有透明值，可采用rgba()函数。16进制能省略就使用省略语法。

  ```css
  /* good */ 
  .background {
    background-color: #fff;
  }
  ```

---
layout: table-contents
gradientColors: ['#17ead9', '#6078ea']
---

# HTML

针对于HTML，我们需要遵循：

- 格式规范。统一采用2个空格进行缩进。
- 命名规范。同一个页面只允许存在一个id。
- 语义化规范。尽量采用语义化标签用来编写，不要满屏的div。
- 图片规范。禁止 `img` 的 `src` 取值为空。延迟加载的图片也要增加默认的 `src`。为重要图片添加 `alt` 属性。

---
layout: cover-logos
logos: [
  'https://v2.cn.vuejs.org/images/logo.svg',
]
---

# Vue

针对于Vue，可直接查看官方的[风格指南](https://v2.cn.vuejs.org/v2/style-guide/)。

---
layout: cover
---

# 借助工具

以上所罗列的主要规范需要人为的遵守，但是这种方式没有强制性，完全取决于开发者是否自觉。

那么就有必要引入工具来协助开发者来规范代码。

---
layout: cover
---

# eslint

- [eslint](https://eslint.org/)是提供一个插件化的javascript代码检测工具。可以使用现有的一些列规则，也可以自定义规则。

- 通过配置eslint，可以提前发现代码不规范的地方，并且支持修复不规范的代码。

```js
// @ts-check
const { defineConfig } = require('eslint-define-config');
module.exports = defineConfig({
  root: true,
  env: {
    browser: true,
  },
  parser: 'vue-eslint-parser',
  parserOptions: {
    parser: '@typescript-eslint/parser',
  },
  extends: [
    'plugin:vue/vue3-recommended',
    'prettier',
    // more
  ],
  rules: {
    'vue/script-setup-uses-vars': 'error',
    // more
  },
});

```

---
layout: cover
---

# prettier

- [prettier](https://prettier.io/)是一个代码格式工具。并内置于WebStorm中。

- 通过和`eslint`搭配使用，在发现格式问题的同时，会自动帮助我们修复格式上的问题。

```js
module.exports = {
  printWidth: 100,
  semi: true,
  vueIndentScriptAndStyle: true,
  singleQuote: true,
  trailingComma: 'all',
  proseWrap: 'never',
  htmlWhitespaceSensitivity: 'strict',
  endOfLine: 'auto',
};

```

---
layout: cover
---

# stylelint

[stylelint](https://stylelint.io/)是一个css代码检测工具。与`eslint`类似，只不过该工具是规范css代码的。

```js
module.exports = {
  root: true,
  plugins: ['stylelint-order'],
  customSyntax: 'postcss-less',
  extends: ['stylelint-config-standard', 'stylelint-config-prettier'],
  rules: {
    // 省略
  },
  ignoreFiles: ['**/*.js', '**/*.jsx', '**/*.tsx', '**/*.ts'],
  overrides: [],
};

```

---
layout: cover
---

# commitlint

[commitlint](https://commitlint.js.org/#/)会规范我们提交git版本的信息。避免所有的commit msg都是fix bug。主要的类型有：

```text
build：主要目的是修改项目构建系统(例如 glup，webpack，rollup 的配置等)的提交
ci：主要目的是修改项目继续集成流程(例如 Travis，Jenkins，GitLab CI，Circle等)的提交
docs：文档更新
feat：新增功能
fix：bug 修复
perf：性能, 体验优化
refactor：重构代码(既没有新增功能，也没有修复 bug)
style：不影响程序逻辑的代码修改(修改空白字符，格式缩进，补全缺失的分号等，没有改变代码逻辑)
test：新增测试用例或是更新现有测试
revert：回滚某个更早之前的提交
chore：不属于以上类型的其他类型
```

---
layout: cover
---

# husky

- [husky](https://typicode.github.io/husky/#/)用来检测commit信息。
- `commitlint` 搭配 `husky` 的 commit message 钩子后，每次提交 git 版本信息的时候，会根据配置的规则进行校验，若不符合规则会 commit 失败，并提示相应信息。


---
layout: cover
---

# 代码评审

上述所有的内容都是为了让开发者的代码写的更加规范，但是很多不规范的写法依旧是工具检测不出来的。这时候需要最后一道防线，也就是代码评审。

代码评审的常见问题：

1. 拼写错误。
2. 未优化的代码实现。
3. 不必要的复杂代码。
4. 重复实现已经存在的代码逻辑。
5. 缺少必要的注释。
6. ...

---
layout: cover
---

# 代码评审

代码评审的正确态度：

1. 评审人对被评审的代码逻辑应做到完全看懂。
2. 评审人对什么是好的代码应该有正确的认识。
3. 评审人对代码的质量应具有一丝不苟的态度。
4. 要将代码评审放在和编写代码同等重要的位置。
5. 在代码评审中要以提升代码质量为最终目标。

---
layout: center
---

# Thank you