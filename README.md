## run vue

仿 https://run.iviewui.com/ 可在线运行 Vue 组件,

代码高亮使用技术：vue-codemirror

> 部分代码参考了 https://github.com/xiaolannuoyi/vue-running
>
> 在 Vue 项目中使用 codemirror 插件实现代码编辑器功能（代码高亮显示及自动提示） https://blog.csdn.net/mySpringandhibernate/article/details/84105095

[预览地址](http://tools.rscl.site/run-vue/)

### 设计思路

- 通过正则表达式获取代码的 template, script 和 style。
- `$mount` 实现手动挂载组件。

```js
const script = (this.getSource("script") || "").replace(
  /export default/,
  "return"
);

let component = {};
if (script) {
  component = new Function(script)();
}
if (template) {
  component.template = template;
  // 目前component是一个对象，没有$mount方法
  // Vue.extend()创建构造器，再创建实例instance
  let instance = new (this.$options._base.extend(component))();
  let vnode = instance.$mount().$el; // 在内存中进行挂载
  this.$refs.display.innerHTML = "";
  this.$refs.display.appendChild(vnode); // 挂载的结果放到了$refs上
}
```

- 第一次运行的时候创建一个 style 标签，里面的内容是 Vue 组件的 style，再插入到 html 中。从第二次开始，每次运行只需要替换该 style 标签的内容。
- 通过`vue-codemirror`实现代码高亮。`vue-codemirror`用法和`codemirror`是一样的，可以参考`codemirror` 文档。实现了代码高亮、显示行号、自定义滚动条、代码折叠、自动补全括号、自动补全结束标签、标签匹配（开始和结束标签同时高亮）、当前选中行高亮。

## Project setup

```
yarn install
```

### Compiles and hot-reloads for development

```
yarn serve
```

### Compiles and minifies for production

```
yarn build
```
