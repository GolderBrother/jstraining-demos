# 手写个强大的Vue复杂表格组件

## 快速原型开发

```js
npm install -g @vue/cli-service-global
```

> vue/global-service和vue-cli有什么区别呢？
除了不初始化项目，其余都一样

用```vue serve```来启动项目

新建个文件夹
项目目录结构：

- public/index.html
- App.vue
- main.js

### 新建个main.js文件
> 写入以下内容：

```js
import Vue from 'vue';
import App from './App';
export default new Vue({
    el: "#app",
    render: h => h(App)
})
```

### 需要安装的依赖
```js
npm i stylus stylus-loader webpack lodash -S
```

参考iview的table组件来写

```js
:class="{border, stripe}"

<zf-table border></zf-table>
```

直接写个border，那就是默认为true

### 父子组件通信：

.sync 同步语法糖
```js
:selectedItems.sync = "selectedItems"
```

相当于下面这样的：
```js
@update:selectItems="newSelectedItems => selectItems = newSelectedItems"
```

自组件向上通知：
```js
this.emit("update:selectItems", newData)
```


checkbox实现半选：

```js
checkboxInstance.indeteminate = true;
```

**只能通过js来设置，不能直接写在html中**

前端排序不靠谱：
数据复杂的话前端排序麻烦

点击排序后，发请求给后台排序，然后获取排序后的新数据重新渲染表格

### 表头固定：
给表格设置height后，就可以固定表头

将原来的表头"剪切"(cloneNode)到一个新的table中

cloneNode()，默认只拷贝父节点，不传参就不会拷贝子元素，传true就会拷贝子元素

### 表头thead的列宽度跟tbody的宽度怎么保持一致？
获取tbody第一行的每一列的宽度，然后同步给thead的对应列的宽度

> 传变量，number，字符串就需要加冒号

### 什么时候需要拷贝数据？
当子组件需要更改父组件数据的时候，就需要拷贝数据

**写组件关键是样式要写好看**






