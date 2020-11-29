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

* **(cookie storage)** `browser-cookies`

* **(node request data)** `body-parser`

* **(React send request)** `axios`

* **(react components communication type)** `prop-types`

* **(React and Redux data communication)** `react-redux`

* **(React router config)** `react-router`

* **(React animation)** `rc-queue-anim`

* **( about Redux decorator)**`babel-plugin-transform-decorators-legacy`

* file structure

```js
    // project structure
    ├─build
    ├─config
    ├─data
    │  ├─MongoDB            				  // DB    
    ├─server  								  // back-end
    │  ├─model          					  // data-model
    │  ├─main          				  		  // back-end entry
    │  ├─user          				 		  // back-end api    
    ├─src
    │  ├─components                           // global components
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
    │  ├─router                                // router
    │  ├─index                                 // entry
    │  ├─util                                  // methods
    │  ├─config                                // request interception
    │  └─container
    │      ├─bossinfo   					   
    │      ├─login          				   
    │      ├─register                          
    │      └─genuisinfo                      

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

