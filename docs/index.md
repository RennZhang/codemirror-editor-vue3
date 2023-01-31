[![GitHub stars](https://img.shields.io/github/stars/RennCheung/codemirror-editor-vue3)](https://github.com/RennCheung/codemirror-editor-vue3/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/RennCheung/codemirror-editor-vue3)](https://github.com/RennCheung/codemirror-editor-vue3/issues)
[![GitHub forks](https://img.shields.io/github/forks/RennCheung/codemirror-editor-vue3)](https://github.com/RennCheung/codemirror-editor-vue3/network)
[![GitHub last commit](https://img.shields.io/github/last-commit/RennCheung/codemirror-editor-vue3)](https://github.com/RennCheung/codemirror-editor-vue3)
[![license](https://img.shields.io/github/license/RennCheung/codemirror-editor-vue3)](https://github.com/RennCheung/codemirror-editor-vue3)

### 介绍

该插件基于 [Codemirror](http://codemirror.net/)，仅支持 vue3 中使用。

### 安装

```bash
npm install codemirror-editor-vue3 -S
```

```bash
yarn add codemirror-editor-vue3
```

```bash
pnpm i codemirror-editor-vue3 codemirror -S
```

### 全局安装

::: info
**不建议全局注册组件**，这会导致无法正确获取模板上的类型提示。
:::
`main.js:`

```js
import { createApp } from "vue";
import App from "./App.vue";
import { GlobalCmComponent } from "codemirror-editor-vue3";

const app = createApp(App);
app.use(GlobalCmComponent);
app.mount("#app");
```

custom component name:

```js
app.use(GlobalCmComponent, { componentName: "customName" });
```

### 组件中使用

```vue
<template>
  <Codemirror
    v-model:value="code"
    :options="cmOptions"
    border
    placeholder="测试 placeholder"
    :height="200"
    @change="onChange"
  />
</template>

<script>
import Codemirror from "codemirror-editor-vue3";

// placeholder
import "codemirror/addon/display/placeholder.js";
// language
import "codemirror/mode/javascript/javascript.js";

import { ref } from "vue";
export default {
  components: { Codemirror },
  setup() {
    const code = ref(`
var i = 0;
for (; i < 9; i++) {
  console.log(i);
  // more statements
}`);

    return {
      code,
      cmOptions: {
        mode: "text/javascript", // 语言模式
        theme: "default", // 主题
        lineNumbers: true, // 显示行号
        smartIndent: true, // 智能缩进
        indentUnit: 2, // 智能缩进单位为4个空格长度
        foldGutter: true, // 启用行槽中的代码折叠
        styleActiveLine: true, // 显示选中行的样式
      },
      onChange(val, cm) {},
    };
  },
};
</script>
```

### 案例

<component v-if="dynamicComponent" :is="dynamicComponent"></component>

<script >
import {shallowRef} from "vue"
export default {
  data() {
    return {
      dynamicComponent: null
    }
  },

  mounted() {
    import('./views/demo/index.vue').then((module) => {
      this.dynamicComponent = shallowRef(module.default)
    })
  }
}
</script>

### Get codemirror instance object

[View code](https://renncheung.github.io/codemirror-editor-vue3/instructions/cminstance.html)

### 使用[Codemirror 静态属性](https://codemirror.net/doc/manual.html#api_static)

```js
import { CodeMirror } from "codemirror-editor-vue3";
CodeMirror.Pos(0, 5);
```

`or:`

```js
import _CodeMirror from "codemirror";
_CodeMirror.Pos(0, 5);
```

### 其他说明

::: tip
考虑插件需要引入以下基础样式（codemirror 官方样式），插件内部已经引入，不需要在使用时重复引入以下样式：
:::

```js
// base style
import "codemirror/lib/codemirror.css";
import "codemirror/mode/css/css.js";
```

::: warning
在`0.2.4`版本后不再需要引入本组件样式，会在头部自动注入相关样式。
:::

```js {2}
// plugin-style
-- import "codemirror-editor-vue3/dist/style.css";
```
