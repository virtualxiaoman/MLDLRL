# 1. Quick Start
## 1.1. 初始化项目

1. **安装`vue`**：
```bash
npm install -g @vitejs/create-vite
npm install vue
```
- 第一句是安装`vite`脚手架工具，`-g`表示全局安装。
- 第二句是安装`vue`，`vue`是`vite`的依赖。

2. **创建名为`vue_front`的项目**：
```bash
npm create vite vue_front
```
- 也可以写为`npm create vite@latest vue_front`。

3. **安装依赖**：
```bash
cd vue_front
npm install
npm run dev
```
- `npm install`卡住时，可以尝试`npm cache clean --force`，然后再次`npm install`。
还可以尝试从默认值`npm config set registry https://registry.npmjs.org/`改为`npm config set registry https://registry.npmmirror.com`设置淘宝镜像源。可以使用`npm config get registry`查看当前镜像源。
- `npm`后面可以加上`--force`参数(强制安装)或者`--legacy-peer-deps`参数(忽略依赖检查)。

4. **安装其他的依赖**：
```bash
npm install vue-router
npm install pinia
npm install axios
npm install element-plus
npm install -D sass sass-loader
```
- 这五个的功能分别是：路由、状态管理、网络请求、UI库、样式处理。


-1. 参考资料：
https://blog.csdn.net/weixin_38898884/article/details/139456620

https://blog.csdn.net/yqahx/article/details/119785262


## 1.2. Usage

1. 组件之间的数据传递：
- 父传子：通过`props`传递。
- 子传父：通过`emit`传递。
- 兄弟组件：通过`bus`传递。

`ParentComponent.vue`:
```javascript
<template>
  <div>
    <h1>父组件</h1>
    <p>父组件数据: {{ parentMessage }}</p>
    <ChildComponent :message="parentMessage" @updateMessage="updateParentMessage" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import ChildComponent from './ChildComponent.vue';

const parentMessage = ref('Hello from Parent');

function updateParentMessage(newMessage) {
  parentMessage.value = newMessage;
}
</script>
```
`ChildComponent.vue`:
```javascript
<template>
  <div>
    <h2>子组件</h2>
    <p>从父组件接收到的数据: {{ message }}</p>
    <input v-model="childMessage" placeholder="更新父组件的数据" />
    <button @click="sendUpdate">更新父组件</button>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps(['message']);
const emit = defineEmits(['updateMessage']);

const childMessage = ref('');

function sendUpdate() {
  emit('updateMessage', childMessage.value);
}
</script>
```