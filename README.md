# 简招 (React+Node+MongoDB)

> start date: 2020-10-10 
> end date: 2020-11-06

<p align="center" style="margin:50px 0;">
	<img src="https://img.shields.io/badge/language-html%20%7C%20javascript-blue" />
    <img src="https://travis-ci.org/2662419405/sh.svg?branch=master"  />
    <img src="https://img.shields.io/badge/version-v1.0-informational" />
    <img src="https://img.shields.io/badge/codecov-25-red" />
    <img src="https://img.shields.io/badge/platform-ios%20%7C%20android%20%7C%20widdow%20%7C%20ipad-inactive"  />
    <img src="https://img.shields.io/badge/weibo-%40SH-blueviolet"  />
</p>

### 介绍

Campus Recruitment APP is a mobile job search website. Recruiters can register as BOSS, job seekers can register as pro, Pros and BOSS can chat, and can view each other's basic information and profile salary

*=============package explained===============*

* **(load on demand)** `babel-plugin-import`

* **(cross domain)** `package.json` in `proxy`

* **(password encryption)** `utility`

* **(关于cookie存储方面的问题)** 使用`browser-cookies`包

* **(方面node中获取请求的数据)** 使用`body-parser`包

* **(在React中发送请求)** 使用`axios`包

* **(加强react中组件之间的通信类型)** 使用`prop-types`包

* **(React和Redux之间的数据通信)** 使用`react-redux`包

* **(React中的路由配置)** 使用`react-router`包

* **(React中的动画)** 使用`rc-queue-anim`包

* **(关于Redux的装饰器)**使用`babel-plugin-transform-decorators-legacy`包

  * 这里需要详细说明一下,安装完这个包之后,需要在`package.json`文件中中babel上加入

  * `"plugins": ["transform-decorators-legacy"]`

  * ```json
    "babel": {
        "presets": [
            "react-app"
        ],
        "plugins": [
            "transform-decorators-legacy"
        ]
    },
    ```
  
* **(配置服务端渲染)** 使用`babel-cli`包

  * 安装

  * ```js
    npm install babel-cli --save 
    ```

  * 配置package.json

  * ```js
    "server": "set NODE_ENV=test&&nodemon --exec babel-node -- server/main.js"
    ```



* 目录结构

```js
    // 项目结构
    ├─build
    ├─config
    ├─data
    │  ├─MongoDB            				  // 数据库解释    
    ├─server  								  // 后台
    │  ├─model          					  // 数据库原型     
    │  ├─main          				  		  // 后台文件入口  
    │  ├─user          				 		  // 后台接口api    
    ├─src
    │  ├─components                           // 全局组件
    │  │  ├─autoRouter
    │  │  ├─avatar-select
    │  │  ├─boss
    │  │  ├─chat
    │  │  ├─Dashboard
    │  │  ├─genius
    │  │  ├─img
    │  │  ├─logo
    │  │  ├─msg
    │  │  ├─navlink
    │  │  ├─shForm
    │  │  ├─user
    │  │  └─chatCard
    │  ├─router                                // 路由
    │  ├─index                                 // 入口	
    │  ├─util                                  // 方法
    │  ├─config                                // 请求拦截
    │  └─container
    │      ├─bossinfo   					   // boss
    │      ├─login          				   // 登录
    │      ├─register                          // 注册
    │      └─genuisinfo                        // 牛人

```



> 注册时, 进行密码MD5加密



``` js
// md5加密
function md5pwd(pwd){
    const salt = 'qwe123~~-!@#$%^&&*()sunhang'
    return utility.md5(utility.md5(salt+pwd))
}
```



> 进行登录以及cookie的存储



```js
//进行注册
Router.post('/register',(req,res)=>{
    const { user,pwd,type } = req.body
    User.findOne({user},(err,doc)=>{
        if(doc){
            return res.json({code:1,msg:'用户名存在'})
        }
        const userModel = new User({user,type,pwd:md5pwd(pwd)})
        userModel.save(function(e,d){
            if(err){
                return res.json({code:2,msg:'后端出错了'})
            }
            const {user,type,_id} = d
            res.cookie('userid',_id)
            return res.json({code:3,msg:'注册成功',data:{user,type,_id}})
        })
    })
})
```



> axios拦截器的制作



```js
import axios from 'axios'
import { Toast } from 'antd-mobile'

//拦截请求
axios.interceptors.request.use(function(config){
    Toast.loading('加载中',0);
    return config;
})

//拦截响应
axios.interceptors.response.use(function(config){
    Toast.hide();
    return config;
})
```



* 登录和注册效果展示

![sh](https://studyit.club/Study/register.gif)

* 双方聊天展示

![sh](https://studyit.club/Study/chat.gif)



* 消息的更新和排序

![sh](https://studyit.club/Study/clear.gif)



* 手机端表情包展示

![sh](https://studyit.club/Study/Screenshot_2019-10-24-14-14-39-53_cb819d8fa60af39.jpg)

> 手机端的表情包就是可以用的,现在的表情包都可以直接使用了,不同代码了,很神奇



### 后台方向

- 由于本人主要是面向前端,数据库就是`MongoDB`
- 数据库的使用请参照`data`目录下面的`mongodb.md`
* 数据库方面使用 **(mongoose)**

- 后台主要使用`node`的`express`

* 后台文件在`server`



# 使用方式

* 需要电脑有 mongo 和 react 还有node环境

* 首先:下载本项目

* ```js
  // 第一种方式
  npm install //安装包依赖
  npm run build //打包项目
  npm run server //启动  打开浏览器输入localhost:9093
  ```

* ```js
  // 第二种方式
  npm install //安装包依赖
  cd server  //进入后台
  node main.js  //运行后台
  //再打开一个cmd
  npm run start //启动  打开浏览器输入localhost:3000
  ```


如果还有bug和建议,欢迎告诉我  (͏ ˉ ꈊ ˉ)✧˖°

![sh](https://studyit.club/Study/qq.jpg)



>  一开始还是遇到了很多的坑,第一次使用antd-mobile这个库,最主要的坑,还是对于项目的上线运行,毕竟个人不太擅长服务器的使用,在配置Nginx的时候卡了很久,为了性能优化,SSR渲染也是花了很大的心血,感觉里面的坑太多了,总的来说收获还是很大的,后期我还会画时间进行界面上的美化
>
> 感觉支持  喜欢的朋友记得给个star  
