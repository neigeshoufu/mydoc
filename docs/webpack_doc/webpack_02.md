## **在webpack中使用Vue**
### **1.使用组件**
#### **1.1配置**
- 安装Vue.js
```
npm i vue-loader vue-template-compiler -d
```
- 安装vue-loader-plugin
```
npm i vue-loader-plugin -S
```
- 配置vue-loader-plugin
```
//踩坑记录！！！
//Vue-loader在15.*之后的版本都是 vue-loader的使用都是需要伴生 VueLoaderPlugin的
const VueLoaderPlugin = require('vue-loader/lib/plugin')
...
plugins: [
        new VueLoaderPlugin()  //注册VueLoaderPlugin
    ],
```
- 在main.js项目入口文件中引入```Vue.js```。
```
import Vue from 'vue'
//或者
import Vue from '../node_modules/vue/dist/vue.js'
```
- ⚠```import Vue from 'vue'```这种方式，引入的是vue.common.js，导入的Vue功能不完整.只提供了runtime-only的方式。使用这种需要配合```render```渲染组件:
**index.js**
```
var vm = new Vue({
    el:'#app',
    data:{
        msg:123
    },
    //  components:{
    //      login
    //  }
    // render: function (createElement) {  //通过runtime-only把一个组件放到页面中，需要用render
    //     return createElement(login)
    // }
    //简写
    render: c => {  //通过runtime-only把一个组件放到页面中，需要用render
        c(login)
    }
})
```
#### **1.2 抽离组件**
- 新建```login.vue```
```
<template>
    <div>
        <h1>这是登陆组件，使用.vue文件定义出来的</h1>
    </div>
    
</template>

<script>
export default{
    data(){
        return{
            msg:123
        }
    },
    methods: {
        show(){
            console.log('调用了login.vue上的show方法');
            
        }
    }
}
</script>


<style>

</style>
```
- ```index.js```中引入```login.vue```
```
//导入login组件
import  login from './login.vue'  
```
- **⚠注意：**
```
webpack无法打包.vue，需要相关loader
npm i vue-loader vue-template-compiler -d
配置文件中新增配置项 {test:/\.vue$/,user:'vue-loader'}
```
- 然后使用```render```将组件放到页面中。注意这个组件会覆盖```#app```

### **2.使用路由**
#### **2.1 配置**
- 安装```vue-loader```
```
npm i vue-router -s
```
- 引入路由
```
//导入路由
import VueRouter from 'vue-router'
```
- 手动创建路由及其对象
```
Vue.use(VueRouter)

//创建路由对象
var router = new VueRouter({
    routes:[
        {path:'/account',component:account},
        {path:'/goodlist',component:goodlist},
    ]
})
```
- 挂载路由对象
```
var vm = new Vue({
    el:'#app',
    render:c => c(app),   //不要把router-view 直接写到app里面
    router  //将路由对象挂载
})
```
#### **2.2 组件化**
- 导入```.vue```组件化
```
//导入组件
import account from './main/account.vue'
import goodlist from './main/goodlist.vue'
```
- 如1.1创建路由对象
- 显示路由
**在主组件,把路由放到页面上**
```
<template>
    <div>
        <h1>这是app组件</h1>
        <router-link to="/account">Account</router-link>
        <router-link to="/goodlist">Goodlist</router-link>

        <router-view></router-view>
    </div>
    
</template>
```
#### **2.3 抽离路由**
- 新建```router.js```
- 引入子组件
```
// //导入Account的两个子组件
import login from './subcom/login.vue'
import register from './subcom/register.vue'
```
- ```index.js```里面要导入```router.js```
- 在```router.js```里面配置
```
**路由抽离 */
import VueRouter from 'vue-router'

import account from './main/account.vue'
import goodlist from './main/goodlist.vue'

//导入Account的两个子组件
import login from './subcom/login.vue'
import register from './subcom/register.vue'



//创建路由对象
var router = new VueRouter({
    routes:[
        {
            path:'/account',
            component:account,
            children:[  //account的子路由
                {path:'login',component:login},
                {path:'register',component:register}
            ]
        },
        {path:'/goodlist',component:goodlist},
    ]
})

/**将路由暴露出去 */
export default router
```
### **3.样式**
#### **3.1 在抽离的组件中使用局部样式**
- 为```style```标签添加```scoped```属性
```
<style scoped>
div{
    color:red;
}
</style>
```
#### **3.2 使用```less```,```scss```**
- 设置```lang```属性
```
<style lang="scss" scoped>
/**普通的style标签只支持普通的样式less或scss需要给style设置lang属性 */
/**只要style在组件中的 都建议开启scoped属性 局部生效样式 */
body{
    div{
        font-style: italic;
    }
}
</style>
```


### **4.注意**
```
1、ES6中，使用export default和export向外暴露成员，如：test.js
export default{
    name:'zs',
    age:22
}

var abc export{
    ...
}
注意：export default向外暴露的成员，可以使用任意的变量来接收，如：
import m22,{title} from './test.js'
注意：在一个模块中，export default只允许向外暴露一次，
export 可以暴露多次。export暴露的成员，使用{}的形式来接收，按需导出
可以起别名：
import m22, { title as title 123,content} from './test.js'
```
