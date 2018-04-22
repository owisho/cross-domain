# cross-domain
跨域知识学习
## 跨域产生的原因：
浏览器限制
跨域（协议/端口/域名不同）
XMLHttpReqeust请求（google浏览器限制type--xhr）
## 解决思路
浏览器不限制跨域问题    
使用非XHR请求调用JSONP   
服务器端在返回的信息中加入字段告诉浏览器允许调用方调用   
调用方使用代理将调用方的域名指定到被调用方的域名，这样浏览器就不会认为请求是跨域的请求了    

### 指定浏览器参数不进行校验
chrome启动是添加参数  --disable-web-security --user-data-dir=g:\temp3   

### 什么是JSONP
jsonp是一个非官方协议   
协议的内容是服务器和浏览器双方进行约定，请求的参数中如果有指定的参数（默认是callback），那么这个请求就是一个jsonp请求，   
服务器发现请求是jsonp请求，会把返回值由原来的json对象改为js代码，js代码的内容是函数调用的形式，它的函数名是callback参数的值，   
它的函数的参数是原来要返回的json对象   


### jsonp 是动态创建的javascript标签
springboot 项目中可以使用AbstractSJsonpResponseBodyAdvice将请求的respone转化成jsonp要求的script格式     
jsonp请求的请求类型type 是script    
jsonp的返回类型是application/javascript     
jsonp是创建一个动态调用的script的脚本    
其中函数名是callback参数的值    
函数的参数是实际要返回的json数据   

### jsonp有什么弊端
服务器需要改动代码支持    
只支持get    
发送的不好似XHR请求    


### 简单请求和非简单请求
简单请求    
GET    
HEAD    
POST    
且请求头里无自定义头    
Content-Type为以下几种：       
text/plain     
multipart/form-data     
application/x-www-form-urlencoded     
其他的就是非简单请求    

工作中常见的【非简单请求】有：     
put,delete方法的ajax请求        
发送json格式的ajax请求       
带自定义头的ajax请求    
