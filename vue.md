# 1. Quick Start
## 1.1. 初始化项目

1. **安装`vue`**：
```bash
npm install vue
npm install -g @vitejs/create-vite
```
- 第一句是安装`vue`，`vue`是`vite`的依赖。
- 第二句是安装`vite`脚手架工具，`-g`表示全局安装(该命令可选)。


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
- `npm install`卡住时或者报错`npm error code E404`，可以尝试`npm cache clean --force`，然后再次`npm install`。
还可以尝试从默认值`npm config set registry https://registry.npmjs.org/`改为`npm config set registry https://registry.npmmirror.com`设置淘宝镜像源。可以使用`npm config get registry`查看当前镜像源。
- `npm`后面可以加上`--force`参数(强制安装)或者`--legacy-peer-deps`参数(忽略依赖检查)。

4. **安装其他的依赖(可选)**：
```bash
npm install vue-router
npm install pinia
npm install axios
npm install element-plus
npm install -D sass sass-loader
```
- 这五个的功能分别是：路由、状态管理、网络请求、UI库、样式处理。


5. 连接到githubpage
- 安装`gh-pages`：
```bash
npm install gh-pages --save-dev
```
- 在`package.json`中添加：
```json
"scripts": {
  "deploy": "gh-pages -d dist"
}
```
- 打包与部署
```bash
npm run build
npm run deploy
```
- 打开 GitHub 仓库的 Settings > Pages，如：https://github.com/virtualxiaoman/blog/settings/pages
在 `Source` 部分选择 `gh-pages` 分支，并点击保存。


6. 参考资料：
- https://blog.csdn.net/weixin_38898884/article/details/139456620
- https://blog.csdn.net/yqahx/article/details/119785262


## 1.2. Usage

1. 组件之间的数据传递：
- 父传子：通过`props`传递。
- 子传父：通过`emit`传递。
- 兄弟组件：通过`bus`传递。

`ParentComponent.vue`:
```html
<template>
  <div>
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
```html
<template>
  <div>
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
上面的原理是：
- `ChildComponent`通过`props`接收`ParentComponent`传递的数据，点击按钮后通过`emit`将数据传递给`ParentComponent`。

细节是：
- `:`表示传递数据，`@`表示接收数据。`v-model`是双向绑定，`@click`是点击事件。
- 父组件里使用`:message`表示传递数据且变量名为`message`，子组件里使用`const props = defineProps(['message']);`表示接收数据且变量名为`message`。
- 子组件里使用`const emit = defineEmits(['updateMessage']);`表示发送数据且事件名为`updateMessage`，父组件里使用`@updateMessage="updateParentMessage"`表示接收数据且事件名为`updateMessage`。


# 2. Vue里渲染markdown

1. **安装`marked`**：
```bash
npm install marked
npm install marked @types/marked highlight.js
npm install highlight.js
npm install vue-markdown
npm install github-markdown-css
npm install katex
npm install --save-dev @types/katex
```
其中`vue-markdown`依赖于`marked`和`highlight.js`。katex的第二个导入是为了在ts文件中使用katex。

2. **导入**：
```ts
import {marked} from 'marked';
import hljs from 'highlight.js';
// import 'highlight.js/styles/github.css';
import "github-markdown-css"
```
注意不是`import marked from 'marked';`，很多gpt都给错了。

# 3. 服务器部署
`https://free.aliyun.com/?spm=5176.28623341`领取阿里云服务器。
`https://ecs.console.aliyun.com/server/i-bp1ddbura4iyenuwu8r6/detail?regionId=cn-hangzhou#/`进入阿里云服务器控制台。
`https://ecs-workbench.aliyun.com/?spm=5176.ecscore_server.0.0.43aa4df5Ps5W6S&form=EcsConsole&instanceType=ecs&regionId=cn-hangzhou&instanceId=i-bp1ddbura4iyenuwu8r6&resourceGroupId=&language=zh`进入阿里云工作台。
输入以下命令
```bash
ssh root@120.55.80.92
sudo yum update -y
sudo yum install nginx -y
sudo yum install mysql-server -y
sudo yum install php-fpm php-mysqlnd -y
```
每一句命令对应的意思是：
- 连接到服务器，这里使用的ip是公网ip。
- 更新服务器。
- 安装nginx。
- 安装mysql。
- 安装php。

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl start mysqld
sudo systemctl enable mysqld
sudo systemctl start php-fpm
sudo systemctl enable php-fpm
```
这些命令的意思是：启动nginx、mysql、php，并且设置开机自启动。
`https://wanwang.aliyun.com/domain/searchresult/?domainCartTradeParams=dr_29379033_1724916831878&spm=5176.29379033.J_fUNSUVBzhRP-3yTOu3xXF.domain-just-search&keyword=azusa&suffix=.net.cn`域名采购。

- https://blog.csdn.net/weixin_45572139/article/details/106085232
- https://blog.csdn.net/weixin_47540834/article/details/138138655
