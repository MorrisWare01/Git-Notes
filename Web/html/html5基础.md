# HTML5基础

#### DOCTYPE 文档类型与浏览器模式

> DTD（document type definition，文档类型定义）是一系列的语法规则， 用来定义XML或(X)HTML的文件类型。浏览器会使用它来判断文档类型， 决定使用何种协议来解析，以及切换浏览器模式。

`<!DOCTYPE html>`

#### 文档字符编码

`<META charset=“utf-8”>`

#### html5结构化标签

```
<header> 标记构建页面的页头
<nav> 标记构建页面的导航
<section> 标记构建页面的一块区域
<article> 标记构建页面的内容
<aside> 标记构建页面的相关辅助信息
<footer> 标记构建页面的页脚
```

## Web存储

### Cookie存储

#### 概念
* 使用文本来存储信息，当有客户端使用Cookie时，服务器端就会发送Cookie到客户端，客户端将保存该信息，下一次页面请求时，客户端就会把Cookie发送的到服务器
* 典型应用于用来保存用户信息、用户设置、密码记忆等

#### 优缺点

##### 优点
* 简单易用
* 浏览器负责发送数据
* 浏览器自动管理不同站点的Cookie

##### 缺点
* 使用简单的文本储存数据，导致Cookie的安全性很差
* Cookie保存在客户端浏览器，很容易被窃取
* Cookie的容量有限，上限为4KB
* 存储Cookie的数量有限，多数浏览器上限为30或50个
* 如果浏览器的安全配置为最高级别，Cookie会失效
* Cookie不适合大量数据的存储，因为Cookie由每次对服务器的请求来传递，从而造成Cookie速度缓慢效率低下

### Web Storage

#### 概念
* 客户端存储数据，包含localStorage和sessionStorage
* localStorage是一种没有时间限制的数据存储方式，可以将数据保存在客户端的硬盘或其他存储器
* sessionStorage针对某一个session的数据存储，即将数据保存在session对象中，当退出浏览器时，数据被清除

#### 优缺点

##### 优点
* 存储空间相对于Cookie大得多
* 存储数据不会发送到服务器
* 提供了一套丰富的接口
* 独立的存储空间，每个域(包括子域)都有独立的存储空间，各个空间完全独立

##### 缺点
* 浏览器会为每个域分配独立的存储空间，即脚本在域A中无法访问到域B中的存储空间，但是浏览器不会检查脚本所在的域与当前域是否相同，即在域B中嵌入域A中的脚本依然可以访问域B的数据
* 存储在本地的数据未加密而且永远不会过期，极易造成隐私泄漏

#### 使用

检查是否支持webStorage
```language
function checkStorageSupport(){
	if(window.sessionStorage){
    	...
    }
    if(window.localStorage){
    	...
    }
}
```
基本操作API
```language
length 获取storage的键值对数量
key(index) 获取指定索引的键值
getItem(key) 根据键值获取数据
setItem(key,value) 根据键值设置数据
removeItem(key) 根据键值删除键值对
clear() 清除所有键值对
```
事件监听
```language
function displayStorageEvent(e){
	e.key + e.newValue + e.oldValue + e.url + e.storageArea(影响储存对象)
}
window.addEventListener("storage",displayStorageEvent,true)
```

## 离线应用

### manifest文件

#### 文件结构
* 第一行必须以CACHE_MANIFEST开头
* 注释使用‘#’开头
* 编码必须为UTF-8
* CACHE MANIFEST节点指明无论应用程序是否在线，浏览器都会从应用程序缓存中获取该文件
* CHCHE：节点指明缓存入口
* NETWORK：节点指明资源必须在线访问
* FALLBACK：节点下每行包含两个URL，第一个为资源文件URL，第二个为回调页面URL，当资源文件URL无法正常访问时，使用回调页面URL
* 节点无先后顺序，在文件中可以多次出现

#### 添加注释行的文件版本的好处(#app v1)
* 很明确地了解离线Web应用的版本
* 通过简单地修改版本号就可以轻易地通知浏览器进行更新
* 可以配合JavaScript程序来完成缓存更新

### 离线缓冲更新实现
* 配置服务器manifest文件的MIME类型
* 编写manifest文件
* 在页面的html元素的manifest属性中引用manifest文件

### 更新缓存
* 清除离线存储的数据
* 修改manifest文件
* 使用JavaScript编写更新程序

#### 使用JavaScript编写更新程序

##### 缓存状态
* 0 UNCACHED 未使用缓存
* 1 IDLE 空闲，说明所有资源都已被浏览器缓存，不需要更新
* 2 CHECKING 检查中，检查是否有缓存更新
* 3 DOWNLOADING 下载中，下载最新缓存到本地
* 4 UPDATEREADY 缓存更新就绪，监听就绪状态更新html
* 5 OBSOLETE 过期，缓存过期，缓存文件丢失

##### window.applicationCache API
* update(): 尝试更新，有缓存更新就进行下载
* swapCache(): 更新到最新的应用缓存

```language
window.applicationCache.onchecking = (e) =>{
	console.log(e)
}

window.applicationCache.onnoupdate = (e) =>{
	console.log(e)
}

window.applicationCache.onobsolete = (e) =>{
	console.log(e)
}

window.applicationCache.ondownloading = (e) =>{
	console.log(e)
}

window.applicationCache.oncached = (e) =>{
	console.log(e)
}

window.applicationCache.onupdateready = (e) =>{
	console.log(e)
	window.applicationCache.swapCache()
	if (confirm('有新版本，是否更新？')) {
        window.location.reload();
  }
}

window.applicationCache.onerror = (e) =>{
	console.log(e)
}

window.addEventListener("online",(e) =>{
	console.log(e)
},true)

window.addEventListener("offline",(e) =>{
	console.log(e)
},true)

let statusMessage = ["没有使用缓存","空闲","正在检查。。。","正在下载。。。","更新完成","过期"]
export const showCacheStatus = (n) => statusMessage[n]

checkCache () {
	console.log('检查更新')
    cache.update()
}
```

## Workers 多线程
### 概述
* 使用postMessage(event),onMessage(event)进行前后台数据交互
* worker不能反问该页面的window对象
* 可以使用setTimeout()、clearTimeout()、setInterval()、clearInterval()
* 使用workers加载数据没有jsonp和ajax加载数据高效

### Workers中可用的变量、函数、类
* self: 本线程范围内的作用域
* postMessage(message):向创建线程的源窗口发送消息
* onMessage(message): 获取接受消息的句柄
* importScripts(urls): 导入其他脚本文件，文件必须与使用该线程文件的页面在同一域，同一端口
* mavigator对象: 用来标记浏览器的字符(appName,platform,userAgent,appVersion)
* sessoinStorage/localStorage: 可以使用web storage
* XMLHttpRequest: 处理ajax请求
* web works: 嵌套线程
* setTimeout()/setInterval()
* close: 结束线程
* object: 可以创建本地对象
* websockets: 可以使用websocketapi项服务器发送和接受信息

### 使用
```language
// 判断浏览器是否支持
if(typeof(Worker) !== 'undefined'){

}
// 将脚本作为参数创建Worker对象
var worker = new Worker("worker.js")
// 处理接受到的消息
worker.onmessage = function(event){

}
```

## Geolocation地理位置
```language
var x=document.getElementById("demo");
function getLocation()
{
  // 判断是否支持定位
  if (navigator.geolocation)
  {
    navigator.geolocation.getCurrentPosition(showPosition);
  }
  else{x.innerHTML="Geolocation is not supported by this browser.";}
}
function showPosition(position)
{
  x.innerHTML="Latitude: " + position.coords.latitude +
  "<br />Longitude: " + position.coords.longitude;
}
```