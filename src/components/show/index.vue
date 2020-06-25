<template>
  <div class="show-box" ref="display"></div>
</template>

<script>
import { match } from "assert";
import { randomString } from "@/utils";

export default {
  props: {
    code: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      component: null,
      cssid: randomString(32)
    };
  },
  methods: {
    run() {
      // 1. 获取模板中的内容 js css
      const template = this.getSource("template");
      const script = (this.getSource("script") || "").replace(
        /export default/,
        "return"
      );
      const style = this.getSource("style");
      // console.log(template, script, style);
      // 动态的加载一个组件 组件就是一个对象 对象里包含数据、render函数、生命周期方法

      let component = {};
      if (script) {
        component = new Function(script)();
      }
      if (template) {
        component.template = template;
        // $mount可以实现手动挂载组件
        // 目前component是一个对象，没有$mount方法
        // Vue.extend()创建构造器，再创建实例
        let instance = new (this.$options._base.extend(component))();
        // let vnode = instance.$mount().$el; // 在内存中进行挂载
        // this.$refs.display.innerHTML = "";
        // this.$refs.display.appendChild(vnode); // 挂载的结果放到了$refs上
        this.component = instance.$mount();
        this.$refs.display.appendChild(this.component.$el);
      }
      if (style) {
        let styleEle = document.getElementById(this.cssid);
        if (styleEle) {
          styleEle.innerText = style;
        } else {
          let element = document.createElement("style");
          element.setAttribute("type", "text/css");
          element.id = this.cssid;
          element.innerText = style;
          document.getElementsByTagName("head")[0].appendChild(element);
        }
      }
      console.log(component);
    },
    getSource(type) {
      const reg = new RegExp(`<${type}[^>]*>`); // 开始标签
      let code = this.code;
      let matches = code.match(reg);

      if (matches) {
        let tag = matches[0];
        return code.slice(
          code.indexOf(tag) + tag.length,
          code.lastIndexOf(`</${type}>`)
        );
      } else {
        return "";
      }
    },
    reset() {
      this.$refs.display.innerHTML = "";
      this.component = null;
      if (this.component) {
        this.component.$destroy();
      }
      // let styleEle = document.getElementById(this.cssid);
      // if (styleEle) {
      //   styleEle.innerText = "";
      // }
    }
  }
};
</script>

<style>
.show-box {
  width: 100%;
  height: 100%;
  padding: 20px;
  box-sizing: border-box;
}
</style>