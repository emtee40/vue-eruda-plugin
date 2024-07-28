**# eruda-vue-devtools**

`eruda-vue-devtools` is an `eruda` plugin that ported `vue.js` official debugging tool `vue-devtools` to the mobile terminal, so that `vue.js` applications can be viewed and debugged directly on the mobile terminal

### preview
[codepen sample code for vue2](https://codepen.io/zippowxk/pen/RwVBgmp)

[CodePen Sample Code for Vue3](https://codepen.io/zippowxk/pen/QWgpJbX)

![Desktop](./docs/eruda-desktop.gif)

### Why do you need this plugin:

1. View and debug `Vue.js` applications on any browser and mobile terminal

2. No need to install the `Vue-devtools` plugin in the browser

3. Support Vue2 & Vue3

### Features

1.  All functions of the official Vue-devtools have been transplanted
2. Some operation methods have been optimized for mobile terminals
3. Now supports the browser in WeChat terminal

### How to use
#### Import by NPM
1. Eruda: ```yarn add eruda-vue-devtools --dev```
2. In the project entry file (such as `src/main.js`)

```javascript
...
import { initPlugin } from 'eruda-vue-devtools' // for eruda
import eruda from 'eruda' // Import toolkit

eruda.init() // Initialization
initPlugin(eruda); // Need to be called before creating the Vue root instance
...
```
3. If your application is not loaded in devtools, please add the following code

```javascript
// Vue 2.x
Vue.config.devtools =  true;
window.__VUE_DEVTOOLS_GLOBAL_HOOK__.emit("init",Vue)
```

#### CDN import

```html
<script src="path/to/eruda.js"></script>
<script>
window.process = { env: {}}
</script>
<script src="https://cdn.jsdelivr.net/npm/eruda-vue-devtools@1.0.1/dist/vue_plugin.js"></script>
<script>
eruda.init();
const Devtools = window.eruda_vue_devtools
Devtools.initPlugin(eruda);
</script>
```

### Advanced usage

1. Import only in development environment

```javascript
new Vue({
render: (h) => h(App),
 }).$mount("#app");

// Called after creating the root instance, it requires the asynchronous module loading capability of webpack
if(process.env.NODE_ENV === "development"){
Promise.all([import("eruda"), import("eruda-vue-devtools")]).then(
(res) => {
if (res.length === 2) {
Vue.config.devtools = true;
window.__VUE_DEVTOOLS_GLOBAL_HOOK__.emit("init",Vue)
const eruda = res[0].default;
const Devtools = res[1].default;
eruda.init() // Initialization
Devtools.initPlugin(eruda); // Need to be called before creating the Vue root instance
}
}
);
}
```
### Update log

#### 1.0.9
1.  Compatible with new versions after vConsole 3.14
2. Update Vue-devtools 6.5.0 to support updated functions
3. Solved some legacy issues after the update

#### v1.0.5
1. Compatible with CDN import and optimized import method
2. Compatible with ES6 destructuring operator import method

#### v1.0.0
1. Major update, upgrade Vue-devtools V6
2. Compatible with Vue3

#### v0.0.7
1. Important update to solve the compatibility problem of iOS WeChat browser
2. Solve the compatibility problem of iOS Ali mPass container

#### v0.0.3
1. Optimized the package size

**### Sample code**

[Github](https://github.com/Zippowxk/Vue-vConsole-devtools/dev)

Welcome to add WeChat **OmniBug ** for discussion and communication, Email:  zippowangxinkai@gmail.com
