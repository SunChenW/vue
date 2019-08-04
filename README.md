# VUE

官方太(๑•̀ㅂ•́)و✧棒，还轮不到我班门弄斧：<a href="https://cn.vuejs.org/v2/guide/">vue官方2.x文档</a>

> vue的官方文档紧跟时代脚步，完全采用es6语法编写教程。建议新学者优先学习ES6，更快掌握学习vue的正确姿势。
>
> 但，万变不离其宗！牢固的javascript语言基础，一眼看穿本质。不管官方各种骚操作，我就`ctrl + c`  `ctrl + v`。

## 指令与选项与生命周期

| {{}}    | v-bind | v-show  |
| ------- | ------ | ------- |
| v-html  | v-on   | v-cloak |
| v-text  | v-if   | v-for   |
| v-model | v-else |         |

| data    | el         | methods   |
| ------- | ---------- | --------- |
| watch   | computed   | componens |
| filters | directives |           |

| beforeCreate  | created   |
| ------------- | --------- |
| beforeMount   | mounted   |
| beforeUpdate  | updated   |
| beforeDestroy | destroyed |

## 自定义键盘修饰符

```javascript
Vue.config.keyCodes.ffff = 123
```

## 自定义指令

```javascript
//全局指令
Vue.directive("focus",{
    bind:function(el,binding),
    inserted:function(el,binding),
    update:...,
    unbind:...
})
//私有指令
directives:{
    focus:funciton(el,binding){}
}
```

## axios

<a href="https://www.jianshu.com/p/7a9fbcbb1114">别人做的axios</a>

<a href="http://www.axios-js.com/docs/nuxtjs-axios.html">axios在vuecli中使用</a>

> vue相关的技术都有比较完美的文档，感谢大神！！！

- axios 是一个独立的js插件，可以单独使用，也可以配置在框架中使用。axios的方法都是支持promise的，也就是可以`.then()`  使用回掉函数接受数据

```javascript
//随便找个地方引入 axios
//<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

//然后就可以放心的使用（如果你过jquery，下边的语法不用我解释的）

axios.get("/post",{}) //请求地址   发送到服务器的数据
    .then(function(res){
    	console.log(res.data) //res调用data获取响应数据
	})
//可以设置全局根目录
axios.default.baseURL = "http://127.0.0.0:8080"
//正常这些够用了，详情自己去百度吧 ↑↑
```

- 如果不嫌麻烦（更不怕别人说你Low），在vue中完全可以将axios单独使用。以下是在中vue(vuecli)中***<u>正确</u>***使用axios的姿势！！

```javascript
//在main.js 中引用及配置
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

//然后就可以在任意地方随意的使用axios
this.$http.get("/post",{})
    .then(function(res){
    	console.log(res.data)
})

//------------------------------------------我更喜欢这么使用axios 也比较好理解
import Vue from 'vue'
import axios from 'axios'

axios.defaults.baseURL = 'http://127.0.0.1:8080';
Vue.prototype.$http = axios

//然后也是自由的翱翔
this.$http.get(）
```

# VUE-CLI

官方叫做，脚手架工具。个人理解：快速开发工具

## 安装及了解

- 确认NPM可以使用，node安装
- 安装vue-cli `npm i vue-cli -g`,全局安装：`C:\Users\Administrator\AppData\Roaming\npm`
- 使用vuec-cli，生成特定的文件目录(webpack:项目模板)`vue init webpack myvue`
- 在生成的项目中执行一些命令： `npm run dev`开启项目内置的服务器,并且对文件进行打包。
- 最后的打包：`npm run build`--dist文件夹
- 项目目录：
  - build webpack相关的文件（一般不会动）
  - config 内置的node服务器代码（一般也不会动）
  - node_modeles 项目用的所有包都在这里（客户端、服务器）
  - src  这是我们的主阵地，咱们的代码在这里写.项目运行以后，这里的所有文件被打包成一个文件app.js
  - static 也是放一些图片等外部文件
  - 一些测试文件，不会用到的
  - 其他的不说了
  - index.html 主网页：全局引入一些文件：reset.css
  - package.json 这是配置文件（整个项目的说明书）
    - dependencies    运行依赖包  ，项目打包完成以后也要使用
    - devDependencies 开发依赖，项目打包完成后是不需要他们
  - README.md  笔记
- 在当前myvue文件件下执行命令，运行项目：(开启内置的服务器，把所有的网页文件打包)：`npm run dev`
- 自动开启服务器：在`config/index.js`中将`autoOpenBrowser: true`,

## 主要文件

- index.html 这是整个网页主网页
- src/main.js  这是整个项目主程序  ：引入 vue 初始化vue实例 、引入vue的第三方插件
  - import --变量名--from- 文件路径-- 
  - 这个文件以后几乎不动，可能会引入其他第三方包，进行配置。

```javascript
//es6的新的语法 引入其他模块（包） 
import Vue from 'vue'  
import App from './App'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({ //初始化vue
  el: '#app',
  components: { App },
  template: '<App/>'
})
```

- App.vue 这是一个单文件组件，在main中使用。其他组件需要引入到App.vue进行使用。

> 以上三个文件的引用关系，webpack已经定义好了，我们基本上不用对他们进行修改。

- `src/router/index.js`中进行路由配置

## 单文件组件定义及调用

- 定义单文件组件`header.vue`，webpakc中使用单文件组件的方式定义组件，在使用时直接调用。

```javascript
<template>
	<div class="header">
		当前组件的模板
	</div>
</template>

<script>
 //当前组件的数据（js）
//	import.. from..
	export default{
		
	}
</script>

<style scoped="scoped">
	/*当前组件的css*/
	/*在组件的style中添加scoped属性,可以限制css的作用范围*/
	.header{
		background-color: #000000;
		overflow: hidden;
	}
</style>
```

- 在`App.vue`中引入`header.vue`并进行配置。

```javascript
<script>
	//在webpack的中，@代表的src的绝对目录
import myheader from "@/components/header.vue"
export default {
  name: 'App',
  components: {
  	myheader:myheader
 //将引入的组件配置为自己的组件选项
//  HelloWorld:HelloWorld
  }
}
</script>
```

- 在`App.vue`的模板中调用`header.vue`组件。

```html
<template>
  <div id="app">
  	<myheader></myheader>
    <!--<hello-world></hello-world>-->
  </div>
</template>
```

## 路由的使用

### 路由的基本使用

- 在`src/router/index.js`中进行路由的配置：

```javascript
import Vue from 'vue'
import Router from 'vue-router'
//引入需要的路由的组件
import myMain from '@/components/myMain.vue'
import myServer from '@/components/myServer.vue'

Vue.use(Router)

export default new Router({
  routes: [//设置路由规则：页面中的路径及对应显示组件
    { 
      path: '/', //页面中切换的路径
      name: 'myMain',
      //调用的组件
      component: myMain
    },
    {
      path: '/server',
      name: 'myServer',
      component: myServer
    },
  ]
})
```

- 在`App.vue`中调用组件：

```html
<template>
  <div id="app">
  		<my-header></my-header>
  		<!--调用路由的组件-->
  		<router-view></router-view>
  		<my-footer></my-footer>
  </div>
</template>
```

- 在任意位置使用`router-link`标签设置类似锚点跳转的效果，既可实现路由切换：

```html
<li><router-link to="/">网站首页</router-link></li>
<li><router-link to="/server">服务范围</router-link></li>
```

- `router-link`在编译之后显示为a标签。最终结果为`<a  href="#/">网站首页</a>`
- 正在被点击的a标签会添加一个类名，代表这个a被激活。通常用来添加辅助效果。`<a data-v-9d1d3a2e="" href="#/" class="router-link-exact-active router-link-active">网站首页</a>`

```css
.nav .menu li a.router-link-active{
    	/*将被选中的a设置为蓝色*/
		background-color: deepskyblue;
}
```

- 可以使用`vue-router`提供的属性`active-class='active'` 将默认的`router-link-active`更改为`active`
- 使用`tag`属性，将`router-link`显示为其他标签.`tag='span'`
- `vue-router`扩展的实例方法
  - `this.$router.push("/server")`,切换路由
  - `this.$router.replace("/server")`,切换路由，并且不会产生新的操作记录
  - `this.$router.go(-1)`,切换路由：根据操作的记录，返回上一步

### 多级路由：二级路由

在一级路由的基础上，设置二级路由：

```javascript
{
      path: '/server',
      name: 'myServer',
      component: myServer,
      children:[
      	{path:"/",component:server01},  //对应的切换路由为 #/server/
      	{path:"server02",component:server02}, //对应的切换路由为 #/server/server02
      ]
    },
```

- 二级路由只能显示在上一级路由对应的组件中：

```html
...
<div class="content">
	<h2>服务范围</h2>
	<!--这是在myServer 中调用的-->
	<router-view></router-view>
</div>
....
```

### 路由传值

- 传值教简单时，将需要传递的值定义在路由的name属性中。在页面中使用`{{$route.name}}`获取页面中正在显示的路由的name属性的值。
- 传值较多，或者比较复杂时。使用`to`属性传值。
  - `<router-link v-bind:to="{name:'index',params:{user:1}}" active-class="active" tag="span">跳转到临时页面</router-link>`
    - 路由切换到具有相同name值的组件
    - params中定义要传的值，调用方式为在页面中使用`{{$route.params.user}}`

### 高级使用

#### 多路由

- 组件定义

```javascript
components:{
    default:change01,
        z1:change02,
            z2:c1
}
```

- 组件显示

```javascript
<router-view name="z1"></router-view>
<router-view name="z2"></router-view>
<router-view></router-view>
```

#### 重定向

```javascript
path: '/server',
redirect:"/s"
```

#### 别名

```javascript
//一个路由，可以匹配多个路径
path: '/s',
alias:"/server",
```

#### 404页面

```javascript
path: '*',//匹配显示多有没有被路由到的的页面切换
```

#### 路由中的钩子函数

- 在index.js的路由选项中中，添加

```javascript
{
      path: '/s',
      alias:"/server",
      components:{
      	default:change01,
      	z1:change02,
      	z2:c1
      },
      beforeEnter:function(to,from,next){
      	console.log(to) //要切换到的组件（路由）的信息
      	console.log(from) //切换之前的路由的信息
      	alert(213)
      	next()
      }
    },
```

- 直接在组件中定义路由的钩子函数：

```javascript
export default {
		name:"server",
		 beforeRouteEnter:function(to,from,next){
		 	alert("组件要显示了")
		 	next()
		 },
		 beforeRouteLeave:function(to,from,next){
		 	alert("组件要离开了")
		 	next()
		 }
}
```

## vue过渡与动画

### 过渡

> vue的动画是在组件（DOM/标签），插入、创建、移除时添加。--------动画是在标签的显示与隐藏过程中添加。

```html
Vue 在插入、更新或者移除 DOM 时，提供多种不同方式的应用过渡效果。
		--------
	 	使用transition 包裹标签以后，在标签的显示和隐藏过程中都会自动添加一些类名，我们通过这些类名添加过渡动画。
	 	.v-enter-active : 在标签显示过程中,都有效 ---添加transition属性，控制变化过程。
	 	.v-enter:标签刚开始显示有效---设置标签开始显示的状态（状态1）
	 	.v-enter-to:标签显示完成以后有效---设置标签的显示状态（状态2）
	 	--------简单理解：显示以后        添加两个状态：通过过度控制状态变化
	 	.v-leave-active: 控制整个隐藏过程
	 	.v-leave:隐藏时添加的第一个状态
	 	.v-leave-to:隐藏时添加的第二个状态
	 	--------简单理解：隐藏之前      添加两个状态：通过过渡控制状态变化
```

- 案例：

```html
-----
<transition>
    <p v-if="show" class="p1">hello</p>
</transition>
-----
```

### 动画

用法与过度一致，只在`.v-enter-active`和`.v-leave-active`,设置`annimation`属性即可。

### 动画的钩子函数

```javascript
<transition
  v-on:before-enter="a"
  v-on:enter="b"
  v-on:after-enter="b"
  v-on:enter-cancelled="enterCancelled"

  v-on:before-leave="beforeLeave"
  v-on:leave="leave"
  v-on:after-leave="afterLeave"
  v-on:leave-cancelled="leaveCancelled"
>
  <!-- ... -->
</transition>
```

```javascript
methods:{
    a:function(el){
        el.style.transition="all 5s";
        el.style.width="100px";
        el.style.height="100px";
    },
        b:function(el,done){
            //随便获取一个标签相关的大小，位置 （js三大家族，特效专用属性）：触发动画执行
            el.offsetHeight;
            el.style.width="200px";
            el.style.height="200px";
            // done的作用是调用第三个事件，正常境况下第三个事件会延迟执行，这样可以让第三个之间立即执行
            done()
        },
            c:function(el){
                //				alert("过度完成")
            }
}
```

### 多个标签的过渡

```html
<transition mode="in-out">
    <button v-if="show" key="a" key="a">
        11111
    </button>
    <button v-else key="b" key="b">
        22222
    </button>
</transition>
```

- 为了区别各个标签，需要给标签添加`key`属性

- 默认情况下，都是第一个标签先指定过渡效果，第二个标签再执行过渡效果。
- 动过过渡模式改变这个顺序
  - `in-out`:先显示后隐藏
  - `out-in`:先隐藏后显示

### 列表过渡

- 使用`transtion-group`包裹需要过渡的列表项

```html
<transition-group appear>
    <div class="list" v-for="(list,index) in lists" v-bind:key="index">{{list}}</div>
</transition-group>
```

- 设置过渡的方式与`transtion`中是一样的

```css
.v-enter-active{
    transition: all 1s; 
}
.v-enter{
    left: 1366px;
}
.v-enter-to{
    left: 0;
}
```

- 通过改变数据的数据，添加或者删除某一项

### 使用css插件:animate.css

- 作为包来配置
  - 安装`npm install animate.css --save`
  - 配置：在main中作为插件引入及配置

```javascript
import Vue from 'vue'
import App from './App'
import router from './router'
//import animate from 'animate.css'
Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
//animate,
  components: { App },
  template: '<App/>'
})

```

- 直接作为普通的css文件引入:一般就是在APP.vue 中为外部css引入

```html
<style scoped="scoped">
	@import url("./assets/animate.css");
</style>
```

- 使用：在过渡的`transition`或者是`transition-group`上直接调用插件的特效
  - `enter-active-class="animated bounceIn" ` 设置进入的动画
  - `leave-active-class="animated bounceOut"` 设置离开的动画

```html
<transition enter-active-class="animated bounceIn" leave-active-class="animated bounceOut">
```

## 使用`element-ui`组件UI库

- 下载`npm i element-ui --save`
- 配置

```javascript
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

- 使用

> 配置完成之后，就可以直接复制使用需要的组件。