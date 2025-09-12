---
title: Axios
date: 2019-10-08 15:38:24
categories: 
- 前端知识
tags:
- Axios
---

### vue中最优axios封装

1.安装axios

```
cnpm install axios -S
```

2.请求拦截器

```
import axios from 'axios';
import \\{ Message \\} from 'element-ui';

axios.defaults.timeout = 5000;
axios.defaults.baseURL ='';


//http request 拦截器
axios.interceptors.request.use(
  config => \\{
    // const token = getCookie('名称');注意使用的时候需要引入cookie方法，推荐js-cookie
    config.data = JSON.stringify(config.data);
    config.headers = \\{
      'Content-Type':'application/x-www-form-urlencoded'
    \\}
    // if(token)\\{
    //   config.params = \\{'token':token\\}
    // \\}
    return config;
  \\},
  error => \\{
    return Promise.reject(err);
  \\}
);

//http response 拦截器
axios.interceptors.response.use(
  response => \\{
    if(response.data.errCode ==2)\\{
      router.push(\\{
        path:"/login",
        querry:\\{redirect:router.currentRoute.fullPath\\}//从哪个页面跳转
      \\})
    \\}
    return response;
  \\},
  error => \\{
    return Promise.reject(error)
  \\}
)
```

3.封装请求方法

```
/**
 * 封装get方法
 * @param url
 * @param data
 * @returns \\{Promise\\}
 */

export function fetch(url,params=\\{\\})\\{
  return new Promise((resolve,reject) => \\{
    axios.get(url,\\{
      params:params
    \\})
    .then(response => \\{
      resolve(response.data);
    \\})
    .catch(err => \\{
      reject(err)
    \\})
  \\})
\\}


/**
 * 封装post请求
 * @param url
 * @param data
 * @returns \\{Promise\\}
 */

 export function post(url,data = \\{\\})\\{
   return new Promise((resolve,reject) => \\{
     axios.post(url,data)
          .then(response => \\{
            resolve(response.data);
          \\},err => \\{
            reject(err)
          \\})
   \\})
 \\}

 /**
 * 封装patch请求
 * @param url
 * @param data
 * @returns \\{Promise\\}
 */

export function patch(url,data = \\{\\})\\{
  return new Promise((resolve,reject) => \\{
    axios.patch(url,data)
         .then(response => \\{
           resolve(response.data);
         \\},err => \\{
           reject(err)
         \\})
  \\})
\\}

 /**
 * 封装put请求
 * @param url
 * @param data
 * @returns \\{Promise\\}
 */

export function put(url,data = \\{\\})\\{
  return new Promise((resolve,reject) => \\{
    axios.put(url,data)
         .then(response => \\{
           resolve(response.data);
         \\},err => \\{
           reject(err)
         \\})
  \\})
\\}
```

4.在main.js中引入，注册到原型

```
import axios from 'axios'
import \\{post,fetch,patch,put\\} from './utils/http'
//定义全局变量
Vue.prototype.$post=post;
Vue.prototype.$fetch=fetch;
Vue.prototype.$patch=patch;
Vue.prototype.$put=put;
```

5.最后在组件里直接使用

```
mounted()\\{
    this.$fetch('/api/v2/movie/top250')
      .then((response) => \\{
        console.log(response)
      \\})
  \\},
//其余的方法一样
```



### 关于axios如何在请求头添加参数

```
vm.$http.post(apiUrl.refundOrder, data,\\{
    headers:\\{
        'lz-shopid':vm.orderRecords.shopId
    \\}
\\}).then(res => \\{
    if(res.code==1)\\{
        vm.$toast.center(res.message)
    \\}
\\}).catch(error => \\{
     
\\})
```

```
export function fetch(url, params = \\{\\},headers) \\{
  return new Promise((resolve, reject) => \\{
    axios.get(url, \\{
        params: params,
        headers:headers.headers
      \\})
      .then(response => \\{
        resolve(response.data);
      \\})
      .catch(err => \\{
        reject(err)
      \\})
  \\})
\\}
```



### post使用form-data和x-www-form-urlencoded的本质区别

一是数据包格式的区别，二是数据包中非ANSCII字符怎么编码，是百分号转码发送还是直接发送

#### 一、application/x-www-form-urlencoded

1、它是post的默认格式，使用js中URLencode转码方法。包括将name、value中的空格替换为加号；将非ascii字符做百分号编码；将input的name、value用‘=’连接，不同的input之间用‘&’连接。

2、百分号编码什么意思呢。比如汉字‘丁’吧，他的utf8编码在十六进制下是0xE4B881，占3个字节，把它转成字符串‘E4B881’，变成了六个字节，每两个字节前加上百分号前缀，得到字符串“\\%E4\\%B8\\%81”，变成九个ascii字符，占九个字节（十六进制下是0x244534254238253831）。把这九个字节拼接到数据包里，这样就可以传输“非ascii字符的  utf8编码的 十六进制表示的 字符串的 百分号形式”，^_^。

3、同样使用URLencode转码，这种post格式跟get的区别在于，get把转换、拼接完的字符串用‘?’直接与表单的action连接作为URL使用，所以请求体里没有数据；而post把转换、拼接后的字符串放在了请求体里，不会在浏览器的地址栏显示，因而更安全一些。

#### 二、multipart/form-data

1、对于一段utf8编码的字节，用application/x-www-form-urlencoded传输其中的ascii字符没有问题，但对于非ascii字符传输效率就很低了（汉字‘丁’从三字节变成了九字节），因此在传很长的字节（如文件）时应用multipart/form-data格式。smtp等协议也使用或借鉴了此格式。

2、此格式表面上发送了什么呢。用此格式发送一段一句话和一个文件，请求体如下

同时请求头里规定了Content-Type: multipart/form-data; boundary=----WebKitFormBoundarymNhhHqUh0p0gfFa8

可见请求体里不同的input之间用一段叫boundary的字符串分割，每个input都有了自己一个小header，其后空行接着是数据。

3、此格式实际上发送了什么呢。fiddler抓包如下

右边明显看到了一段乱码，为什么呢，以汉字‘丁’为例，其utf8编码为0xE4B881，这三个字节会直接拼接到数据包中，即其在实际发送时只占三字节，上图右边是逐字节转为ascii字符显示的，因此会显示为三个乱码字符。

4、由上可见，multipart/form-data将表单中的每个input转为了一个由boundary分割的小格式，没有转码，直接将utf8字节拼接到请求体中，在本地有多少字节实际就发送多少字节，极大提高了效率，适合传输长字节。



### axios每次发送请求会有两次，多一次Request Method: OPTIONS是怎么回事？

其实跨域分为 `简单跨域请求`和`复杂跨域请求`
**简单跨域**请求是**不会**发送`options`请求的 
**复杂跨域**请求**会**发送一个预检请求`options`

如果不想发送`option`请求可以改为简单请求 比如你的`Content-Type`可能是`application/json`格式 将其改为`application/x-www-form-urlencoded`

**1.简单跨域满足的条件**

1.请求方式是以下三种之一：

> HEAD
>
> GET
>
> POST

2.HTTP的头信息不超出以下几种字段

> Accept
>
> Accept-Language
>
> Content-Language
>
> Last-Event-ID
>
> Content-Type

但是Content-Type的值，只限于三个值：

> application/x-www-form-urlencoded、multipart/form-data、text/plain

**2.复杂跨域满足的条件**

1.请求方法不是GET/HEAD/POST

2.post请求的Content-Type并非application/x-www-form-urlencoded, multipart/form-data, 或text/plain

3.请求设置了自定义的header字段

在header中自定义了字段就会触发options预检请求

```
// 请求拦截器
service.interceptors.request.use(
 config => \\{
 if (store.getters.token) \\{
 config.headers['Content-MD5'] = 'MD5'
 config.headers['authToken'] = getToken()
 config.headers['accessTokenRetireTime'] = getTokenTime()
 \\}

 return config
 \\},
 error => \\{
 console.log(error) // for debug
 return Promise.reject(error)
 \\}
)

```

**3.解决方案**

1.可以通过跟后端协调，将所有options放行，此时便能通过post/get请求访问到数据。

2.引入qs模块处理数据

qs.parse()将URL解析成对象的形式

qs.stringify()将对象 序列化成URL的形式，以&进行拼接

1.安装qs

> npm install qs

2.在main.js引入qs

> import qs from 'qs';
>
> Vue.prototype.$qs = qs;

3.vue实例组件里都可以直接用this.$qs.stringify(要处理的数据)，进行数据转换

个人倾向第一种方法，如果用第二种方法对前后端来说比较繁琐。

**补充知识：****vue当中axios调取后台数据 以及设置自定义请求头**

从vue2.0开始vue-resource就不再维护了，尤大大开始推荐使用 axios。 具体详细教程可在官网查阅，这篇文章主要说明一些简单的问题。

**第一步：**安装axios

> $ npm install axios

**第二步：**在 main.js中引入axios

![img](https://img.jbzj.com/file_images/article/202008/20200814142742.jpg)

**第三步：**设置我们自定义的 头请求；

header也可以在我们具体的请求中添加 header参数，我们这里是在main.js中添加公众的。

> axios.defaults.timeout = 5000; 

//请求超时的时间设定

> axios.defaults.headers.post['Content-Type'] = 'application/json'; 

//axios默认的请求方式,可以自己设置

> axios.defaults.baseURL = 'http://localhost:8008'; 

//axios默认的请求地址,开发时可以实际的接口地址来设置该值,去请求别人的接口(前提是后台已经帮你解决了接口的跨域问题,如果没有,请看下文,我们自己可以解决开发跨域的问题)

> axios.defaults.headers.common["token"] = "aaaaaaaaaaa";



### 面对多个baseurl 如何封装请求方法 多个服务器请求地址

config.js

```
export const baseURL= \\{
base1: 'http://192.168.1.1:1111',
base2: 'http://192.168.2.1:2222',
base3: 'http://192.168.3.1:3333',
base4: 'http://192.168.4.1:4444',
base5: 'http://192.168.5.1:5555',
\\}
```

service.js

```
import \\{ baseURL\\} from '../axios/config.js'

const base1= baseURL.base1;
const base2= baseURL.base2;

export const getToken = (params) =>\\{
return request(\\{
	url:base1+'/xxx/getToken.do',
	method:'get',
	params:params
	\\})
\\}
```



### axios 30秒后提示超时

在使用 Axios 发起请求时，你可以通过设置 `timeout` 选项来定义请求的超时时间。如果你想要在请求发起30秒后提示超时，可以将 `timeout` 设置为 30000 毫秒（因为时间单位是毫秒）。下面是一个简单的例子：

```javascript
axios.get('你的请求URL', \\{
  timeout: 30000, // 30秒超时设置
\\})
.then(function (response) \\{
  // 请求成功后的处理逻辑
  console.log(response);
\\})
.catch(function (error) \\{
  if (error.code === 'ECONNABORTED' && error.message.indexOf('timeout') !== -1) \\{
    // 超时错误处理
    console.log('请求超时，请稍后再试');
  \\} else \\{
    // 其他错误处理
    console.error(error);
  \\}
\\});
```

这段代码首先设置了请求的超时时间为30秒。如果请求在这个时间内没有完成（包括完成连接、响应等所有过程），Axios 将会抛出一个超时错误。我们在 `.catch()` 方法中捕捉这个错误，并且检查错误是否由超时引起。如果是的话，则输出相应的超时提示信息。

请注意，你需要根据实际情况替换 `'你的请求URL'` 为你实际要请求的 URL。此外，对于不同的环境和需求，你可能需要调整错误处理逻辑。



### ECONNABORTED是什么意思，来自于哪里

```js
import axios from 'axios'// 添加拦截器
function addInterceptors() \\{
  // 添加响应拦截器
  httpServe.interceptors.response.use(
    function (response) \\{\\},
    (error) => \\{
      if (error.code === 'ECONNABORTED') \\{
        showFrontToast('请求超时，请稍后重试！')
      \\}
      return Promise.reject(error)
    \\}
\\}
```

`ECONNABORTED` 是一个网络请求相关的错误码，它表示**网络连接被意外中止**。这个错误通常来源于底层网络库（如 Node.js 的 `http` 模块或浏览器端的 `XMLHttpRequest`），在以下场景中可能被触发：

---

#### 常见场景
1. **请求超时**  
   当客户端（如 axios）设置了 `timeout` 参数，且请求在指定时间内未收到响应，连接会被主动中止，触发此错误。

2. **手动取消请求**  
   如果使用 axios 的 `CancelToken` 或 `AbortController` 主动取消请求，也可能导致此错误（但通常会有更明确的取消标识）。

3. **网络不稳定**  
   客户端和服务端之间的网络连接意外中断（如用户断网、代理服务器故障等）。

---

#### 在 axios 中的表现
在 axios 的拦截器中，可以通过 `error.code` 或 `error.message` 识别此错误：
```javascript
axios.interceptors.response.use(
  response => response,
  error => \\{
    if (error.code === 'ECONNABORTED') \\{
      console.log('请求被中止！', error.message);
    \\}
    return Promise.reject(error);
  \\}
);
```

---

#### 解决方案
1. **调整超时时间**
   适当增大 axios 的 `timeout` 配置：
   
   ```javascript
   axios.create(\\{ timeout: 10000 \\}); // 10 秒超时
```
   
2. **重试机制**
   对超时请求添加自动重试逻辑（注意幂等性）：
   
   ```javascript
   let retryCount = 0;
   axios.interceptors.response.use(null, async (error) => \\{
     if (error.code === 'ECONNABORTED' && retryCount < 3) \\{
       retryCount++;
       return axios.request(error.config);
     \\}
     return Promise.reject(error);
   \\});
```
   
3. **优化服务器性能**
   检查服务端响应速度，避免因处理时间过长导致超时。

4. **网络监控**
   检测用户网络状态，提示网络不稳定：
   
   ```javascript
   window.addEventListener('offline', () => \\{
     showToast('网络已断开，请检查连接！');
   \\});
   ```

---

#### 其他常见网络错误码
| 错误码                      | 含义             |
| --------------------------- | ---------------- |
| `ECONNRESET`                | 连接被对端重置   |
| `ENOTFOUND`                 | DNS 解析失败     |
| `ERR_NETWORK`               | 浏览器端网络错误 |
| `ERR_INTERNET_DISCONNECTED` | 网络完全断开     |

建议在拦截器中统一处理这些错误，提升用户体验。