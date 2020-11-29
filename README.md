# recruit-easz (React+Node+MongoDB)

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

### Intro

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

*=============file structure===============*

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

### Back-end

- `MongoDB`
- database useage please refer `mongodb.md` under `data` folder
* database: **(mongoose)**

- back-end: `node`+`express`

* back-end files: `server` folder



# Usage

* mongo + react + node 8.0+

* ```js
  // option 1
  npm install 
  npm run build 
  npm run server 
  localhost:9093
  ```

* ```js
  // option 2
  npm install 
  cd server
  node main.js
  npm run start
  localhost:3000
  ```

