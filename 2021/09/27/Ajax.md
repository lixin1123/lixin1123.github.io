# Ajax

## 1. 过程

```javascript
const xhr = new XMLHttpRequest()
xhr.open('get', url, true)
xhr.send()
xhr.onreadystatechange = function() {
	if(xhr.readyState === 4) {
		if(xhr.status === 200) {
			console.log(xhr.responseText)
		}
	}
}
```

## 2. 实例属性

#### 2.1 readyState

- 0，表示 XMLHttpRequest 实例已经生成，但是实例的`open()`方法还没有被调用。
- 1，表示`open()`方法已经调用，但是实例的`send()`方法还没有调用，仍然可以使用实例的`setRequestHeader()`方法，设定 HTTP 请求的头信息。
- 2，表示实例的`send()`方法已经调用，并且服务器返回的头信息和状态码已经收到。
- 3，表示正在接收服务器传来的数据体（body 部分）。这时，如果实例的`responseType`属性等于`text`或者空字符串，`responseText`属性就会包含已经收到的部分信息。
- 4，表示服务器返回的数据已经完全接收，或者本次接收已经失败。

#### 2.2 onreadytstatechange

#### 2.3 xhr.response === xhr.responseText

#### 2.4 xhr.responseType

返回类型是xhr.responseType (该属性可写，在open之后，send之前)

- ”“（空字符串）：等同于`text`，表示服务器返回文本数据。
- “arraybuffer”：ArrayBuffer 对象，表示服务器返回二进制数组。
- “blob”：Blob 对象，表示服务器返回二进制对象。
- “document”：Document 对象，表示服务器返回一个文档对象。
- “json”：JSON 对象。
- “text”：字符串

#### 2.5 xhr.responseXML

返回从服务器接受到的HTML或XML文档

前提：responseType = 'document'  （是 HTTP 回应的Content-Type头信息等于text/xml或application/xml）

#### 2.6 xhr.responseURL

发送数据的的服务器的网址。

这个属性的值与open()方法指定的请求网址不一定相同

#### 2.7 status statusText

#### 2.8 xhr.timeout && xhr.ontimeout

timeout设置超时的秒数， ontimeout设置超时时对应的操作

```javascript
 xhr.timeout = 100
 xhr.ontimeout = function() {
   console.log('超时')
 }
```

#### 2.9 事件监听属性

- XMLHttpRequest.onloadstart：loadstart 事件（HTTP 请求发出）的监听函数
- XMLHttpRequest.onprogress：progress事件（正在发送和加载数据）的监听函数
- XMLHttpRequest.onabort：abort 事件（请求中止，比如用户调用了`abort()`方法）的监听函数
- XMLHttpRequest.onerror：error 事件（请求失败）的监听函数
- XMLHttpRequest.onload：load 事件（请求成功完成）的监听函数
- XMLHttpRequest.ontimeout：timeout 事件（用户指定的时限超过了，请求还未完成）的监听函数
- XMLHttpRequest.onloadend：loadend 事件（请求完成，不管成功或失败）的监听函数

onprogress示例

```javascript
//有三个参数 e.total返回的总数据量 e.loaded已传输的数据量 e.lengthComputable 进度是否可以计算
xhr.onprogress = function(e){
  console.log(e, '111111')
}
```

#### 2.10 withCredentials

```javascript
xhr.withCredentials = true
//表明跨域请求时，请求中会带有cookie
```

#### 2.11 upload

upload是指上传文件。xhr.upload返回的是对象，这个对象有各种监听事件：loadstart、loadend、load、abort、error、progress、timeout

```javascript
xhr.open('post', '/server', true)
xhr.upload.onprogress = function(e) {
	console.log(e.total, e.loaded)
}
```

## 3.实例方法

#### 3.1 open()

```javascript
void open(
   string method,
   string url,
   optional boolean async,
   optional string user,
   optional string password
);
```

- `method`：表示 HTTP 动词方法，比如`GET`、`POST`、`PUT`、`DELETE`、`HEAD`等。
- `url`: 表示请求发送目标 URL。
- `async`: 布尔值，**表示请求是否为异步，默认为`true`**。如果设为`false`，则`send()`方法只有等到收到服务器返回了结果，才会进行下一步操作。该参数可选。由于同步 AJAX 请求会造成浏览器失去响应，许多浏览器已经禁止在主线程使用，只允许 Worker 里面使用。所以，这个参数轻易不应该设为`false`。
- `user`：表示用于认证的用户名，默认为空字符串。该参数可选。
- `password`：表示用于认证的密码，默认为空字符串。该参数可选。

#### 3.2 send(objects)

objects 选填，表示请求头带的参数

```javascript
xhr.open('post', '/server')
const data = {
	name: 'lixin',
	age: 23
}
xhr.send(data)
```

#### 3.3 setRequestHeader()

设置发送的请求头，必须在open之后，send之前

#### 3.4 overrideMimeType()

当获取不到服务器返回的信息时，改变返回数据格式，必须在open之后，send之前

#### 3.5 getResponseHeader()

```xhr.getResponseHeader('Last-Modified')```

#### 3.6 getAllResponseHeader()

#### 3.7 abort()

终止请求

## 4.实例事件

#### 4.1 readyStateChange事件

#### 4.2 progress事件

#### 4.3 load error abort loadend

load表示数据接受完毕

error表示请求出错

abort 请求中断

loadend 请求结束



