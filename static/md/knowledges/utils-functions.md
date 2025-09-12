---
title: utils函数
date: 2024-03-05 21:02:08
categories: 
- 前端知识
tags:
- vue
- 函数
---

# vue3

### 通用步骤

@/utils/index.js中写入

在页面中使用

```
import \\{ xxx \\} from '@/utils/index'
import \\{ getAssets, truncate \\} from '@/utils/index'
```



### vue3的vite中图片的动态加载

```javascript
// 获取assets静态资源路径
export const getAssets = (url) => \\{
  return new URL(`../assets/images/$\\{url\\}`, import.meta.url).href
\\}
```

注意：这里只能通过 …/…/ 这种方式去获取路径，无法通过@/assets

页面中

```
import \\{ getAssets \\} from '@/utils/index'

<img :src="getAssets(`home/cover$\\{activeIndex\\}@2x.png`)" alt="">
```



### 截取指定长度字符串

```
// 截取指定长度字符串
export const truncate = (value, length) => \\{
  return value.length > length ? `$\\{value.substring(0, length)\\}...` : value
\\}
```

页面中

```
import \\{ truncate \\} from '@/utils/index'

<div class="content-title">\\\{\\\{ truncate(item.name,12)\\\}\\\} }}</div>
```







# vue2

### 工具函数挂载到Vue.prototype

在main.js中

```
import utils from '@/utils';

Vue.prototype.getLabelByKey = utils.getLabelByKey
```

在组件中可以直接使用

```
\\\{\\\{getLabelByKey(item.state, confirmationMethodEnum\\\}\\\})}}
```



### 根据key和枚举数组返回label

你可以通过遍历`Enum`数组来找到与给定`key`匹配的对象的`label`。以下是一个简单的JavaScript方法来实现这个功能：

```javascript
/**
 * 根据key和枚举数组返回label
 */
utils.getLabelByKey = (key, enumArray) => \\{
	for (let i = 0; i < enumArray.length; i++) \\{
		if (enumArray[i].key === key) \\{
			return enumArray[i].label
		\\}
	\\}
	// 如果没有找到匹配的key，返回空字符串 
	return ''
\\}
  
// 使用示例  
const Enum = [  
  \\{  
    key: 1,  
    label: '无需确认'  
  \\},  
  \\{  
    key: 2,  
    label: '手动确认'  
  \\}  
];  
  
const keyToFind = 1;  
const label = getLabelByKey(keyToFind, Enum);  
console.log(label); // 输出: 无需确认
```

在这个例子中，`getLabelByKey`函数接受两个参数：`key`和`enumArray`。它遍历`enumArray`数组，并检查每个对象的`key`属性是否匹配给定的`key`。如果找到了匹配的`key`，它就返回对应的`label`。如果遍历完整个数组都没有找到匹配的`key`，函数返回空字符串 。



### iOS设备检测

为了检测用户是否使用iOS设备，并将结果赋值给一个名为`isIOS`的变量，你可以使用JavaScript来检查用户的浏览器User-Agent字符串。以下是一个简单的例子：

```javascript
const isIOS = /iPad|iPhone|iPod/i.test(navigator.userAgent) && !window.MSStream
```

这段代码做了以下几件事：

- 它创建了一个不区分大小写的正则表达式来匹配用户代理字符串User-Agent中的`iPad`, `iPhone`, 或 `iPod`。
- 使用`navigator.userAgent`获取当前浏览器的User-Agent字符串。
- 检查`window.MSStream`以排除某些情况下Windows系统的误判（如Edge浏览器在旧版本中可能会包含"iPhone"字样）。

需要注意的是，依赖User-Agent进行检测并不是最可靠的方法，因为User-Agent字符串可以被用户修改，而且一些浏览器可能会模拟其他浏览器的User-Agent。此外，随着技术的发展，苹果可能发布新的iOS设备或更新现有的命名方案，这可能导致上述检测方法在未来失效。因此，如果你需要更可靠的检测方式，你可能需要考虑使用特征检测或其他更加健壮的方法。



### 时间戳转换成字符串格式

```
// 时间戳转换成字符串格式
  formatTime(value) \\{
    if (value) \\{
      // let date = new Date(value * 1000) // 时间戳为秒：10位数
      let date = new Date(value)    // 时间戳为毫秒：13位数
      let year = date.getFullYear()
      let month = date.getMonth() + 1 < 10 ? `0$\\{date.getMonth() + 1\\}` : date.getMonth() + 1
      let day = date.getDate() < 10 ? `0$\\{date.getDate()\\}` : date.getDate()
      let hour = date.getHours() < 10 ? `0$\\{date.getHours()\\}` : date.getHours()
      let minute = date.getMinutes() < 10 ? `0$\\{date.getMinutes()\\}` : date.getMinutes()
      let second = date.getSeconds() < 10 ? `0$\\{date.getSeconds()\\}` : date.getSeconds()
      return `$\\{year\\}-$\\{month\\}-$\\{day\\} $\\{hour\\}:$\\{minute\\}:$\\{second\\}`
    \\} else \\{
      return ''
    \\}
  \\},
```



### 日期格式转换字符串格式

```
// 日期格式转换字符串格式
const formatDate = value => \\{
  let Year = value.getFullYear();
  let Month = value.getMonth() + 1;
  let Day = value.getDate();
  let Hours = value.getHours();
  let Minutes = value.getMinutes();
  let Seconds = value.getSeconds();
  let MonthVal = Month >= 10 ? Month : "0" + Month;
  let DayVal = Day >= 10 ? Day : "0" + Day;
  let HoursVal = Hours >= 10 ? Hours : "0" + Hours;
  let MinutesVal = Minutes >= 10 ? Minutes : "0" + Minutes;
  let SecondsVal = Seconds >= 10 ? Seconds : "0" + Seconds;
  return `$\\{Year\\}-$\\{MonthVal\\}-$\\{DayVal\\} $\\{HoursVal\\}:$\\{MinutesVal\\}:$\\{SecondsVal\\}`;
\\}

// 日期格式转换字符串格式（年月日）
const formatDate = value => \\{
  let Year = value.getFullYear();
  let Month = value.getMonth() + 1;
  let Day = value.getDate();
  let MonthVal = Month >= 10 ? Month : "0" + Month;
  let DayVal = Day >= 10 ? Day : "0" + Day;
  return `$\\{Year\\}-$\\{MonthVal\\}-$\\{DayVal\\}`;
\\}
```



### 字符串yyyy-MM-dd HH:mm:ss转标准日期格式

```
// 字符串yyyy-MM-dd HH:mm:ss转标准日期格式
const getDateFromTimeString = (str) => \\{
  let reg = /^(\d+)-(\d+)-(\d+) (\d+):(\d+):(\d+)/;
  let s = str.match(reg);
  let result = "";
  if (s) \\{
    result = new Date(s[1], s[2] - 1, s[3], s[4], s[5], s[6]);
  \\}
  return result;
\\}
```

调用方式：

```
			const use_end = Utils.getDateFromTimeString(this.detail.use_end)
            const time = new Date()
            let day = (time - use_end) / (1000 * 60 * 60 * 24)
            console.log(this.detail, use_end, time, day)
            // 如果超过一天
            if (day > 1) \\{
                this.isShow = false
            \\}
```



### 字符串yyyy-MM-dd转标准日期格式

```
// 字符串yyyy-MM-dd转标准日期格式
const getDateFromString = (str) => \\{
  let reg = /^(\d+)-(\d+)-(\d+)/;
  let s = str.match(reg);
  let result = "";
  if (s) \\{
    result = new Date(s[1], s[2] - 1, s[3]);
  \\}
  return result;
\\}
```

调用方式：

```
					this.dateEnd = '2025-01-09'
					const date = Utils.getDateFromString(res.date)
                    const dateEnd = Utils.getDateFromString(this.dateEnd)
                    console.log(date, dateEnd)
                    if (date > dateEnd) \\{
                        uni.showToast(\\{
                            title: `日期不能超过$\\{this.dateEnd\\}`,
                            icon: 'none',
                            duration: 2000
                        \\})
                        return
                    \\}
```



### 时间不同显示

格式为"2024-08-23 15:57:27"，今天显示15:57，本年显示08-23 15:57，往年显示2023-08-23

```
// 格式化时间字符串，今天今年往年不同格式
const formatTimeStr = (timeStr) => \\{
  // timeStr = '2023-09-03 15:57:27'
  const itemTime = new Date(timeStr)
  const now = new Date()

  if (isSameDay(itemTime, now)) \\{
    // 今天
    return itemTime.toLocaleTimeString([], \\{
      hour: '2-digit',
      minute: '2-digit',
    \\})
  \\} else if (now.getFullYear() === itemTime.getFullYear()) \\{
    // 今年
    return `$\\{
      itemTime.getMonth() + 1
    \\}-$\\{itemTime.getDate()\\} $\\{itemTime.toLocaleTimeString([], \\{
      hour: '2-digit',
      minute: '2-digit',
    \\})\\}`
  \\} else \\{
    // 往年
    return itemTime.toISOString().split('T')[0]
  \\}
\\}
// 检查时间是否是今天
const isToday = (timeStr) => \\{
  return isSameDay(new Date(timeStr), new Date())
\\}
// 比较两个日期是否是同一天
const isSameDay = (date1, date2) => \\{
  return (
    date1.getFullYear() === date2.getFullYear() &&
    date1.getMonth() === date2.getMonth() &&
    date1.getDate() === date2.getDate()
  )
\\}
```

低版本IOS系统日期处理问题：

2024-10-11 （高版本可识别，低版本无法识别）

处理为2024/10/11 （高低版本均可识别）

```
export const getDateByDateStr = (dateStr) => \\{
  // 确保兼容性：将日期字符串中的所有短横线-替换为斜杠/
  dateStr = dateStr.replace(/\-/g, '/')
  return new Date(dateStr)
\\}
// 格式化时间字符串，今天今年往年不同格式
export const formatTimeStr = (timeStr) => \\{
  // timeStr = '2024-11-18 10:10:10'
  // timeStr = '2024-09-09 09:09:09'
  // timeStr = '2023-11-15 10:10:10'
  if (!timeStr || typeof timeStr !== 'string') \\{
    throw new Error('timeStr不能为空且为字符串类型')
  \\}
  const date = getDateByDateStr(timeStr)
  if (isNaN(date.getTime())) \\{
    throw new Error('日期字符串格式无效')
  \\}
  const year = date.getFullYear()
  const month = (date.getMonth() + 1).toString().padStart(2, '0')
  const day = date.getDate().toString().padStart(2, '0')
  const hour = date.getHours().toString().padStart(2, '0')
  const minute = date.getMinutes().toString().padStart(2, '0')
  const currentDate = new Date()
  if (isSameDay(date, currentDate)) \\{
    // 今天
    return `$\\{hour\\}:$\\{minute\\}`
  \\} else if (currentDate.getFullYear() === year) \\{
    // 今年
    return `$\\{month\\}-$\\{day\\} $\\{hour\\}:$\\{minute\\}`
  \\} else \\{
    // 往年
    return `$\\{year\\}-$\\{month\\}-$\\{day\\}`
  \\}
\\}

// 检查时间是否是今天
export const isToday = (timeStr) => \\{
  // timeStr = '2024-11-18 10:10:10'
  const tempDateObj = getDateByDateStr(timeStr)
  return isSameDay(tempDateObj, new Date())
\\}

// 比较两个日期是否是同一天
const isSameDay = (date1, date2) => \\{
  return (
    date1.getFullYear() === date2.getFullYear() &&
    date1.getMonth() === date2.getMonth() &&
    date1.getDate() === date2.getDate()
  )
\\}
```



### 获取上个月的日期范围

```
		getPrev() \\{
            // 获取当前日期
            let currentDate = new Date()

            // 设置日期为1号
            currentDate.setDate(1)

            // 减去一个月
            currentDate.setMonth(currentDate.getMonth() - 1)

            // 获取上个月的年份和月份
            let previousYear = currentDate.getFullYear()
            let previousMonth = currentDate.getMonth() + 1 // 月份从0开始，需要加1

            // 获取上个月的最后一天
            let lastDayOfPreviousMonth = new Date(
                previousYear,
                previousMonth,
                0
            ).getDate()

            // 构造上个月的开始和结束日期
            let startDate = `$\\{previousYear\\}-$\\{previousMonth
                .toString()
                .padStart(2, '0')\\}-01`
            let endDate = `$\\{previousYear\\}-$\\{previousMonth
                .toString()
                .padStart(2, '0')\\}-$\\{lastDayOfPreviousMonth
                .toString()
                .padStart(2, '0')\\}`

            console.log(startDate + '~' + endDate)
            this.searchData.use_end = `$\\{startDate\\} 00:00:00~$\\{endDate\\} 23:59:59`
            this.use_end = [`$\\{startDate\\} 00:00:00`, `$\\{endDate\\} 23:59:59`]
        \\}
```



### 节流

```
// 节流
const throttle = (fn, wait) => \\{
  let delay = wait || 500 // 不传默认500毫秒
  let timer = +new Date()  // 声明初始时间
  return function (...arg) \\{ // 获取参数
    let newTimer = +new Date()  // 获取触发事件的时间
    console.log(timer, newTimer)
    if (newTimer - timer >= delay) \\{  // 时间判断,是否满足条件
      fn.apply(this, arg)  // 调用需要执行的函数,修改this值,并且传入参数
      timer = +new Date() // 重置初始时间
    \\}
  \\}
\\}
```

调用方式：

```
		// 点击提交按钮
        onClick: Utils.throttle(function () \\{
            console.log("点击事件随机值" + Math.random());
            this.submit();
        \\}, 2000),

        // 提交数据
        async submit() \\{\\}
```



### 手机号码校验

```
isMobile:  function(value) \\{
	return /^1[3|4|5|6|7|8|9][0-9]\d\\{8\\}$/.test(value); 
\\}
```

调用方式：

```
if(!this.isMobile(aac067))\\{
    alert("手机号码格式错误!")
    return;
\\}
```



### 邮箱校验

```
// 邮箱校验正则
utils.isEmail = (email) => \\{
  let emailRegExp = /^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/
  return emailRegExp.test(email)
\\}
```



### 将url转换成对象

#### 1.有域名

```
		// 将url转换成对象
        urlToObject(url) \\{
            if (/\?/.test(url)) \\{
                let urlString = url.substring(url.indexOf('?') + 1)
                let urlArray = urlString.split('&'),
                    obj = \\{\\}
                for (let i = 0; i < urlArray.length; i++) \\{
                    let item = urlArray[i].split('=')
                    obj[item[0]] = item[1]
                \\}
                return obj
            \\}
        \\},
```

调用方式：

```
let testUrl = 'http://tools.jb51.net/index.php?key0=0&key1=1&key2=2'
console.log(this.urlToObject(testUrl))
```

#### 2.没有域名

```
// 将url转换成对象
const urlToObject = (url) => \\{
  let urlArray = url.split('&'),
    obj = \\{\\}
  for (let i = 0; i < urlArray.length; i++) \\{
    let item = urlArray[i].split('=')
    obj[item[0]] = item[1]
  \\}
  return obj
\\}
```

调用方式：

```
let scene = 'mch_id=WgrpwNplS8rL&task_no=DUCeGliAJ'
let obj = Utils.urlToObject(scene)
console.log(obj)
```

#### 其他方式

```
		// 截取url中的code方法
		getUrlCode() \\{
            var url = location.search
            var theRequest = new Object()
            if (url.indexOf('?') != -1) \\{
                var str = url.substr(1)
                var strs = str.split('&')
                for (var i = 0; i < strs.length; i++) \\{
                    theRequest[strs[i].split('=')[0]] = strs[i].split('=')[1]
                \\}
            \\}
            return theRequest
        \\},

// sub_user/userInfo/AccountInfo?is_show=1&is_success=0
let is_show = this.getUrlCode().is_show // 截取
let is_success = this.getUrlCode().is_success // 截取
console.log(is_show, is_success) // '1','0'
```



### 格式化带间隔的手机号

```
// 格式化带间隔的手机号
const phoneFormat = (val) => \\{
  if (typeof (val) === 'string') \\{
    const head = val.slice(0, 3),
      middle = val.slice(3, 7),
      last = val.slice(7, 11);
    return `$\\{head\\} $\\{middle\\} $\\{last\\}`;
  \\}
\\}
```

过滤器使用

```
// 全局过滤器添加
import Vue from "vue"

// 格式化带间隔的手机号
Vue.filter("phoneFormat", (val) => \\{
    if (typeof (val) === 'string') \\{
        const head = val.slice(0, 3),
            middle = val.slice(3, 7),
            last = val.slice(7, 11);
        return `$\\{head\\} $\\{middle\\} $\\{last\\}`;
    \\}
\\})
```



### 字符串省略

```
// 字符串省略 strNum:字符串最大长度
Vue.filter("ellipsisStr", (val, strNum) => \\{
    if (typeof (val) === "string") \\{
        if (val.length > strNum) \\{
            const str = `$\\{val.substr(0, strNum - 1)\\}...`;
            return str;
        \\} else \\{
            return val;
        \\}
    \\}
\\})
```



### 判断是否是电话号码

```
function isPhone(tel) \\{
    var regex = /^1[34578]\d\\{9\\}$/;
    return regex.test(tel);
\\}
```



### 验证是否是邮箱

```
function isEmail(email) \\{
    var regex = /^([a-zA-Z0-9_\-])+@([a-zA-Z0-9_\-])+(\.[a-zA-Z0-9_\-])+$/;
    return regex.test(email);
\\}
```



### 验证是否是身份证

```
function isCardNo(number) \\{
    const regex = /(^\d\\{15\\}$)|(^\d\\{18\\}$)|(^\d\\{17\\}(\d|X|x)$)/;
    return regex.test(number);
\\}
```

```
function isCardNo(number) \\{
    const regex = /(^\d\\{15\\}$)|(^\d\\{17\\}([0-9]|X)$)/;
    return regex.test(number);
\\}
```



### 脱敏身份证号

```
// 脱敏身份证号
Vue.filter("encryptId", (val) => \\{
    if (val && typeof (val) === 'string') \\{
        return val.replace(/(.\\{9\\}).*(.\\{2\\})/, '$1********$2')
    \\} else \\{
        return '--'
    \\}
\\})
```



### 避免address中省市区重复

省份（province）：表示地址所在的省份。
城市（city）：表示地址所在的城市。
区县（district）：表示地址所在的区县。
详细地址（detail）：可能包括街道、小区、门牌号等更详细的地址信息。
address是上面几个字段拼接起来的，但detail有可能前面几个字包含省市区，请写一个js方法避免address中省市区重复，如果省市相同的话只显示省。
例如：detail为朝阳区体育公园，执行该方法后address显示北京市朝阳区体育公园

为了优化并避免在拼接`address`时出现省市区重复的问题，我们可以使用以下JavaScript方法。这个方法会检查`detail`字段是否以`province`和`city`（可能还包括`district`）开头，并据此决定是否需要重复添加这些部分到`address`中。

```javascript
function generateAddress(province, city, district, detail) \\{  
  // 初始化address，从province和city开始  
  let address = province;  
  if (city && city !== province) \\{ // 如果city和province不同，则添加city  
    address += city;  
  \\}  
    
  // 如果detail以district开头，则只添加district；否则，添加district和detail  
  if (detail.startsWith(district)) \\{  
    address += detail;  
  \\} else \\{  
    address += `$\\{district\\}$\\{detail\\}`;
  \\}  
    
  return address.trim(); // 移除可能的首尾空格  
\\}  
  
// 示例用法  
const province = '北京';  
const city = '北京';  
const district = '朝阳区';  
const detail = '体育公园';  
  
const address = generateAddress(province, city, district, detail);  
console.log(address); // 输出：北京市朝阳区体育公园
```

在这个方法中，我们首先根据`province`和`city`（如果它们不同）构建`address`的基础部分。然后，我们检查`detail`是否以`district`开头。如果是，则我们直接将`detail`添加到`address`中，因为这意味着`detail`已经包含了完整的区县级信息。如果不是，我们则添加`district`和`detail`到`address`中，确保所有的信息都被包含。

最后，我们使用`trim()`方法确保`address`字符串没有不必要的首尾空格。

这个方法简洁明了，避免了复杂的正则表达式和多次字符串拼接，从而提高了性能。



### 将分钟转换为小时和分钟

```
// 将分钟转换为小时和分钟
Vue.filter("minutesToHours", (val) => \\{
    if (val <= 60) \\{
        return `$\\{val\\}分钟`
    \\} else \\{
        const hours = Math.floor(val / 60);
        const minutes = val \\% 60;
        if (minutes === 0) \\{
            return `$\\{hours\\}小时`
        \\} else \\{
            return `$\\{hours\\}小时$\\{minutes\\}分钟`
        \\}
    \\}
\\})
```



### 将数字转换为中文金额大写

```
function amountToChinese(num) \\{
  const digits = '零壹贰叁肆伍陆柒捌玖';
  const units = ['元', '拾', '佰', '仟', '万', '拾', '佰', '仟', '亿', '拾', '佰', '仟'];
  const decimals = ['角', '分'];

  let integerPart = Math.floor(num); // 整数部分
  let decimalPart = Math.round((num - integerPart) * 100); // 小数部分

  let chineseStr = '';

  const integerStr = integerPart.toString();

  if (integerStr.length > 12) \\{
    throw new Error('超出计算范围');
  \\}

  let zeroCount = 0; // 连续为零的计数
  for (let i = 0; i < integerStr.length; i++) \\{
    const digit = integerStr[i];
    const unit = units[integerStr.length - i - 1];
    if (digit === '0') \\{
      zeroCount++;
    \\} else \\{
      if (zeroCount > 0) \\{
        chineseStr += digits[0];
      \\}
      zeroCount = 0;

      chineseStr += digits[parseInt(digit)] + unit;
    \\}
  \\}

  if (chineseStr[chineseStr.length - 1] !== units[0]) \\{
    chineseStr += units[0];
  \\}

  if (decimalPart > 0) \\{
    const decimalStr = decimalPart.toString().padStart(2, '0');
    for (let i = 0; i < decimalStr.length; i++) \\{
      const digit = decimalStr[i];
      const unit = decimals[i];

      if (digit !== '0') \\{
        chineseStr += digits[parseInt(digit)] + unit;
      \\}
    \\}
  \\} else \\{
    chineseStr += '整';
  \\}

  return chineseStr;
\\}
```

调用方式：

```
// js输入8888.88输出捌仟捌佰捌拾捌元捌角捌分
const num = 8888.88;
const chineseAmount = amountToChinese(num);
console.log(chineseAmount); // 输出：捌仟捌佰捌拾捌元捌角捌分
```

注意：以上代码中，将数字转换为金额大写时，小数部分会进行四舍五入。 







### 选择单张图片

```
// 选择单张图片
const chooseImage = () => \\{
  /* 返回一个promise实例化对象 */
  return new Promise((resolve, reject) => \\{
    uni.chooseImage(\\{
      count: 1,
      sizeType: ["compressed"],
      sourceType: ["album", "camera"],
      success: (res) => \\{
        console.log(res, store.state.login.envType)
        let filePath, dealName
        // 钉钉且不是开发者工具中（预览、真机调试、体验版、正式版）
        if (store.state.login.envType === 3 && !dd.isIDE) \\{
          // 可以作为img标签的src属性显示图片
          filePath = res.files[0].path.slice(0, -5) + res.files[0].fileType
          dealName = filePath.replace("https://resource/", "").toLowerCase();
        \\} else if (store.state.login.envType === 4) \\{
          // 网页版
          filePath = res.tempFilePaths[0]
          dealName = res.tempFiles[0].name;
        \\} else \\{
          // 微信/企微/钉钉开发者工具
          filePath = res.tempFilePaths[0]
          dealName = filePath.replace("http://tmp/", "").toLowerCase();
        \\}
        console.log(filePath, dealName)
        resolve([filePath, dealName])
      \\},
      fail: (err) => \\{
        console.log(err)
        uni.showToast(\\{
          title: '图片获取失败，请重新选择',
          icon: 'none'
        \\})
        reject(err)
      \\}
    \\})
  \\})
\\}
```



### 选择多张图片

```
// 选择多张图片
const chooseImages = (count) => \\{
  /* 返回一个promise实例化对象 */
  return new Promise((resolve, reject) => \\{
    uni.chooseImage(\\{
      count,
      sourceType: ["album", "camera"],
      success: (res) => \\{
        console.log(res, store.state.login.envType)
        let files = []
        // 钉钉且不是开发者工具中（预览、真机调试、体验版、正式版）
        if (store.state.login.envType === 3 && !dd.isIDE) \\{
          res.files.forEach(item => \\{
            let path = item.path.slice(0, -5) + item.fileType
            let name = path.replace("https://resource/", "").toLowerCase();
            files.push(\\{ path, name \\})
          \\});
        \\} else if (store.state.login.envType === 4) \\{
          // 网页版
          res.tempFiles.forEach(item => \\{
            files.push(\\{ path: item.path, name: item.name \\})
          \\});
        \\} else \\{
          // 微信/企微/钉钉开发者工具
          res.tempFilePaths.forEach(item => \\{
            let name = item.replace("http://tmp/", "").toLowerCase()
            files.push(\\{ path: item, name \\})
          \\});
        \\}
        console.log(files)
        resolve(files)
      \\},
      fail: (err) => \\{
        reject(err)
      \\}
    \\})
  \\})
\\}
```



### chooseVideo选择视频

```
// 选择视频
const chooseVideo = () => \\{
  /* 返回一个promise实例化对象 */
  return new Promise((resolve, reject) => \\{
    uni.chooseVideo(\\{
      count: 1,
      camera: 'front', // 默认打开前摄像头
      success: (res) => \\{
        console.log(res, store.state.login.envType)
        // 检查视频大小
        if (res.size > 50000000) \\{
          uni.showToast(\\{
            title: '请上传50M以内的视频',
            icon: 'none'
          \\})
          return
        \\}
        let filePath = res.tempFilePath, dealName
        // 钉钉且不是开发者工具中（预览、真机调试、体验版、正式版）
        if (store.state.login.envType === 3 && !dd.isIDE) \\{

        \\} else if (store.state.login.envType === 4) \\{
          // 网页版
          dealName = res.name;
        \\} else \\{
          // 微信/企微/钉钉开发者工具
          dealName = filePath.replace("wxfile://tmp_", "").toLowerCase();
        \\}
        console.log(filePath, dealName)
        resolve([filePath, dealName])
      \\},
      fail: (err) => \\{
        console.log(err)
        uni.showToast(\\{
          title: '视频获取失败，请重新选择',
          icon: 'none'
        \\})
        reject(err)
      \\}
    \\})
  \\})
\\}
```



### chooseMedia选择视频

```js
// 选择视频
const chooseVideo = () => \\{
  /* 返回一个promise实例化对象 */
  return new Promise((resolve, reject) => \\{
    const envType = store.state.login.envType
    const count = 1
    const camera = 'front' // 默认打开前摄像头
    console.log(envType);
    if (envType === 1) \\{
      // 微信
      uni.chooseMedia(\\{
        count,
        camera,
        sourceType: ['camera'],
        mediaType: ['video'],
        success: (res) => \\{
          console.log(res)
          handleSuccess(res.tempFiles[0])
        \\},
        fail: (err) => \\{
          handleFail(err)
        \\}
      \\})
    \\} else \\{
      // 其他环境
      uni.chooseVideo(\\{
        count,
        camera,
        success: (res) => \\{
          console.log(res)
          handleSuccess(res.tempFile, res.tempFilePath)
        \\},
        fail: (err) => \\{
          handleFail(err)
        \\}
      \\})
    \\}
    // 成功统一处理
    function handleSuccess(file, tempFilePath) \\{
      console.log(file)
      // 检查视频大小
      if (file.size > 50000000) \\{
        uni.showToast(\\{
          title: '请上传50M以内的视频',
          icon: 'none'
        \\})
        return
      \\}
      let filePath, dealName
      // 钉钉且不是开发者工具中（预览、真机调试、体验版、正式版）
      if (envType === 3 && !dd.isIDE) \\{

      \\} else if (envType === 4) \\{
        // 网页版
        filePath = tempFilePath
        dealName = file.name;
      \\} else \\{
        // 微信/企微/钉钉开发者工具
        filePath = file.tempFilePath
        dealName = filePath.replace("wxfile://tmp_", "").toLowerCase();
      \\}
      console.log(filePath, dealName)
      resolve([filePath, dealName])
    \\}
    // 失败统一处理
    function handleFail(err) \\{
      console.log(err)
      uni.showToast(\\{
        title: '视频获取失败，请重新选择',
        icon: 'none'
      \\})
      reject(err)
    \\}
  \\})
\\}
```

小程序开发者工具报错：chooseVideo:fail MEDIA_ELEMENT_ERROR: Format error，真机正常。



### 选择文件

```
// 选择文件
const chooseFile = () => \\{
  /* 返回一个promise实例化对象 */
  return new Promise((resolve, reject) => \\{
    const envType = store.state.login.envType
    const count = 30
    // 根据文件拓展名过滤(前面不能加.否则ios找不到文件)
    const extension = ['.png', '.jpg', '.jpeg', '.doc', '.docx', '.xls', '.xlsx', '.pdf', '.zip', '.rar']
    console.log(envType);
    if (envType === 1) \\{
      // 微信
      wx.chooseMessageFile(\\{
        count,
        extension,
        success: (res) => \\{
          handleSuccess(res)
        \\},
        fail: (err) => \\{
          handleFail(err)
        \\}
      \\})
    \\} else \\{
      // 其他环境
      uni.chooseFile(\\{
        count,
        extension,
        success: (res) => \\{
          handleSuccess(res)
        \\},
        fail: (err) => \\{
          handleFail(err)
        \\}
      \\})
    \\}
    // 成功统一处理
    function handleSuccess(res) \\{
      console.log(res)
      const file = res.tempFiles[0]
      // 检查文件大小
      if (file.size > 52430000) \\{
        uni.showToast(\\{
          title: '文件大小不能超过50M',
          icon: 'none'
        \\})
        return
      \\}
      console.log(file.path, file.name, file.size)
      resolve([file.path, file.name, file.size])
    \\}
    // 失败统一处理
    function handleFail(err) \\{
      console.log(err)
      uni.showToast(\\{
        title: '文件获取失败，请重新选择',
        icon: 'none'
      \\})
      reject(err)
    \\}
  \\})
\\}
```



### 上传文件到oss

```js
// 上传文件到oss
const uploadFile = (res, filePath) => \\{
  // 返回一个promise实例化对象
  return new Promise((resolve, reject) => \\{
    uni.uploadFile(\\{
      url: res.host,
      filePath,
      name: "file",
      // 钉钉多传两个参数
      fileType: "image",
      fileName: "file",
      formData: \\{
        type: 2,
        "x:source_name": res.source_name,
        key: res.path + res.name,
        OSSAccessKeyId: res.accessid,
        signature: res.signature,
        policy: res.policy,
        callback: res.callback
      \\},
      success(res) \\{
        console.log(res);
        resolve(JSON.parse(res.data))
      \\},
      fail(err) \\{
        console.log(err);
        reject(err)
      \\}
    \\});
  \\})
\\}
```







### 0 - n 的随机数

```javascript
    Math.floor(Math.random() * (n + 1));
```



### Max - Min 的随机数

```javascript
// 一、min ≤ r ≤ max
function RandomNumBoth(Min,Max)\\{
    var Range = Max - Min;
    var Rand = Math.random();
    var num = Min + Math.round(Rand * Range); //四舍五入
    return num;
\\}

// 二、min ≤ r < max
function RandomNum(Min, Max) \\{
    var Range = Max - Min;
    var Rand = Math.random();
    var num = Min + Math.floor(Rand * Range); //舍去
    return num;
\\}

// 三、min < r ≤ max
function RandomNum(Min, Max) \\{
    var Range = Max - Min;
    var Rand = Math.random();
    if(Math.round(Rand * Range)==0)\\{       
        return Min + 1;
    \\}
    var num = Min + Math.round(Rand * Range);
    return num;
\\}

// 四、min < r < max 
function RandomNum(Min, Max) \\{
    var Range = Max - Min;
    var Rand = Math.random();
    if( Math.round(Rand * Range)==0 )\\{
        return Min + 1;
    \\} else if(Math.round(Rand * Max)==Max)\\{
        index++;
        return Max - 1;
    \\}else\\{
        var num = Min + Math.round(Rand * Range) - 1;
        return num;
    \\}
 \\}
```



### 数组打乱排序

```javascript
function shuffle(array) \\{
    var _array = array.concat();
    for (var i = _array.length; i--; ) \\{
        // 产生 0 - i 的随机数
        var j = Math.floor(Math.random() * (i + 1));
        var temp = _array[i];
        _array[i] = _array[j];
        _array[j] = temp;
    \\}
    return _array;
\\}
```



### 深拷贝 - extend 的实现

```javascript
// 深拷贝有bug
var extend = (function() \\{
	var isObjFunc = function(name) \\{
			var toString = Object.prototype.toString
			return function() \\{
				return toString.call(arguments[0]) === '[object ' + name + ']'
			\\}
		\\}
	var isObject = isObjFunc('Object'),
		isArray = isObjFunc('Array'),
		isBoolean = isObjFunc('Boolean');
 	return function extend() \\{
			var index = 0,
				isDeep = false,
				obj, copy, destination, source, i
			if (isBoolean(arguments[0])) \\{
				index = 1;
				 isDeep = arguments[0]
			\\}
			for (i = arguments.length - 1; i > index; i--) \\{
				destination = arguments[i - 1]; source = arguments[i]
				if (isObject(source) || isArray(source)) \\{
					console.log(source);
					for (var property in source) \\{
						obj = source[property];
						if (isDeep && (isObject(obj) || isArray(obj))) \\{
							copy = isObject(obj) ? \\{\\} : [];
							var extended = extend(isDeep, copy, obj);
							 destination[property] = extended
						\\} else \\{
							destination[property] = source[property]
						\\}
					\\}
				\\} else \\{
					destination = source
				\\}
			\\}
			return destination
		\\}
\\})()


作者：文兴
链接：https://www.jianshu.com/p/04b1d88dabf2
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


// 可以
void function(global)\\{
    var extend,
        _extend,
        _isObject;

    _isObject = function(o)\\{
        return Object.prototype.toString.call(o) === '[object Object]';
    \\}

    _extend = function self(destination, source) \\{
        var property;
        for (property in destination) \\{
            if (destination.hasOwnProperty(property)) \\{

                // 若destination[property]和sourc[property]都是对象，则递归
                if (_isObject(destination[property]) && _isObject(source[property])) \\{
                    self(destination[property], source[property]);
                \\};

                // 若sourc[property]已存在，则跳过
                if (source.hasOwnProperty(property)) \\{
                    continue;
                \\} else \\{
                    source[property] = destination[property];
                \\}
            \\}
        \\}
    \\}

    extend = function()\\{
        var arr = arguments,
            result = \\{\\},
            i;

        if (!arr.length) return \\{\\};

        for (i = arr.length - 1; i >= 0; i--) \\{
            if (_isObject(arr[i])) \\{
                _extend(arr[i], result);
            \\};
        \\}

        arr[0] = result;
        return result;
    \\}

    global.extend = extend;
\\}(window)
```



### 深拷贝

```javascript
function cloneObject (obj) \\{
    var newObj = \\{\\}
    //如果不是引用类型，直接返回
    if ( obj instanceof Object ) \\{
      return obj
    \\}
    //如果是引用类型，遍历属性
    else\\{
         for (var attr in obj) \\{
         //如果某个属性还是引用类型，递归调用
          newObj[attr] = cloneObject(obj[attr])
        \\}
    \\}
   
    return newObj
  \\}
```



### 浅拷贝

```javascript
var extend = function(destination,source) \\{
    for(var property in source) \\{
        destination[property] = source[property]
    \\}
    return destination
\\}
```



### 移动端遮罩穿透

```javascript
/**
  * ModalHelper helpers resolve the modal scrolling issue on mobile devices
  * https://github.com/twbs/bootstrap/issues/15852
  * requires document.scrollingElement polyfill https://github.com/yangg/scrolling-element
  */
var ModalHelper = (function(bodyCls) \\{
  var scrollTop;
  return \\{
    afterOpen: function() \\{
      scrollTop = document.scrollingElement.scrollTop;
      document.body.classList.add(bodyCls);
      document.body.style.top = -scrollTop + 'px';
    \\},
    beforeClose: function() \\{
      document.body.classList.remove(bodyCls);
      // scrollTop lost after set position:fixed, restore it back.
      document.scrollingElement.scrollTop = scrollTop;
    \\}
  \\};
\\})('modal-open');
```



### vue中解析template用到的一些正则方法

```javascript
const ncname = '[a-zA-Z_][\\w\\-\\.]*'; 
const singleAttrIdentifier = /([^\s"'<>/=]+)/ 
const singleAttrAssign = /(?:=)/ 
const singleAttrValues = [ /"([^"]*)"+/.source, /'([^']*)'+/.source, /([^\s"'=<>`]+)/.source ] 
const attribute = new RegExp( '^\\s*' + singleAttrIdentifier.source + '(?:\\s*(' + singleAttrAssign.source + ')' + '\\s*(?:' + singleAttrValues.join('|') + '))?' ) 
const qnameCapture = '((?:' + ncname + '\\:)?' + ncname + ')' 
const startTagOpen = new RegExp('^<' + qnameCapture) 
const startTagClose = /^\s*(\/?)>/ 
const endTag = new RegExp('^<\\/' + qnameCapture + '[^>]*>') 
const defaultTagRE = /\\\{\\\{((?:.|\n)+?)\\\}\\\}/g 
const forAliasRE = /(.*?)\s+(?:in|of)\s+(.*)/

https://juejin.im
掘金 — 一个帮助开发者成长的社区
```



### 获取某月最后一天

```javascript
new Date( 2018, 03, 0 ) // 序列化后的结果  "2018-03-31 00:00:00"
new Date( 2018, 02, 0 ) // 序列化后的结果  "2018-02-28 00:00:00"  自动计算是否是闰月
```



### 获取当前月的下个月的第一天

```javascript
new Date(2018, 03, 1) // 序列化后的结果  "2018-04-01 00:00:00"
```



### 获取当前月的第一天

> 有用吗？ 每个月不都一号么。。 

```javascript
new Date('2018/03/1') // 序列化后的结果  "2018-03-01 00:00:00"
```



### 循环一段数字N次

```javascript
function repeat( str, num )\\{
	return new Array( num + 1 ).join( str );
\\}

// 举个栗子
repeat( '123', 3 )
"123123123"

// 将数组的间隔转换成字符串  
```



### 零宽断言

```javascript
// 测试 谷歌支持 火狐IE不支持  2018-03-14 之后的版本就不清楚啦
'My name is: Jerry . My age is: 12 . : :666 .'.match(/(?<=:\s?)([^\s:]+)/g)

// 输出 (3) ["Jerry", "12", "666"]
```



### 数组去重 并统计每项有多少重复值

```javascript
// 数组去重并统计每一项有几个
var arr = ["a","b","c","c","ab","d","ab","d","c"],
	newArr = [],
	obj = \\{\\};
for ( var i = 0, l = arr.length; i < l; i++ )\\{
    if( newArr.indexOf( arr ) <= -1 )\\{
        newArr.push( arr );
        obj[arr] = 1
    \\}else \\{
        obj[arr] = obj[arr] + 1;
    \\}    
\\}
```



### 加减乘除避免失真

```javascript
var work = \\{
	
	/**
	 * 解决加法失真
	 * @param \\{Number\\} 两个数字
	 * work.accAdd(1.1, 2)
	 * */
	accAdd: function (arg1, arg2) \\{
		var r1, r2, m;
		try \\{
			r1 = arg1.toString().split(".")[1].length
		\\} catch (e) \\{
			r1 = 0
		\\}
		try \\{
			r2 = arg2.toString().split(".")[1].length
		\\} catch (e) \\{
			r2 = 0
		\\}
		m = Math.pow(10, Math.max(r1, r2));
		//console.log(m)
		return (arg1 * m + arg2 * m) / m;
	\\},
	/**
	 * 解决减法失真
	 * @param \\{Number\\} 两个数字
	 * work.accSub(1.1, 2)
	 * */
	accSub: function (arg1, arg2) \\{
		var r1, r2, m, n;
		try \\{
			r1 = arg1.toString().split(".")[1].length
		\\} catch (e) \\{
			r1 = 0
		\\}
		try \\{
			r2 = arg2.toString().split(".")[1].length
		\\} catch (e) \\{
			r2 = 0
		\\}
		m = Math.pow(10, Math.max(r1, r2));
		//last modify by deeka
		//动态控制精度长度
		n = (r1 >= r2) ? r1 : r2;
		return ((arg1 * m - arg2 * m) / m).toFixed(n);
	\\},
	/**
	 * 解决乘法失真
	 * @param \\{Number\\} 两个数字
	 * work.accMul(1.1, 2)
	 * */
	accMul: function (arg1, arg2) \\{
		var m = 0,
			s1 = arg1.toString(),
			s2 = arg2.toString();
		try \\{
			m += s1.split(".")[1].length
		\\} catch (e) \\{\\}
		try \\{
			m += s2.split(".")[1].length
		\\} catch (e) \\{\\}
		return Number(s1.replace(".", "")) * Number(s2.replace(".", "")) / Math.pow(10, m)
	\\},
	/**
	 * 解决除法失真
	 * @param \\{Number\\} 两个数字
	 * work.accDiv(1.1, 2)
	 * */
	accDiv: function (arg1, arg2) \\{
		var t1 = 0,
			t2 = 0,
			r1, r2;
		try \\{
			t1 = arg1.toString().split(".")[1].length
		\\} catch (e) \\{\\}
		try \\{
			t2 = arg2.toString().split(".")[1].length
		\\} catch (e) \\{\\}
		with(Math) \\{
			r1 = Number(arg1.toString().replace(".", ""));
			r2 = Number(arg2.toString().replace(".", ""));
			return (r1 / r2) * pow(10, t2 - t1);
		\\}
	\\}
\\}	

```



### 多层数据的查找

> [面试题：给你个id，去拿到name，多叉树遍历](https://segmentfault.com/a/1190000014381365)

```javascript
var cityData = [
      \\{
        id: 1,
        name: '广东省',
        children: [
          \\{
            id: 11,
            name: '深圳',
            children: [
              \\{
                id: 111,
                name: '宝安',
                children: [
                  \\{
                    id: 1111,
                    name: '西乡',
                    children:[
                      \\{
                        id: 11111,
                        name: '坪洲',
                        children:[]
                      \\},
                      \\{
                        id: 11112,
                        name: '灵芝',
                        children:[]
                      \\}
                    ]
                  \\},
                  \\{
                    id: 1112,
                    name: '南山',
                    children:[
                      \\{
                        id: 11121,
                        name: '科技园',
                        children:[]
                      \\}
                    ]
                  \\}
                ]
              \\},
              \\{
                id: 112,
                name: '福田',
                children: []
              \\}
            ]
          \\},
          \\{
            id: 12,
            name: '广州',
            children: [
              \\{
                id: 122,
                name: '白云区',
                children: [
                  \\{
                    id: 1222,
                    name: '白云区',
                    children: []
                  \\}
                ]
              \\},
              \\{
                id: 122,
                name: '珠海区',
                children: []
              \\}
            ]
          \\}
        ]
      \\},
      \\{
        id: 2,
        name: '湖南省',
        children: []
      \\}
    ];

```

**递归方法**

```javascript
let result = ''

// 递归实现
const recursion = (cityData, id) => \\{
  // cityData数据为空的时候直接返回
  if (!cityData || !cityData.length) return;
  // 常规循环cityData
  for (let i = 0, len = cityData.length; i < len; i++) \\{
    const childs = cityData[i].children;
    
    // 如果匹配到id的话，就是我们要的结果
    if (cityData[i].id === id) \\{
      result = cityData[i].name
    \\}
    // 如果还有子节点，执行递归
    if(childs && childs.length > 0)\\{
      recursion(childs, id);
    \\}
  \\}
  return result
\\};

const r = recursion(cityData, 11112);
console.log(r) // 灵芝

```

**广度优先实现**

```javascript
let result = ''

const range = (cityData, id) => \\{
  if (!cityData || !cityData.length) return;
  // 定义一个数据栈
  let stack = [];

  let item = null;

  //先将第一层节点放入栈
  for (var i = 0, len = cityData.length; i < len; i++) \\{
    stack.push(cityData[i]);
  \\}

  while (stack.length) \\{
    // 将数据栈的第一个取出来
    item = stack.shift();
    // 如果符合就赋值给result
    if (item.id === id) \\{
      result = item.name
    \\}
    //如果该节点有子节点，继续添加进入栈底
    if (item.children && item.children.length) \\{
      stack = stack.concat(item.children);
    \\}
  \\}
  return result
\\};

let r1 = range(cityData, 11112);

console.log(r1) // 灵芝

```

**深度优先实现**

```javascript
let result = ''

const deep = (cityData, id) => \\{
  // 没有数据直接返回
  if (!cityData || !cityData.length) return;
  // 先定义一个数据栈
  let stack = []
  let item = null

  //先将第一层节点放入数据栈
  for (var i = 0, len = cityData.length; i < len; i++) \\{
    stack.push(cityData[i])
  \\}
  // 循环
  while (stack.length) \\{
    item = stack.shift()
    if (item.id === id) \\{
      result = item.name
    \\}
    //如果该节点有子节点，继续添加进入栈顶
    if (item.children && item.children.length) \\{
      // 注意这里调换了顺序
      stack = item.children.concat(stack);
    \\}
  \\}
  return result
\\};

let r3 = deep(cityData, 11112)
console.log(r3) // 灵芝

```

**正则方式实现**

```javascript
const regular = (cityData, id) => \\{
  // 没有数据直接返回
  if (!cityData || !cityData.length) return;
  // 数据转成字符串
  let cityStr = JSON.stringify(cityData)
  // 定义正则
  let reg = new RegExp(`"id":$\\{id\\},"name":"([^\\x00-\\xff]+)",`)
  // 取到正则的子字符串并返回
  return (cityStr.match(reg))[1]
\\}

let r4 = regular(cityData, 11112);

console.log(r4) // 灵芝


```

** 图片canvas压缩 转blob对象 **

```javascript
utils = \\{
	// 压缩比率
    quality: 0.5,
    // 执行压缩图片
    photoCompress: function (file, w, objDiv)\\{
        var ready = new FileReader();
        /*开始读取指定的Blob对象或File对象中的内容. 当读取操作完成时,readyState属性的值会成为DONE,如果设置了onloadend事件处理程序,则调用之.同时,result属性中将包含一个data: URL格式的字符串以表示所读取文件的内容.*/
        ready.readAsDataURL(file);
        ready.onload = function()\\{
            var re = this.result;
            utils.canvasDataURL(re, w, objDiv)
        \\}
    \\},
    // 压缩图片的详细
    canvasDataURL: function (path, obj, callback)\\{
        var img = new Image();
        img.src = path;
        img.onload = function()\\{
            var that = this;
            // 默认按比例压缩
            var w = that.width,
                h = that.height,
                scale = w / h;
            w = obj.width || w;
            h = obj.height || (w / scale);
            var quality = 0.7;  // 默认图片质量为0.7
            //生成canvas
            var canvas = document.createElement('canvas');
            var ctx = canvas.getContext('2d');
            // 创建属性节点
            var anw = document.createAttribute("width");
            anw.nodeValue = w;
            var anh = document.createAttribute("height");
            anh.nodeValue = h;
            canvas.setAttributeNode(anw);
            canvas.setAttributeNode(anh);
            ctx.drawImage(that, 0, 0, w, h);
            // 图像质量
            if(obj.quality && obj.quality <= 1 && obj.quality > 0)\\{
                quality = obj.quality;
            \\}
            // quality值越小，所绘制出的图像越模糊
            var base64 = canvas.toDataURL('image/jpeg', quality);
            // 回调函数返回base64的值
            callback(base64);
        \\}
    \\},
    /**
        * 将以base64的图片url数据转换为Blob
        * @param urlData
        *            用url方式表示的base64图片数据
        */
    convertBase64UrlToBlob: function (urlData)\\{
        var arr = urlData.split(','), mime = arr[0].match(/:(.*?);/)[1],
            bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
        while(n--)\\{
            u8arr[n] = bstr.charCodeAt(n);
        \\}
        return new Blob([u8arr], \\{type:mime\\});
    \\}
\\}

```



### 格式化日期

> 垃圾代码

```javascript
// 序列化日期
/**
 * @param 获取当前日期的时间戳返回对应日期 
 * @param \\{Number | String\\}
 * @param \\{Number\\} 1 => "2017-09-08 09:25:21"
 * @param \\{Number\\} 2 => "2017-09-08"
 * @prarm \\{String\\} year  获取当前年份 
 * @prarm \\{String\\} month  获取当前月份 
 * @prarm \\{String\\} day  获取当前几号 
 * */
export const formatDate =  (option) => \\{
  option = option || \\{\\};
  option.time = option.time || '/';
  option.type = option.type || "";
  // 为什么转成时间戳 因为ios - 的时间格式会报错
  option.time = Date.parse( option.time );
  if( isNaN( option.time ) )\\{
    return '/'
  \\};
  let date = new Date(option.time),
    year = date.getFullYear(),
    month = date.getMonth() + 1,
    day = date.getDate(),
    hour = date.getHours(),
    minute = date.getMinutes(),
    second = date.getSeconds();
  month < 10 ? month = '0' + month : month = month.toString();
  day < 10 ? day = '0' + day : day = day.toString();
  hour < 10 ? hour = '0' + hour : hour = hour.toString();
  minute < 10 ? minute = '0' + minute : minute = minute.toString();
  second < 10 ? second = '0' + second : second = second.toString();
  switch (option.type) \\{
    case 1:
      var time = year + "-" + month + "-" + day + " " + hour + ":" + minute + ":" + second;
      return time;
      break;
    case 2:
      return year + "-" + month + "-" + day;
      break;
    case 'year':
      return year
      break;
    case 'month':
      return month
      break;
    case 'day':
      return day
      break;
    default:
      return ''
      break;
  \\}
\\}

```



### echarts 半环形进度条

>  [例子地址](http://gallery.echartsjs.com/editor.html?c=xrJzQ35eVM) 复制上去配置项


```javascript
option = \\{
    tooltip: \\{
        formatter: "\\{a\\} <br/>\\{b\\} : \\{c\\}"
    \\},
    series: [\\{
        //类型
        type: 'gauge',
        //半径
        radius: 180,
        //起始角度。圆心 正右手侧为0度，正上方为90度，正左手侧为180度。
        startAngle: 180,
        //结束角度。
        endAngle: 0,
        center: ['50\\%', '50\\%'],
        //仪表盘轴线相关配置。
        axisLine: \\{
            show: true,
            // 属性lineStyle控制线条样式
            lineStyle: \\{
                width: 40,
                color: [
                    [0.6, '#3ebfff'],
                    [1, '#f5f5f5']
                ]
            \\}
        \\},
        //分隔线样式。
        splitLine: \\{
            show: false,
        \\},
        //刻度样式。
        axisTick: \\{
            show: false,
        \\},
        //刻度标签。
        axisLabel: \\{
            show: true,
            distance: -20,
            lineHeight: 100,
            color: '#000',
            formatter: function( params )\\{
                if( params == 0  )\\{
                    return '\n\n\n\v\v' + 0
                \\}else if( params == 100 )\\{
                    return '\n\n\n\v' + 100
                \\}else\\{
                    return ''
                \\}
            \\}
        \\},
        //仪表盘指针。
        pointer: \\{
            //这个show属性好像有问题，因为在这次开发中，需要去掉指正，我设置false的时候，还是显示指针，估计是BUG吧，我用的echarts-3.2.3；希望改进。最终，我把width属性设置为0，成功搞定！
            show: false,
            //指针长度
            length: '90\\%',
            width: 0,
        \\},
        //仪表盘标题。
        title: \\{
            show: true,
            offsetCenter: [0, '-25\\%'], // x, y，单位px
            textStyle: \\{
                color: '#000',
                fontSize: 12
            \\}
        \\},
        //仪表盘详情，用于显示数据。
        detail: \\{
            show: false,
            offsetCenter: [0, '-10\\%'],
            formatter: '\\{value\\}',
            textStyle: \\{
                fontSize: 12
            \\}
        \\},
        data: [\\{
            value: '',
            name: '60\\%',
        \\}]
    \\}]
\\};

```



### 数组去重

```javascript
Array.prototype.unique = function () \\{
  const newArray = [];
  let isRepeat;
  for (let i = 0; i < this.length; i++) \\{
    isRepeat = false;
    for (let j = 0; j < newArray.length; j++) \\{
      if (this[i] === newArray[j]) \\{
        isRepeat = true;
        break;
      \\}
    \\}
    if (!isRepeat) \\{
      newArray.push(this[i]);
    \\}
  \\}
  return newArray;
\\}

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```

```javascript
Array.prototype.unique = function () \\{
  const newArray = [];
  let isRepeat;
  for (let i = 0; i < this.length; i++) \\{
    isRepeat = false;
    for (let j = i + 1; j < this.length; j++) \\{
      if (this[i] === this[j]) \\{
        isRepeat = true;
        break;
      \\}
    \\}
    if (!isRepeat) \\{
      newArray.push(this[i]);
    \\}
  \\}
  return newArray;
\\}

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```

```javascript
Array.prototype.unique = function () \\{
  const newArray = [];
  
  for (let i = 0; i < this.length; i++) \\{
    for (let j = i + 1; j < this.length; j++) \\{
      if (this[i] === this[j]) \\{
        j = ++i;
      \\}
    \\}
    newArray.push(this[i]);
  \\}
  return newArray;
\\}

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```

- 10万个随机数的时间

```javascript
test1: 3688.440185546875ms
test2: 4641.60498046875ms
test3: 17684.365966796875ms

```

- indexOf

```javascript
// 利用Array.prototype.filter()过滤功能
// Array.prototype.indexOf()返回的是第一个索引值
// 只将数组中元素第一次出现的返回
// 之后出现的将被过滤掉

Array.prototype.unique = function () \\{
  return this.filter((item, index) => \\{
    return this.indexOf(item) === index;
  \\})
\\}

let arr = [1, 2, 3, 22, 233, 22, 2, 233, 'a', 3, 'b', 'a'];
Array.prototype.unique = function () \\{
  const newArray = [];
  this.forEach(item => \\{
    if (newArray.indexOf(item) === -1) \\{
      newArray.push(item);
    \\}
  \\});
  return newArray;
\\}

// 耗时
test1: 4887.201904296875ms
test2: 3766.324951171875ms

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


```

```javascript
Array.prototype.unique = function () \\{
  const newArray = [];
  this.sort();
  for (let i = 0; i < this.length; i++) \\{
    if (this[i] !== this[i + 1]) \\{
      newArray.push(this[i]);
    \\}
  \\}
  return newArray;
\\}

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

Array.prototype.unique = function () \\{
  const newArray = [];
  this.sort();
  for (let i = 0; i < this.length; i++) \\{
    if (this[i] !== newArray[newArray.length - 1]) \\{
      newArray.push(this[i]);
    \\}
  \\}
  return newArray;
\\}

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

test1: 121.6259765625ms
test2: 123.02197265625ms

```

```javascript
Array.prototype.unique = function () \\{
  const newArray = [];
  this.forEach(item => \\{
    if (!newArray.includes(item)) \\{
      newArray.push(item);
    \\}
  \\});
  return newArray;
\\}

test: 4123.377197265625ms

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


```

```javascript
Array.prototype.unique = function () \\{
  return this.sort().reduce((init, current) => \\{
    if(init.length === 0 || init[init.length - 1] !== current)\\{
      init.push(current);
    \\}
    return init;
  \\}, []);
\\}
test: 180.401123046875ms

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```

```javascript
Array.prototype.unique = function () \\{
  const newArray = [];
  const tmp = new Map();
  for(let i = 0; i < this.length; i++)\\{
        if(!tmp.get(this[i]))\\{
            tmp.set(this[i], 1);
            newArray.push(this[i]);
        \\}
    \\}
    return newArray;
\\}

Array.prototype.unique = function () \\{
  const tmp = new Map();
  return this.filter(item => \\{
    return !tmp.has(item) && tmp.set(item, 1);
  \\})
\\}

// 综合考虑 map最优
test1: 27.89697265625ms
test2: 21.945068359375ms

作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
作者：棕小渐
链接：https://juejin.im/post/5b0284ac51882542ad774c45
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```



### 全屏化某个DOM

```javascript
export default \\{
  data() \\{
    return \\{
      isFull: false
    \\};
  \\},
  mounted() \\{
    this.addListenWindow();
  \\},
  beforeDestroy() \\{
    this.removeListenWindow();
  \\},
  methods: \\{
    toggleFullScreen($el = document.querySelector("body")) \\{
      $el && this.fullScreen($el);
    \\},
    // 以下是全屏的逻辑
    fullScreen(el) \\{
      // 进入全屏  退出全屏
      if (window.navigator.userAgent.indexOf(".NET ") > -1) \\{
        if (
          window.outerHeight === window.screen.height &&
          window.outerWidth === window.screen.width
        ) \\{
          this.escFullScreen(el);
        \\} else \\{
          this.toFullScreen(el);
        \\}
      \\} else \\{
        !this.isFullScreen() ? this.toFullScreen(el) : this.escFullScreen(el);
      \\}
    \\},
    // 进入全屏
    toFullScreen(el) \\{
      (el.requestFullscreen && el.requestFullscreen()) ||
        (el.mozRequestFullScreen && el.mozRequestFullScreen()) ||
        (el.webkitRequestFullscreen && el.webkitRequestFullscreen()) ||
        (el.msRequestFullscreen && el.msRequestFullscreen());
      this.isFull = true;
    \\},
    // 退出全屏
    escFullScreen() \\{
      if (document.exitFullscreen) \\{
        document.exitFullscreen();
      \\} else if (document.mozCancelFullScreen) \\{
        document.mozCancelFullScreen();
      \\} else if (document.webkitExitFullscreen) \\{
        document.webkitExitFullscreen();
      \\} else if (document.msExitFullscreen) \\{
        document.msExitFullscreen();
      \\}
      this.isFull = false;
    \\},
    // 判断是否进入全屏
    isFullScreen() \\{
      // 火狐升级导致判断失效了 只用window去判断 谷歌 68版本以上也会有这个问题
      // window.fullScreen
      if (navigator.userAgent.indexOf("Firefox") >= 0) \\{
        return window.fullScreen;
      \\} else \\{
        return (
          window.fullScreen ||
          document.webkitIsFullScreen ||
          document.msFullscreenEnabled
        );
      \\}
    \\},
    // 获取chrome版本号
    getChromeVerson() \\{
      let userAgent = navigator.userAgent;
      let strStart = userAgent.indexOf("Chrome");
      let strStop = userAgent.indexOf(" Safari");
      let temp = userAgent.substring(strStart, strStop);
      let arr = temp.match(/\d+/);
      let version = arr[0] ? arr[0] : -1;
      return version;
    \\},
    addListenWindow() \\{
      // window.addEventListener("resize", this.toggleChange)
      document.addEventListener("fullscreenchange", this.toggleChange);
      document.addEventListener("webkitfullscreenchange", this.toggleChange);
      document.addEventListener("mozfullscreenchange", this.toggleChange);
      document.addEventListener("MSFullscreenChange", this.toggleChange);
    \\},
    removeListenWindow() \\{
      // window.removeEventListener("resize", this.toggleChange)
      document.removeEventListener("fullscreenchange", this.toggleChange);
      document.removeEventListener("webkitfullscreenchange", this.toggleChange);
      document.removeEventListener("mozfullscreenchange", this.toggleChange);
      document.removeEventListener("MSFullscreenChange", this.toggleChange);
    \\},
    toggleChange() \\{
      clearTimeout(this.reseizeTimeId);
      // 避免多次触发
      this.reseizeTimeId = setTimeout(() => \\{
        if (window.navigator.userAgent.indexOf(".NET ") > -1) \\{
          if (
            window.outerHeight === window.screen.height &&
            window.outerWidth === window.screen.width
          ) \\{
            this.isFull = true;
          \\} else \\{
            this.isFull = false;
          \\}
        \\} else \\{
          !this.isFullScreen() && (this.isFull = false);
        \\}
      \\}, 200);
    \\}
  \\}
\\};
```



### 格式化日期

```javascript
/*@param date 时间戳*/
/*@param format 时间格式*/
function dateFormat(date,format)\\{
    if(!format || typeof format !== 'string')\\{
      console.error('format is undefiend or type is Error');
      return '';
    \\}

    date = date instanceof Date? date : (typeof date === 'number'|| typeof date === 'string')? new Date(date): new Date();

    //解析
    var formatReg = \\{
      'y+': date.getFullYear(),
      'M+': date.getMonth()+1,
      'd+': date.getDate(),
      'h+': date.getHours(),
      'm+': date.getMinutes(),
      's+': date.getSeconds()
    \\}
    for(var reg in formatReg)\\{
      if(new RegExp(reg).test(format))\\{
            var match = RegExp.lastMatch;
            format = format.replace(match, formatReg[reg]< 10 ? '0'+formatReg[reg]: formatReg[reg].toString() );
      \\}
    \\}
    return format;
\\}

dateFormat(new Date().getTime(),'yyyy-MM-dd hh:mm:ss') 
dateFormat(new Date().getTime(),'MM-dd-yy hh:mm:ss') 
```



### 获取URL 域名 + 端口

```javascript
export const getBaseUrl = url => \\{
    var reg = /^((\w+):\/\/([^/:]*)(?::(\d+))?)(.*)/
    reg.exec(url)
    return RegExp.$1
\\}
```



### bytes转其他单位

```javascript
export const bytesToSize = bytes => \\{
    if (bytes === 0) return '0 B'
    let k = 1000 // or 1024
    let sizes = ['B', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']
    let i = Math.floor(Math.log(bytes) / Math.log(k))
    return (bytes / Math.pow(k, i)).toPrecision(3) + ' ' + sizes[i]
\\}
```



### 数组打乱

```javascript
export const randomArr = arr => \\{
    function randomsort () \\{
        return Math.random() > 0.5 ? -1 : 1
        // 用Math.random()函数生成0~1之间的随机数与0.5比较，返回-1或1
    \\}
    let newArr = arr.sort(randomsort)
    return newArr
\\}
```



### trigger 实现

```javascript
export const trigger = (el, event) => \\{
    if (document.all) \\{
        el.event()
    \\} else \\{
        const evt = document.createEvent('Events') // 还有onchange则是HtmlEvents
        evt.initEvent(event, true, true)
        el.dispatchEvent(evt)
    \\}
\\}
```



### 下载传入的文件流

```javascript
/**
 * 下载传入的文件流
 * @param \\{ Blob \\} blob 文件流
 * @param \\{ String \\} file_name 生成的文件名称 例如 xxx.jpg xxx.txt
 */
export const download_blob = (blob, file_name) => \\{
    return new Promise((resolve, reject) => \\{
        try \\{
            const BLOB = new Blob([blob])
            if ('download' in document.createElement('a')) \\{
                // 非IE下载
                const elink = document.createElement('a')
                elink.download = file_name
                elink.style.display = 'none'
                elink.href = URL.createObjectURL(BLOB)
                document.body.appendChild(elink)
                elink.click()
                // trigger 不触发下载 trigger( elink, 'click' )
                // 删除引用 释放URL 对象
                URL.revokeObjectURL(elink.href)
                document.body.removeChild(elink)
                // IE10+下载
            \\} else \\{
                navigator.msSaveBlob(BLOB, file_name)
            \\}
            resolve(\\{
                status: 'success',
                content: ''
            \\})
        \\} catch (error) \\{
            reject(error)
        \\}
    \\})
\\}
```



### dataURLtoBlob

```javascript
export const dataURLtoBlob = dataurl => \\{
    let arr = dataurl.split(',')
    let mime = arr[0].match(/:(.*?);/)[1]
    let bstr = atob(arr[1])
    let n = bstr.length
    let u8arr = new Uint8Array(n)
    while (n--) \\{
        u8arr[n] = bstr.charCodeAt(n)
    \\}
    return new Blob([u8arr], \\{ type: mime \\})
\\}
```



### 时间戳转多少时间

```javascript
/**
 * 时间戳转多少时间
 * @param \\{Date\\} 日期时间戳
 */
export const time2Long = date => \\{
    // 传入时间戳
    if (isNaN(date)) \\{
        return '/'
    \\}
    // 1 - 1000 毫秒
    if (date >= 1 && date < 1000) \\{
        return `$\\{date\\} 毫秒`
        // 1-59s  1000 - 59999
    \\} else if (date >= 1000 && date < 60000) \\{
        return `$\\{Math.round(date / 1000)\\} 秒`
        // 1-59.99分 1*60s*1000  59.99*60*1000 3599400  3600000
    \\} else if (date >= 60000 && date < 3600000) \\{
        return `$\\{Math.round(date / 60000)\\} 分钟`
        // 24小时 一小时3600000毫秒 86400000
    \\} else if (date >= 3600000 && date < 86400000) \\{
        return `$\\{Math.round(date / 3600000)\\} 小时`
    \\} else if (date >= 86400000) \\{
        return `$\\{Math.round(date / 86400000)\\} 天`
    \\}
\\}
```



### 数组上移下移

```javascript
\\{
	moveTop(index) \\{
      const cur = this.tableData.rows[index];
      cur && this.swapItems(index, index - 1);
    \\},
    moveBottom(index) \\{
      const cur = this.tableData.rows[index];
      cur && this.swapItems(index, index + 1);
    \\},
    swapItems(index1, index2) \\{
      this.tableData.rows[index1] = this.tableData.rows.splice(
        index2,
        1,
        this.tableData.rows[index1]
      )[0];
    \\},
\\}
```



### 数组分组

```javascript
// 比如三个一组
for (let i = 0; i < length; i += 3) \\{
          newArr.push(arr.slice(i, i + 3));
        \\}
```



### 百度地图和浏览器定位的封装 

```javascript
// 百度地图右键点击事件是 `rightclick`
import BMap from "BMap";

export default \\{
  methods: \\{
    // 将获取的位置解析为百度API
    translatePoint(x, y) \\{
      return new Promise((resolve, reject) => \\{
        const point = new BMap.Point(x, y);
        const convertor = new BMap.Convertor();
        let pointArr = [];
        pointArr.push(point);
        convertor.translate(pointArr, 1, 5, data => \\{
          if (data.status === 0) \\{
            resolve(data);
          \\} else \\{
            reject(new Error("坐标转换失败"));
          \\}
        \\});
      \\});
    \\},
    // 封装获取位置API方法
    promiseGeo() \\{
      return new Promise((resolve, reject) => \\{
        window.navigator.geolocation.getCurrentPosition(
          data => \\{
            data.coords && resolve(data);
          \\},
          err => \\{
            reject(err);
          \\},
          \\{ timeout: 2000 \\}
        );
      \\});
    \\},
    // 坐标解析成地址
    position2Address(position) \\{
      return new Promise((resolve, reject) => \\{
        const myGeo = new BMap.Geocoder();
        myGeo.getLocation(position, rs => \\{
          var addComp = rs.addressComponents;
          if (addComp) \\{
            resolve(addComp.province);
          \\} else \\{
            reject(new Error());
          \\}
        \\});
      \\});
    \\},
    // 地址解析成坐标
    address2Position(address) \\{
      return new Promise((resolve, reject) => \\{
        const myGeo = new BMap.Geocoder();
        myGeo.getPoint(address, point => \\{
          point ? resolve(point) : reject(new Error("您的位置没有解析到结果"));
        \\});
      \\});
    \\},
    // 根据用户信息所在的省份设置默认展示的省份
    setPositionByAddress(address) \\{
      this.address2Position(address).then(data => \\{
        this.map.setCenter(data);
      \\});
    \\},
    createContextMenu(menuArr = []) \\{
      const menu = new BMap.ContextMenu();
      menuArr.forEach(v => \\{
        menu.addItem(new BMap.MenuItem(v.name, v.callback, 100));
      \\});
      this.map.addContextMenu(menu);
    \\}
  \\}
\\};
```



### 百度地图画块逻辑

```javascript
\\{
	/**
     *
     * 添加地块的逻辑
     */
    // 弹窗点击确认后 获取弹窗中的数据
    getPolygonData(data) \\{
      this.mapStatus = "edit";
      this.curPointArr = [];
      // 先实例化一个区域范围
      this.createPolygon(data);
      // 监听地图点击事件 给这个范围加点 圈选开始 开始编辑  添加这些点
      this.map.addEventListener("click", this.updatePolygonPoint);
    \\},
    //
    updatePolygonPoint(event) \\{
      // 如果点的是拖动的点 不加
      if (event.domEvent.target.className === "BMap_vectex BMap_vectex_node") \\{
        return;
      \\}
      this.curPointArr = this.curPolygon.getPath();
      // 每次点击改变这个实例化的
      this.curPointArr.push(event.point);
      this.curPolygon.setPath(this.getPolygonPath());
      this.curPolygon.enableEditing();
    \\},
    // 创建点
    createPolygon(data) \\{
      const polygon = new BMap.Polygon(this.getPolygonPath(), \\{
        strokeColor: data.color,
        strokeWeight: 1,
        strokeOpacity: 1,
        fillColor: data.color,
        fillOpacity: 0.4
      \\});
      polygon.htData = data;
      this.map.addOverlay(polygon);
      polygon.enableEditing();
      this.addPolygonEvent(polygon);
      this.curPolygon = polygon;
    \\},
    // 将点解析为可以画圈的点
    getPolygonPath() \\{
      return this.curPointArr.map(v => \\{
        const \\{ lng, lat \\} = v;
        return new BMap.Point(lng, lat);
      \\});
    \\}
\\}
```



### 省市对应坐标

```javascript
export default \\{
  北京市: [116.4551, 40.2539],
  天津市: [117.4219, 39.4189],
  河北省: [114.4995, 38.1006],
  山西省: [112.3352, 37.9413],
  内蒙古自治区: [111.4124, 40.4901],
  辽宁省: [123.1238, 42.1216],
  吉林省: [125.8154, 44.2584],
  黑龙江省: [127.9688, 45.368],
  上海市: [121.4648, 31.2891],
  江苏省: [118.8062, 31.9208],
  浙江省: [119.5313, 29.8773],
  安徽省: [117.29, 32.0581],
  福建省: [119.4543, 25.9222],
  江西省: [116.0046, 28.6633],
  山东省: [117.1582, 36.8701],
  河南省: [113.4668, 34.6234],
  湖北省: [114.3896, 30.6628],
  湖南省: [113.0823, 28.2568],
  广东省: [113.5107, 23.2196],
  广西壮族自治区: [108.479, 23.1152],
  海南省: [110.3893, 19.8516],
  重庆市: [107.7539, 30.1904],
  四川省: [103.9526, 30.7617],
  贵州省: [106.6992, 26.7682],
  云南省: [102.9199, 25.4663],
  西藏自治区: [91.1865, 30.1465],
  陕西省: [109.1162, 34.2004],
  甘肃省: [103.5901, 36.3043],
  青海省: [101.4038, 36.8207],
  宁夏回族自治区: [106.3586, 38.1775],
  新疆维吾尔自治区: [87.9236, 43.5883],
  台湾: [121.6, 24.9],
  澳门: [22.1, 113.33],
  香港: [114.15, 22.15],

  北京: [116.4551, 40.2539],
  天津: [117.4219, 39.4189],
  河北: [114.4995, 38.1006],
  山西: [112.3352, 37.9413],
  内蒙古: [111.4124, 40.4901],
  辽宁: [123.1238, 42.1216],
  吉林: [125.8154, 44.2584],
  黑龙江: [127.9688, 45.368],
  上海: [121.4648, 31.2891],
  江苏: [118.8062, 31.9208],
  浙江: [119.5313, 29.8773],
  安徽: [117.29, 32.0581],
  福建: [119.4543, 25.9222],
  江西: [116.0046, 28.6633],
  山东: [117.1582, 36.8701],
  河南: [113.4668, 34.6234],
  湖北: [114.3896, 30.6628],
  湖南: [113.0823, 28.2568],
  广东: [113.5107, 23.2196],
  广西: [108.479, 23.1152],
  海南: [110.3893, 19.8516],
  重庆: [107.7539, 30.1904],
  四川: [103.9526, 30.7617],
  贵州: [106.6992, 26.7682],
  云南: [102.9199, 25.4663],
  西藏: [91.1865, 30.1465],
  陕西: [109.1162, 34.2004],
  甘肃: [103.5901, 36.3043],
  青海: [101.4038, 36.8207],
  宁夏: [106.3586, 38.1775],
  新疆: [87.9236, 43.5883],

  合肥: [117.29, 32.0581],
  东莞: [113.8953, 22.901],
  东营: [118.7073, 37.5513],
  中山: [113.4229, 22.478],
  临汾: [111.4783, 36.1615],
  临沂: [118.3118, 35.2936],
  丹东: [124.541, 40.4242],
  丽水: [119.5642, 28.1854],
  乌鲁木齐: [87.9236, 43.5883],
  佛山: [112.8955, 23.1097],
  保定: [115.0488, 39.0948],
  兰州: [103.5901, 36.3043],
  包头: [110.3467, 41.4899],
  北海: [109.314, 21.6211],
  南京: [118.8062, 31.9208],
  南宁: [108.479, 23.1152],
  南昌: [116.0046, 28.6633],
  南通: [121.1023, 32.1625],
  厦门: [118.1689, 24.6478],
  台州: [121.1353, 28.6688],

  呼和浩特: [111.4124, 40.4901],
  咸阳: [108.4131, 34.8706],
  哈尔滨: [127.9688, 45.368],
  唐山: [118.4766, 39.6826],
  嘉兴: [120.9155, 30.6354],
  大同: [113.7854, 39.8035],
  大连: [122.2229, 39.4409],
  太原: [112.3352, 37.9413],
  威海: [121.9482, 37.1393],
  宁波: [121.5967, 29.6466],
  宝鸡: [107.1826, 34.3433],
  宿迁: [118.5535, 33.7775],
  常州: [119.4543, 31.5582],
  广州: [113.5107, 23.2196],
  廊坊: [116.521, 39.0509],
  延安: [109.1052, 36.4252],
  张家口: [115.1477, 40.8527],
  徐州: [117.5208, 34.3268],
  德州: [116.6858, 37.2107],
  惠州: [114.6204, 23.1647],
  成都: [103.9526, 30.7617],
  扬州: [119.4653, 32.8162],
  承德: [117.5757, 41.4075],
  拉萨: [91.1865, 30.1465],
  无锡: [120.3442, 31.5527],
  日照: [119.2786, 35.5023],
  昆明: [102.9199, 25.4663],
  杭州: [119.5313, 29.8773],
  枣庄: [117.323, 34.8926],
  柳州: [109.3799, 24.9774],
  株洲: [113.5327, 27.0319],
  武汉: [114.3896, 30.6628],
  汕头: [117.1692, 23.3405],
  江门: [112.6318, 22.1484],
  沈阳: [123.1238, 42.1216],
  沧州: [116.8286, 38.2104],
  河源: [114.917, 23.9722],
  泉州: [118.3228, 25.1147],
  泰安: [117.0264, 36.0516],
  泰州: [120.0586, 32.5525],
  济南: [117.1582, 36.8701],
  济宁: [116.8286, 35.3375],
  海口: [110.3893, 19.8516],
  淄博: [118.0371, 36.6064],
  淮安: [118.927, 33.4039],
  深圳: [114.5435, 22.5439],
  清远: [112.9175, 24.3292],
  温州: [120.498, 27.8119],
  渭南: [109.7864, 35.0299],
  湖州: [119.8608, 30.7782],
  湘潭: [112.5439, 27.7075],
  滨州: [117.8174, 37.4963],
  潍坊: [119.0918, 36.524],
  烟台: [120.7397, 37.5128],
  玉溪: [101.9312, 23.8898],
  珠海: [113.7305, 22.1155],
  盐城: [120.2234, 33.5577],
  盘锦: [121.9482, 41.0449],
  石家庄: [114.4995, 38.1006],
  福州: [119.4543, 25.9222],
  秦皇岛: [119.2126, 40.0232],
  绍兴: [120.564, 29.7565],
  聊城: [115.9167, 36.4032],
  肇庆: [112.1265, 23.5822],
  舟山: [122.2559, 30.2234],
  苏州: [120.6519, 31.3989],
  莱芜: [117.6526, 36.2714],
  菏泽: [115.6201, 35.2057],
  营口: [122.4316, 40.4297],
  葫芦岛: [120.1575, 40.578],
  衡水: [115.8838, 37.7161],
  衢州: [118.6853, 28.8666],
  西宁: [101.4038, 36.8207],
  西安: [109.1162, 34.2004],
  贵阳: [106.6992, 26.7682],
  连云港: [119.1248, 34.552],
  邢台: [114.8071, 37.2821],
  邯郸: [114.4775, 36.535],
  郑州: [113.4668, 34.6234],
  鄂尔多斯: [108.9734, 39.2487],

  金华: [120.0037, 29.1028],
  铜川: [109.0393, 35.1947],
  银川: [106.3586, 38.1775],
  镇江: [119.4763, 31.9702],
  长春: [125.8154, 44.2584],
  长沙: [113.0823, 28.2568],
  长治: [112.8625, 36.4746],
  阳泉: [113.4778, 38.0951],
  青岛: [120.4651, 36.3373],
  韶关: [113.7964, 24.7028]
\\};
```



### 驼峰转下划线

```javascript
const hyphenateRE = /\B([A-Z])/g
 const hyphenate = str=> \\{
  return str.replace(hyphenateRE, '-$1').toLowerCase()
\\}
```



### 洗牌算法

```javascript
function shuffle(arr) \\{
    let shuffled = arr.concat(), rand;
    for (let i = shuffled.length; i--;) \\{
        rand = Math.floor(Math.random() * (i + 1));
        [shuffled[i],shuffled[rand]] = [shuffled[rand],shuffled[i]] 
    \\}
    return shuffled;
\\}
```



### 过滤html敏感符号

```javascript
function htmlEscape(text) \\{
  return text.replace(/[<>"&]/g, function(match, pos, originalText) \\{
    switch (match) \\{
      case "<":
        return "&lt;";
      case ">":
        return "&gt;";
      case "&":
        return "&amp;";
      case '"':
        return "&quot;";
    \\}
  \\});
\\}
alert(htmlEscape('<p class="greeting">Hello world!</p>'));
```



### 判断浏览器UA

```javascript
// Browser environment sniffing
export const inBrowser = typeof window !== 'undefined'
export const inWeex = typeof WXEnvironment !== 'undefined' && !!WXEnvironment.platform
export const weexPlatform = inWeex && WXEnvironment.platform.toLowerCase()
export const UA = inBrowser && window.navigator.userAgent.toLowerCase()
export const isIE = UA && /msie|trident/.test(UA)
export const isIE9 = UA && UA.indexOf('msie 9.0') > 0
export const isEdge = UA && UA.indexOf('edge/') > 0
export const isAndroid = (UA && UA.indexOf('android') > 0) || (weexPlatform === 'android')
export const isIOS = (UA && /iphone|ipad|ipod|ios/.test(UA)) || (weexPlatform === 'ios')
export const isChrome = UA && /chrome\/\d+/.test(UA) && !isEdge
export const isPhantomJS = UA && /phantomjs/.test(UA)
export const isFF = UA && UA.match(/firefox\/(\d+)/)
```



### 简体中文转繁体中文，并可区分港台繁体

> https://segmentfault.com/a/1190000020591236

```javascript
zh_CN_2_zh_HK_TW('我要做公共汽车去出差','zh-tw'); // zh-hk

function zh_CN_2_zh_HK_TW(str, type) \\{
    // 简体转繁体
    // zh :[hk,tw]
    //默认返回台湾繁体字
    var langMap = zhTraditional();
    for (var oldItem in zhTraditional) \\{
        var hasItem = str.indexOf(oldItem) > -1;
        if (hasItem) \\{
            var newStr = typeof langMap[oldItem] === 'string' ? langMap[oldItem] : langMap[oldItem][type === 'zh-tw' ? 1 : 0];
            var reg = new RegExp(oldItem, 'g');
            str = str.replace(reg, newStr);
        \\}
    \\}
    return str;
\\}


function zhTraditional()\\{
    // 这里才是重点，我费了几天时间，查找港台繁体字的区别，都整理这里了。如果你有更多的区别，评论区留下你的宝贵建议。
    return \\{
    "里面": [
        "裏面",
        "裡面"
    ],
    "软件": [
        "軟件",
        "軟體"
    ],
    "出租车": [
        "的士",
        "計程車"
    ],
    "公共汽车": [
        "巴士",
        "公車"
    ],
    "公交车": [
        "巴士",
        "公車"
    ],
    "摩托车": [
        "電單車",
        "機車"
    ],
    "摩托": [
        "電單車",
        "機車"
    ],
    "空调": [
        "冷氣機",
        "冷氣機"
    ],
    "计算器": [
        "電算器",
        "計數機"
    ],
    "钥匙": [
        "鎖匙",
        "鑰匙"
    ],
    "出差": [
        "公幹",
        "公幹"
    ],
    "游泳": [
        "游水",
        "游水"
    ],
    "烫发": [
        "電髮",
        "燙髮"
    ],
    "马铃薯": [
        "蕃薯",
        "蕃薯"
    ],
    "救护车": [
        "十字車",
        "救護車"
    ],
    "急救车": [
        "十字車",
        "救護車"
    ],
    "方便面": [
        "即食面",
        "速食面"
    ],
    "蜂蜜": [
        "蜜糖",
        "蜂蜜"
    ],
    "草莓": [
        "士多啤犁",
        "草莓"
    ],
    "水果": [
        "生果",
        "水果"
    ],
    "樱桃": [
        "車厘子",
        "櫻桃"
    ],
    "提示": [
        "貼士",
        "提示"
    ],
    "沙拉": [
        "沙律",
        "沙拉"
    ],
    "色拉": [
        "沙律",
        "沙拉"
    ],
    "话筒": [
        "咪高峰",
        "麥克風"
    ],
    "麦克风": [
        "咪高峰",
        "麥克風"
    ],
    "三明治": [
        "三文治",
        "三明治"
    ],
    "马达": [
        "摩打",
        "馬達"
    ],
    "巧克力": [
        "朱古力",
        "巧克力"
    ],
    "冰箱": [
        "雪櫃",
        "冰箱"
    ],
    "激光": [
        "鐳射",
        "雷射"
    ],
    "首席执行官": [
        "行政總監",
        "執行長"
    ],
    "首席运营官": [
        "營運總監",
        "營運長"
    ],
    "首席财务官": [
        "財務總監",
        "財務長"
    ],
    "信用证": [
        "信用證",
        "信用狀"
    ],
    "卡": [
        "咭",
        "卡"
    ],
    "瓶": [
        "樽",
        "瓶"
    ],
    "叹": [
        "歎",
        "嘆"
    ],
    "为": [
        "爲",
        "為"
    ],
    "着": [
        "着",
        "著"
    ],
    "妆": [
        "粧",
        "妝"
    ],
    "床": [
        "牀",
        "床"
    ],
    "里": [
        "裏",
        "裡"
    ],
    "线": [
        "綫",
        "線"
    ],
    "面": [
        "麪",
        "麵"
    ],
    "钩": [
        "鈎",
        "鉤"
    ],
    "群": [
        "羣",
        "群"
    ],
    "酝": [
        "醖",
        "醞"
    ],
    "卫": [
        "衞",
        "衛"
    ],
    "才": [
        "才",
        "纔"
    ],
    "峰": [
        "峯",
        "峰"
    ],
    "污": [
        "污",
        "汙"
    ],
    "爱": "愛",
    "碍": "礙",
    "袄": "襖",
    "肮": "骯",
    "罢": "罷",
    "坝": "壩",
    "摆": "擺",
    "办": "辦",
    "板": "闆",
    "帮": "幫",
    "宝": "寶",
    "报": "報",
    "贝": "貝",
    "备": "備",
    "笔": "筆",
    "币": "幣",
    "毕": "畢",
    "毙": "斃",
    "边": "邊",
    "变": "變",
    "标": "標",
    "表": "錶",
    "别": "彆",
    "宾": "賓",
    "卜": "蔔",
    "补": "補",
    "布": "佈",
    "参": "參",
    "惨": "慘",
    "蚕": "蠶",
    "灿": "燦",
    "仓": "倉",
    "层": "層",
    "产": "產",
    "搀": "攙",
    "谗": "讒",
    "馋": "饞",
    "缠": "纏",
    "忏": "懺",
    "尝": "嘗",
    "偿": "償",
    "厂": "廠",
    "长": "長",
    "车": "車",
    "彻": "徹",
    "陈": "陳",
    "尘": "塵",
    "衬": "襯",
    "唇": "脣",
    "称": "稱",
    "惩": "懲",
    "痴": "癡",
    "迟": "遲",
    "齿": "齒",
    "冲": "衝",
    "虫": "蟲",
    "丑": "醜",
    "筹": "籌",
    "处": "處",
    "触": "觸",
    "出": "齣",
    "础": "礎",
    "刍": "芻",
    "疮": "瘡",
    "辞": "辭",
    "从": "從",
    "聪": "聰",
    "丛": "叢",
    "窜": "竄",
    "达": "達",
    "呆": "獃",
    "带": "帶",
    "担": "擔",
    "胆": "膽",
    "单": "單",
    "当": "當",
    "档": "檔",
    "党": "黨",
    "导": "導",
    "灯": "燈",
    "邓": "鄧",
    "敌": "敵",
    "籴": "糴",
    "递": "遞",
    "淀": "澱",
    "点": "點",
    "电": "電",
    "垫": "墊",
    "冬": "鼕",
    "东": "東",
    "冻": "凍",
    "栋": "棟",
    "动": "動",
    "斗": "鬥",
    "独": "獨",
    "断": "斷",
    "对": "對",
    "队": "隊",
    "吨": "噸",
    "夺": "奪",
    "堕": "墮",
    "恶": "惡",
    "尔": "爾",
    "儿": "兒",
    "发": "發",
    "范": "範",
    "矾": "礬",
    "飞": "飛",
    "奋": "奮",
    "粪": "糞",
    "坟": "墳",
    "风": "風",
    "丰": "豐",
    "凤": "鳳",
    "妇": "婦",
    "复": "復",
    "麸": "麩",
    "肤": "膚",
    "盖": "蓋",
    "干": "幹",
    "赶": "趕",
    "个": "個",
    "巩": "鞏",
    "沟": "溝",
    "过": "過",
    "构": "構",
    "购": "購",
    "谷": "穀",
    "顾": "顧",
    "雇": "僱",
    "刮": "颳",
    "挂": "掛",
    "关": "關",
    "观": "觀",
    "冈": "岡",
    "广": "廣",
    "归": "歸",
    "龟": "龜",
    "柜": "櫃",
    "国": "國",
    "硅": "矽",
    "汉": "漢",
    "号": "號",
    "合": "閤",
    "轰": "轟",
    "哄": "閧",
    "后": "後",
    "胡": "鬍",
    "护": "護",
    "壶": "壺",
    "沪": "滬",
    "画": "畫",
    "划": "劃",
    "华": "華",
    "怀": "懷",
    "坏": "壞",
    "欢": "歡",
    "环": "環",
    "还": "還",
    "回": "迴",
    "会": "會",
    "秽": "穢",
    "汇": "匯",
    "伙": "夥",
    "获": "獲",
    "迹": "跡",
    "几": "幾",
    "机": "機",
    "击": "擊",
    "际": "際",
    "剂": "劑",
    "济": "濟",
    "挤": "擠",
    "积": "積",
    "饥": "飢",
    "鸡": "鷄",
    "极": "極",
    "继": "繼",
    "家": "傢",
    "价": "價",
    "夹": "夾",
    "艰": "艱",
    "荐": "薦",
    "戋": "戔",
    "坚": "堅",
    "歼": "殲",
    "监": "監",
    "见": "見",
    "茧": "繭",
    "舰": "艦",
    "鉴": "鑒",
    "拣": "揀",
    "硷": "礆",
    "姜": "薑",
    "将": "將",
    "奖": "獎",
    "浆": "漿",
    "桨": "槳",
    "酱": "醬",
    "讲": "講",
    "胶": "膠",
    "借": "藉",
    "阶": "階",
    "节": "節",
    "疖": "癤",
    "秸": "稭",
    "杰": "傑",
    "尽": "盡",
    "紧": "緊",
    "仅": "僅",
    "进": "進",
    "烬": "燼",
    "惊": "驚",
    "竞": "競",
    "旧": "舊",
    "举": "舉",
    "剧": "劇",
    "据": "據",
    "巨": "鉅",
    "惧": "懼",
    "卷": "捲",
    "觉": "覺",
    "开": "開",
    "克": "剋",
    "壳": "殼",
    "垦": "墾",
    "恳": "懇",
    "夸": "誇",
    "块": "塊",
    "矿": "礦",
    "亏": "虧",
    "昆": "崑",
    "捆": "綑",
    "困": "睏",
    "扩": "擴",
    "腊": "臘",
    "蜡": "蠟",
    "来": "來",
    "兰": "蘭",
    "拦": "攔",
    "栏": "欄",
    "烂": "爛",
    "劳": "勞",
    "痨": "癆",
    "乐": "樂",
    "类": "類",
    "累": "纍",
    "垒": "壘",
    "泪": "淚",
    "厘": "釐",
    "礼": "禮",
    "厉": "厲",
    "励": "勵",
    "离": "離",
    "历": "暦",
    "隶": "隸",
    "俩": "倆",
    "帘": "簾",
    "联": "聯",
    "恋": "戀",
    "怜": "憐",
    "炼": "煉",
    "练": "練",
    "粮": "糧",
    "两": "兩",
    "辆": "輛",
    "了": "瞭",
    "疗": "療",
    "辽": "遼",
    "猎": "獵",
    "临": "臨",
    "邻": "鄰",
    "灵": "靈",
    "龄": "齡",
    "岭": "嶺",
    "刘": "劉",
    "浏": "瀏",
    "龙": "龍",
    "楼": "樓",
    "娄": "婁",
    "录": "錄",
    "陆": "陸",
    "虏": "虜",
    "卤": "鹵",
    "卢": "盧",
    "庐": "廬",
    "泸": "瀘",
    "芦": "蘆",
    "炉": "爐",
    "乱": "亂",
    "仑": "侖",
    "罗": "羅",
    "屡": "屢",
    "虑": "慮",
    "滤": "濾",
    "驴": "驢",
    "麻": "蔴",
    "马": "馬",
    "买": "買",
    "卖": "賣",
    "迈": "邁",
    "麦": "麥",
    "脉": "脈",
    "猫": "貓",
    "蛮": "蠻",
    "门": "門",
    "黾": "黽",
    "么": "麼",
    "霉": "徾",
    "蒙": "濛",
    "梦": "夢",
    "弥": "彌",
    "庙": "廟",
    "灭": "滅",
    "蔑": "衊",
    "亩": "畝",
    "难": "難",
    "鸟": "鳥",
    "恼": "惱",
    "脑": "腦",
    "拟": "擬",
    "酿": "釀",
    "聂": "聶",
    "镊": "鑷",
    "疟": "瘧",
    "宁": "寧",
    "农": "農",
    "欧": "歐",
    "盘": "盤",
    "辟": "闢",
    "苹": "蘋",
    "凭": "憑",
    "朴": "樸",
    "仆": "僕",
    "扑": "撲",
    "栖": "棲",
    "齐": "齊",
    "气": "氣",
    "弃": "棄",
    "启": "啟",
    "岂": "豈",
    "千": "韆",
    "迁": "遷",
    "佥": "僉",
    "签": "簽",
    "牵": "牽",
    "纤": "縴",
    "蔷": "薔",
    "墙": "墻",
    "枪": "槍",
    "乔": "喬",
    "侨": "僑",
    "桥": "橋",
    "窍": "竅",
    "窃": "竊",
    "亲": "親",
    "寝": "寢",
    "庆": "慶",
    "穷": "窮",
    "琼": "瓊",
    "秋": "鞦",
    "区": "區",
    "曲": "麯",
    "趋": "趨",
    "权": "權",
    "劝": "勸",
    "确": "確",
    "让": "讓",
    "扰": "擾",
    "热": "熱",
    "认": "認",
    "荣": "榮",
    "洒": "灑",
    "伞": "傘",
    "丧": "喪",
    "扫": "掃",
    "啬": "嗇",
    "涩": "澀",
    "杀": "殺",
    "晒": "曬",
    "伤": "傷",
    "舍": "捨",
    "摄": "攝",
    "沈": "瀋",
    "审": "審",
    "渗": "滲",
    "声": "聲",
    "升": "陞",
    "胜": "勝",
    "圣": "聖",
    "绳": "繩",
    "湿": "濕",
    "适": "適",
    "时": "時",
    "实": "實",
    "势": "勢",
    "师": "師",
    "兽": "獸",
    "属": "屬",
    "数": "數",
    "术": "術",
    "树": "樹",
    "书": "書",
    "帅": "帥",
    "双": "雙",
    "松": "鬆",
    "苏": "蘇",
    "肃": "肅",
    "虽": "雖",
    "随": "隨",
    "岁": "歲",
    "孙": "孫",
    "笋": "筍",
    "它": "牠",
    "态": "態",
    "台": "臺",
    "檯": "颱",
    "摊": "攤",
    "滩": "灘",
    "瘫": "癱",
    "坛": "壇",
    "汤": "湯",
    "誊": "謄",
    "体": "體",
    "条": "條",
    "椭": "橢",
    "粜": "糶",
    "铁": "鐵",
    "听": "聽",
    "厅": "廳",
    "头": "頭",
    "图": "圖",
    "涂": "塗",
    "团": "團",
    "袜": "襪",
    "洼": "漥",
    "万": "萬",
    "弯": "彎",
    "网": "網",
    "伪": "偽",
    "韦": "韋",
    "稳": "穩",
    "乌": "烏",
    "务": "務",
    "无": "無",
    "雾": "霧",
    "牺": "犧",
    "席": "蓆",
    "系": "係",
    "戏": "戲",
    "习": "習",
    "吓": "嚇",
    "虾": "蝦",
    "绣": "繡",
    "锈": "銹",
    "献": "獻",
    "咸": "醎",
    "显": "顯",
    "宪": "憲",
    "县": "縣",
    "向": "嚮",
    "响": "響",
    "乡": "鄉",
    "协": "協",
    "写": "寫",
    "胁": "脅",
    "泻": "瀉",
    "亵": "褻",
    "衅": "釁",
    "兴": "興",
    "须": "鬚",
    "选": "選",
    "旋": "鏇",
    "悬": "懸",
    "学": "學",
    "寻": "尋",
    "逊": "遜",
    "凶": "兇",
    "压": "壓",
    "亚": "亞",
    "哑": "啞",
    "艳": "艷",
    "严": "嚴",
    "岩": "巖",
    "盐": "鹽",
    "厌": "厭",
    "养": "養",
    "痒": "癢",
    "样": "樣",
    "阳": "陽",
    "尧": "堯",
    "钥": "鑰",
    "药": "藥",
    "页": "頁",
    "叶": "葉",
    "爷": "爺",
    "业": "業",
    "医": "醫",
    "异": "異",
    "义": "義",
    "仪": "儀",
    "艺": "藝",
    "亿": "億",
    "忆": "憶",
    "隐": "隱",
    "阴": "陰",
    "蝇": "蠅",
    "应": "應",
    "营": "營",
    "拥": "擁",
    "佣": "傭",
    "踊": "踴",
    "涌": "湧",
    "痈": "癰",
    "优": "優",
    "犹": "猶",
    "邮": "郵",
    "忧": "憂",
    "余": "餘",
    "鱼": "魚",
    "御": "禦",
    "吁": "籲",
    "郁": "鬱",
    "与": "與",
    "誉": "譽",
    "屿": "嶼",
    "渊": "淵",
    "远": "遠",
    "园": "園",
    "愿": "願",
    "跃": "躍",
    "岳": "嶽",
    "云": "雲",
    "运": "運",
    "韵": "韻",
    "札": "剳",
    "扎": "紥",
    "杂": "雜",
    "灾": "災",
    "赃": "贓",
    "灶": "竈",
    "凿": "鑿",
    "枣": "棗",
    "斋": "齋",
    "战": "戰",
    "占": "佔",
    "毡": "氈",
    "赵": "趙",
    "这": "這",
    "折": "摺",
    "征": "徵",
    "症": "癥",
    "证": "證",
    "郑": "鄭",
    "只": "祗",
    "帜": "幟",
    "职": "職",
    "致": "緻",
    "制": "製",
    "执": "執",
    "滞": "滯",
    "质": "質",
    "种": "種",
    "众": "眾",
    "钟": "鐘",
    "肿": "腫",
    "周": "週",
    "昼": "晝",
    "朱": "誅",
    "筑": "築",
    "烛": "燭",
    "注": "註",
    "专": "專",
    "庄": "莊",
    "壮": "壯",
    "装": "裝",
    "状": "狀",
    "桩": "樁",
    "准": "準",
    "浊": "濁",
    "总": "總",
    "纵": "縱",
    "钻": "鑚"
\\};
\\}
```



### 判断是否是PC

```javascript
/**
 * 判断是否是PC环境
 * @return \\{Boolean\\} true 就是PC  false 不是PC
 * @description https://www.cnblogs.com/s313139232/p/9447069.html
 */
export const isPC = () => \\{
  const userAgentInfo = navigator.userAgent;
  const Agents = [
    "Android",
    "iPhone",
    "SymbianOS",
    "Windows Phone",
    "iPad",
    "iPod"
  ];
  let flag = true;
  for (let i = 0, l = Agents.length; i < l; i++) \\{
    if (userAgentInfo.indexOf(Agents[i]) > 0) \\{
      flag = false;
      break;
    \\}
  \\}
  return flag;
\\};
```



### 长按逻辑的思路

- touchstart 创建一个延迟函数
- touchmove 清除这个延迟
- touchend 清除延迟



### 音频能量分级

```javascript
// x /= y 等同于 x = x/y
var _getVolume = function(data)\\{
    //音频能量分级
    var volumeEnergy = [328,421,541,695,893,1147,1473,1892,2430,3121,4007,5145,6607,8484,10893,13987,17959,23060,29609,38018,48814,62676,80476,103329,132673,170349,218724,280837,360589,462988,594466,763280,980034,1258341,1615680,2074495,2663603,3420004,4391204];
    var getLevelByEnergy = function(energy)\\{
        var level = 40;
        volumeEnergy.every(function(value,index)\\{
            if(energy < value)\\{
                level = index;
                return false;//跳出循环
            \\}
            return true;
        \\});
        return level;
    \\};
    var calEnergy = function(data)\\{
        if(data == null || data.byteLength <= 2)\\{
            return 0;
        \\}
        // 采样平均值
        var avg = 0;
        var i;
        for(i=0;i<data.length;i++)\\{
            avg += data[i];
        \\}
        avg /= data.length;
        var energy = 0;
        for(i=0;i<data.length;i++)\\{
            energy += parseInt(Math.pow(data[i]-avg,2))>>9;
        \\}
        energy /= data.length;
        return parseInt(energy);
    \\};
    return getLevelByEnergy(calEnergy(data));
\\};
```



### bd09转wgs84等

```javascript
/**
 * @原算法 https://www.jianshu.com/p/57ca061f3987
 * @根据该作者的修改成JS版的
 * @time 2019-7-17 09:58:42
 * @description bd09 转WGS84,精准度高
 * */
let coordinateUtil = \\{
  x_pi: (3.14159265358979324 * 3000.0) / 180.0,
  //pai
  pi: 3.1415926535897932384626,
  //离心率
  ee: 0.00669342162296594323,
  //长半轴
  a: 6378245.0,
  //百度转国测局
  bd09togcj02: function(bd_lon, bd_lat) \\{
    let x = bd_lon - 0.0065;
    let y = bd_lat - 0.006;
    let z =
      Math.sqrt(x * x + y * y) - 0.00002 * Math.sin(y * coordinateUtil.x_pi);
    let theta = Math.atan2(y, x) - 0.000003 * Math.cos(x * coordinateUtil.x_pi);
    let gg_lng = z * Math.cos(theta);
    let gg_lat = z * Math.sin(theta);
    return \\{
      lng: gg_lng,
      lat: gg_lat
    \\};
  \\},
  //国测局转百度
  gcj02tobd09: function(lng, lat) \\{
    let z =
      Math.sqrt(lng * lng + lat * lat) +
      0.00002 * Math.sin(lat * coordinateUtil.x_pi);
    let theta =
      Math.atan2(lat, lng) + 0.000003 * Math.cos(lng * coordinateUtil.x_pi);
    let bd_lng = z * Math.cos(theta) + 0.0065;
    let bd_lat = z * Math.sin(theta) + 0.006;
    return \\{
      lng: bd_lng,
      lat: bd_lat
    \\};
  \\},
  //国测局转84
  gcj02towgs84: function(lng, lat) \\{
    let dlat = coordinateUtil.transformlat(lng - 105.0, lat - 35.0);
    let dlng = coordinateUtil.transformlng(lng - 105.0, lat - 35.0);
    let radlat = (lat / 180.0) * coordinateUtil.pi;
    let magic = Math.sin(radlat);
    magic = 1 - coordinateUtil.ee * magic * magic;
    let sqrtmagic = Math.sqrt(magic);
    dlat =
      (dlat * 180.0) /
      (((coordinateUtil.a * (1 - coordinateUtil.ee)) / (magic * sqrtmagic)) *
        coordinateUtil.pi);
    dlng =
      (dlng * 180.0) /
      ((coordinateUtil.a / sqrtmagic) * Math.cos(radlat) * coordinateUtil.pi);
    let mglat = lat + dlat;
    let mglng = lng + dlng;
    return \\{
      lng: lng * 2 - mglng,
      lat: lat * 2 - mglat
    \\};
  \\},
  //经度转换
  transformlat: function(lng, lat) \\{
    let ret =
      -100.0 +
      2.0 * lng +
      3.0 * lat +
      0.2 * lat * lat +
      0.1 * lng * lat +
      0.2 * Math.sqrt(Math.abs(lng));
    ret +=
      ((20.0 * Math.sin(6.0 * lng * coordinateUtil.pi) +
        20.0 * Math.sin(2.0 * lng * coordinateUtil.pi)) *
        2.0) /
      3.0;
    ret +=
      ((20.0 * Math.sin(lat * coordinateUtil.pi) +
        40.0 * Math.sin((lat / 3.0) * coordinateUtil.pi)) *
        2.0) /
      3.0;
    ret +=
      ((160.0 * Math.sin((lat / 12.0) * coordinateUtil.pi) +
        320 * Math.sin((lat * coordinateUtil.pi) / 30.0)) *
        2.0) /
      3.0;
    return ret;
  \\},
  //纬度转换
  transformlng: function(lng, lat) \\{
    let ret =
      300.0 +
      lng +
      2.0 * lat +
      0.1 * lng * lng +
      0.1 * lng * lat +
      0.1 * Math.sqrt(Math.abs(lng));
    ret +=
      ((20.0 * Math.sin(6.0 * lng * coordinateUtil.pi) +
        20.0 * Math.sin(2.0 * lng * coordinateUtil.pi)) *
        2.0) /
      3.0;
    ret +=
      ((20.0 * Math.sin(lng * coordinateUtil.pi) +
        40.0 * Math.sin((lng / 3.0) * coordinateUtil.pi)) *
        2.0) /
      3.0;
    ret +=
      ((150.0 * Math.sin((lng / 12.0) * coordinateUtil.pi) +
        300.0 * Math.sin((lng / 30.0) * coordinateUtil.pi)) *
        2.0) /
      3.0;
    return ret;
  \\},
  getWgs84xy: function(x, y) \\{
    //先转 国测局坐标
    let doubles_gcj = coordinateUtil.bd09togcj02(x, y); //（x 117.   y 36. ）
    //国测局坐标转wgs84
    let doubles_wgs84 = coordinateUtil.gcj02towgs84(
      doubles_gcj.lng,
      doubles_gcj.lat
    );
    //返回 纠偏后 坐标

    return doubles_wgs84;
  \\}
\\};
// 使用方法
coordinateUtil.getWgs84xy(lng, lat)
```



### 公共方法

> 多个项目中使用到的公共方法维护到这里。

#### debounce

> 防抖，可使用lodash的防抖代替

| 参数  | 类型     | 默认值    | 是否必填 | 描述         |
| ----- | -------- | --------- | -------- | ------------ |
| fn    | Function | undefined | 是       | 要执行的函数 |
| delay | Number   | 300       | 否       | 延迟时间     |

#### 返回值

对应的执行函数

#### 代码

```js
/**
 * 防抖
 * @param \\{function\\} fn 要执行的函数
 * @param \\{number\\} delay 延迟时间 默认300毫秒
 * @example
 * methods: \\{
 *   searchTopClick: debounce(function() \\{
 *     ...
 *   \\})
 * \\}
 */
export const debounce = function(fn, delay = 300) \\{
  let timer = null;
  return function() \\{
    const context = this;
    const args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function() \\{
      fn.apply(context, args);
    \\}, delay);
  \\};
\\};

```

#### 栗子

```js
import \\{ debounce \\} from '@assets/js/utils';
// 在普通监听中
window.addEventListener('resize', debounce(hanldeChangeSize));
// 在setup return中
return \\{
  resize: debounce(hanldeChangeSize)
\\}
```



### formatDataByType

> 格式化接口返回的数据格式 简单的 复杂的单独处理

| 参数     | 类型                                             | 默认值    | 是否必填 | 描述                                                         |
| -------- | ------------------------------------------------ | --------- | -------- | ------------------------------------------------------------ |
| data     | Any                                              | undefined | 是       | 接口返回的数据                                               |
| dataType | ['Object', 'Array', 'Null', 'String', 'Boolean'] | 'Array'   | 否       | 校验后端返回的数据是否是这个格式，如果不是，返回对应的默认值 |

#### 返回值

类型正确返回接口返回的数据，不正确返回默认值

#### 代码

```js
// 数据类型转数据 formatDataByType 这些是数据类型不对的时候返回的默认值
const dataType2data = \\{
  Object: \\{\\},
  Array: [],
  Null: null,
  String: '',
  Boolean: false
\\};
/**
 * 将后端传进的数据格式化
 * @param \\{*\\} data 传入的数据
 * @param \\{string\\} dataType 数据类型 默认 'Array' 共有 'Object'、 'Array'、 'Null'三种
 */
export const formatDataByType = function(data, dataType = 'Array') \\{
  return Object.prototype.toString.call(data) === `[object $\\{dataType\\}]`
    ? data
    : dataType2data[dataType];
\\};
```

#### 栗子

```js
import \\{ formatDataByType \\} from '@js/utils';
/**
 * 获取列表
 * @param \\{object\\} params
 */
export function getCombosList(params) \\{
  return fetch(\\{
    url: GET_VIEW_COMBOS_LIST,
    method: 'GET',
    params
  \\}).then(res => formatDataByType(res.result));
\\}

/**
 * 获取列表
 * @param \\{object\\} params
 */
export function getComboDetail(params) \\{
  return fetch(\\{
    url: GET_VIEW_COMBO_DETAIL,
    method: 'GET',
    params
  \\}).then(res => formatDataByType(res.result, 'Object'));
```



### triggerElEvent

> 触发子组件的事件 容错处理 如果报错了那么就不执行

| 参数      | 类型                                  | 默认值    | 是否必填 | 描述                               |
| --------- | ------------------------------------- | --------- | -------- | ---------------------------------- |
| el        | Vue components \| Object\|HtmlElement | Undefined | 是       | vue组件实例的引用或某个对象某个dom |
| eventName | String                                | undefined | 是       | 对应的要触发的事件名称             |
| ...args   | Any                                   | undefined | 否       | 要传给事件的参数                   |

#### 返回值

事件执行成功，返回对应的执行结果。报错，返回false。

#### 代码

```js
/**
 * 触发组件实例中的方法
 * @param \\{Vue\\} el 组件实例
 * @param \\{string\\} eventName 组件实例中的方法
 * @param \\{...\\} 要传入的参数
 * @returns \\{function\\}
 */
export const triggerElEvent = function(el, eventName, ...args) \\{
  return el && typeof el[eventName] === 'function' && el[eventName](...args);
\\};
```

#### 栗子

```js
import \\{ triggerElEvent \\} from '@js/utils';

triggerElEvent(refs.drawer, 'closeDrawer');
triggerElEvent($input, 'setName', name.value);
```



### spliceArray2Group

> 数组分组

| 参数 | 类型   | 默认值    | 是否必填 | 描述       |
| ---- | ------ | --------- | -------- | ---------- |
| arr  | Array  | Undefined | 是       | 原始数组   |
| num  | Number | undefined | 是       | 要分成几组 |

#### 返回值

分割后的数组

#### 代码

```js
/**
 * 按照数量分割数组
 * @param \\{Array\\} arr 被分割的数组
 * @param \\{Number\\} num 分割的段数
 * @returns \\{Array\\} 返回分割后的数组
 */
export const spliceArray2Group = function(arr, num) \\{
  const newArr = [];
  const length = arr.length;
  for (let i = 0; i < length; i += num) \\{
    newArr.push(arr.slice(i, i + num));
  \\}
  return newArr;
\\};
```

#### 栗子

```js
import \\{ spliceArray2Group \\} from '@js/utils';
const arr = [1,2,3,4,5,6,7,8];
spliceArray2Group(arr, 2) // [[1,2], [3,4], [5,6], [7,8]]
```



### deepClone

> 只满足于深拷贝数据的业务需求

| 参数 | 类型 | 默认值    | 是否必填 | 描述     |
| ---- | ---- | --------- | -------- | -------- |
| Obj  | Any  | Undefined | 是       | 原始数据 |

#### 返回值

深拷贝后的数据

#### 代码

```js
/**
 * 深拷贝
 * @param \\{any\\} obj 要被拷贝的数据
 */
export function deepClone(obj) \\{
  return JSON.parse(JSON.stringify(obj));
\\}
```

#### 栗子

```js
import \\{ deepClone \\} from '@js/utils';

const choicedList = deepClone(choicedApiList.value);
```



### formatDate

> 将时间戳格式化为日期

| 参数      | 类型   | 默认值  | 是否必填 | 描述                                           |
| --------- | ------ | ------- | -------- | ---------------------------------------------- |
| timestamp | Number | 0       | 是       | 时间戳                                         |
| formats   | String | 'Y-m-d' | 否       | *Y-m-d Y-m-d H:i:s Y年m月d日 Y年m月d日 H时i分* |

#### 返回值

传入的格式的日期

#### 代码

```js
const formatDayNum = function(value) \\{
  return value < 10 ? '0' + value: value;
\\};
/**
 * 时间戳转日期
 *
 * 传入
 * Y-m-d Y-m-d H:i:s Y年m月d日 Y年m月d日 H时i分
 * @param \\{number\\} timestamp 时间戳
 * @param \\{string\\} formats  Y-m-d Y-m-d H:i:s Y年m月d日 Y年m月d日 H时i分
 */
export const formatDate = function(timestamp = 0, formats = 'Y-m-d') \\{
  const myDate = timestamp ? new Date(timestamp) : new Date();
  const year = myDate.getFullYear();
  const month = formatDayNum(myDate.getMonth() + 1);
  const day = formatDayNum(myDate.getDate());
  const hour = formatDayNum(myDate.getHours());
  const minite = formatDayNum(myDate.getMinutes());
  const second = formatDayNum(myDate.getSeconds());

  return formats.replace(/Y|m|d|H|i|s/gi, function(matches) \\{
    return \\{
      Y: year,
      m: month,
      d: day,
      H: hour,
      i: minite,
      s: second
    \\}[matches];
  \\});
\\};
```

#### 栗子

```js
import \\{ formatDate \\} from '@js/utils';

formatDate(date.getTime(), 'Y-m-d H:i') // 2020-12-20 23:58
```



### isId

> 判断是否是符合规则的id 避免隐式转换

| 参数 | 类型             | 默认值    | 是否必填 | 描述     |
| ---- | ---------------- | --------- | -------- | -------- |
| id   | Number \| String | undefined | 是       | 传入的id |

#### 返回值

符合规则 true 不符合 false

#### 代码

```js
/**
 * 判断是否是id
 *
 * 如果是字符串去空格判断
 *
 * 如果是数字正则判断
 *
 * 如果是合法id  返回true
 * @param \\{Number | String\\} id
 * @returns \\{Boolean\\} true | false
 */
export function isId(id) \\{
  return typeof id === 'string' ? !!id.replace(/\s/g, '') : /^\d+$/.test(id);
\\}
```

#### 栗子

```js
import \\{ isId \\} from '@assets/js/utils';

if (isId(cacheWidth)) \\{
  // ...
\\}
```



### isIeBrowser

> 判断是否是IE浏览器

#### 返回值

是IE浏览器 返回 true 否则 false

#### 代码

```js
/**
 * 判断是否是IE浏览器
 */
export function isIeBrowser() \\{
  return (
    !!window.ActiveXObject ||
    'ActiveXObject' in window ||
    window.navigator.userAgent.indexOf('MSIE') >= 1
  );
\\}
```

#### 栗子

```js
import \\{ isIeBrowser \\} from '@js/utils';

isIeBrowser() &&
      setTimeout(() => \\{
        // ...
      \\}, 2000);
```



### getWindowScrollTop

> 获取浏览器窗口垂直滚动高度 兼容写法

#### 返回值

滚动高度数值

#### 代码

```js
/**
 * 摘抄自mdn
 * 兼容式获取window的滚动高度
 */
export function getWindowScrollTop() \\{
  const supportPageOffset = window.pageXOffset !== undefined;
  const isCSS1Compat = (document.compatMode || '') === 'CSS1Compat';

  return supportPageOffset
    ? window.pageYOffset
    : isCSS1Compat
    ? document.documentElement.scrollTop
    : document.body.scrollTop;
\\}
```

#### 栗子

```js
import \\{ getWindowScrollTop \\} from '@assets/js/utils';

const SCROLL_Y = getWindowScrollTop();
```



### getWindowScrollLeft

> 获取浏览器窗口左右滚动宽度 兼容写法

#### 返回值

滚动宽度数值

#### 代码

```js
/**
 * 摘抄自mdn
 * 兼容式获取window的滚动宽度
 */
export function getWindowScrollLeft() \\{
  const supportPageOffset = window.pageXOffset !== undefined;
  const isCSS1Compat = (document.compatMode || '') === 'CSS1Compat';

  return supportPageOffset
    ? window.pageXOffset
    : isCSS1Compat
    ? document.documentElement.scrollLeft
    : document.body.scrollLeft;
\\}
```

#### 栗子

```js
import \\{ getWindowScrollLeft \\} from '@assets/js/utils';

const SCROLL_X = getWindowScrollLeft();
```



### getQueryVariable

> 获取url中的参数

| 参数     | 类型   | 默认值    | 是否必填 | 描述               |
| -------- | ------ | --------- | -------- | ------------------ |
| variable | String | undefined | 是       | 要获取url参数的key |

#### 返回值

如果有返回对应的值，没有返回null

#### 代码

```js
/**
 * 获取url参数
 * @param \\{string\\} variable 获取的参数
 */
export function getQueryVariable(variable) \\{
  const query = window.location.search.substring(1);
  const vars = query.split('&');
  for (let i = 0, l = vars.length; i < l; i++) \\{
    const pair = vars[i].split('=');
    if (pair[0] == variable) \\{
      return pair[1];
    \\}
  \\}
  return null;
\\}
```

#### 栗子

```js
import \\{ getQueryVariable \\} from '@js/utils';
getQueryVariable('type') === 'door'
```



### filterEscapeCharacter

> 过滤转义字符，传入的不是字符串类型将返回空字符串

| 参数 | 类型   | 默认值    | 是否必填 | 描述           |
| ---- | ------ | --------- | -------- | -------------- |
| str  | String | undefined | 是       | 要过滤的字符串 |

#### 返回值

过滤之后的字符串

#### 代码

```js
/**
 * 过滤转义字符
 * @param \\{string\\} str
 */
export const filterEscapeCharacter = function(str) \\{
  return typeof str === 'string'
    ? str.replace(/\s|\n|\b|\0|\t|\n|\v|\f|\r/g, '')
    : '';
\\};
```

#### 栗子

```js
import \\{ filterEscapeCharacter \\} from '@js/utils';

filterEscapeCharacter(text.value).length <= 0;
```



### focusInputEndPosition

> 聚焦到input的最后一位

| 参数 | 类型        | 默认值    | 是否必填 | 描述          |
| ---- | ----------- | --------- | -------- | ------------- |
| el   | HTMLElement | undefined | 是       | 要聚焦的input |

#### 返回值

undefined

#### 代码

```js
/**
 * 聚焦到最后一位
 * @param \\{HTMLElement\\} 聚焦的实例
 */
export function focusInputEndPosition(el) \\{
  el.focus();
  const len = el.value.length;
  if (
    typeof el.selectionStart == 'number' &&
    typeof el.selectionEnd == 'number'
  ) \\{
    el.selectionStart = el.selectionEnd = len;
  \\} else if (document.selection) \\{
    const sel = el.createTextRange();
    sel.moveStart('character', len); //设置开头的位置
    sel.collapse();
    sel.select();
  \\}
\\}
```

#### 栗子

```js
focusInputEndPosition(refs.input)
```



### getElementOffsetTop

> 获取当前元素到指定元素的offsetTop  逻辑是从起始element 一直往上找 offsetparent 直到满足停止标识就停下

| 参数      | 类型                                          | 默认值    | 是否必填 | 描述          |
| --------- | --------------------------------------------- | --------- | -------- | ------------- |
| element   | HTMLElement                                   | undefined | 是       | 起始element   |
| className | 停止查找的标识 这个弄个元素作为终止应该更灵活 | undefined | 是       | 终止classname |

#### 返回值

计算出来的高度

#### 代码

```js
/**
 * 获取当前dom到指定父元素的offsetTop
 * @param \\{HTMLElement\\} element 当前dom
 * @param \\{*\\} className 当前dom的某个父元素
 */
export function getElementOffsetTop(element, className) \\{
  let actualTop = element.offsetTop;
  let current = element.offsetParent;

  while (current && !current.className.includes(className)) \\{
    actualTop += current.offsetTop;
    current = current.offsetParent;
  \\}
  return actualTop;
\\}

```

#### 栗子

```js
import \\{ getElementOffsetTop \\} from '@js/utils';
const offsetTop = getElementOffsetTop($item, endClass);

```



### isWin

> 判断是否是windows系统

#### 返回值

是win系统 返回 true 别的false

#### 代码

```js
/**
 * 判断是否是windows系统
 */
export function isWin() \\{
  const platform = window.navigator.platform;
  return ['Win32', 'Windows'].includes(platform);
\\}
```

#### 栗子

```js
import \\{ isWin, asyncAddLink \\} from '@js/utils';

/**
 * 如果是window系统 加载chrome滚动条样式
 */
export default function useScrollBarStyle() \\{
  isWin() && asyncAddLink(\\{ path: '/scrollbar.css' \\});
\\}
```



### asyncAddLink

> 异步加载css样式

| 参数           | 类型   | 默认值    | 是否必填 | 描述         |
| -------------- | ------ | --------- | -------- | ------------ |
| param[0]: path | String | undefined | 是       | 要加载的地址 |

#### 返回值

返回一个promise对象 成功将link标签加入到dom中  resolve 否则reject

#### 代码

```js
/**
 * 异步加载css
 * @param \\{string\\} path url路径
 */
export function asyncAddLink(\\{ path \\}) \\{
  return new Promise((resolve, reject) => \\{
    const head = document.querySelector('head');
    if (head) \\{
      let link = document.createElement('link');
      link.href = path;
      link.rel = 'stylesheet';
      link.type = 'text/css';
      head.appendChild(link);
      link = null;
      resolve();
    \\} else \\{
      reject('not find head');
    \\}
  \\});
\\}
```

#### 栗子

```js
asyncAddLink(\\{ path: '/scrollbar.css' \\});
```



### downloadFileByBlob

> 通过文件流下载文件

| 参数     | 类型             | 默认值       | 是否必填 | 描述           |
| -------- | ---------------- | ------------ | -------- | -------------- |
| blob     | ？？？文件流对象 | undefined    | 是       | 要下载的文件流 |
| filename | String           | undefined    | 是       | 下载的文件名   |
| fileType | String           | 'text/plain' | 否       | blob文件类型   |

#### 返回值

返回一个 promise对象

#### 代码

```js
// 该方法从知识库项目中拿到 做了修改 
export function downloadFileByBlob(blob, filename, fileType = 'text/plain') \\{
 	return new Promise((resolve, reject) => \\{
    const blob = new Blob([blob], \\{
      type: fileType
    \\});
    if(blob.size > 0)\\{
      const url = window.URL.createObjectURL(blob);
      const $a = document.createElement('a');
      $a.style.display = 'none';
      $a.href = url;
      $a.setAttribute('download', filename);
      document.body.appendChild($a);
      $a.click();
      document.body.removeChild($a); // 下载完成移除元素
      window.URL.revokeObjectURL(url); // 释放掉blob对象
      resolve()
    \\}else\\{
      reject(new Error('not found file'))
    \\}
  \\})
\\}
```

#### 栗子

```js
getFile(...).then(res=>\\{
   downloadFileByBlob(res, 'demo.xsl')     
\\})
```



### focusEndPositionBySelection

> 聚焦到最后一位 通用方法 不仅仅是input

| 参数 | 类型        | 默认值    | 是否必填 | 描述            |
| ---- | ----------- | --------- | -------- | --------------- |
| $el  | HTMLElement | undefined | 是       | 要聚焦的dom对象 |

#### 返回值

undefined

#### 代码

```js
/**
 * 聚焦到最后一位
 * @param \\{HTMLElement\\} 聚焦的实例
 */

export function focusEndPositionBySelection($el) \\{
  $el.focus();
  const range = document.createRange();
  range.selectNodeContents($el);
  range.collapse(false);
  const sel = window.getSelection();
  sel.removeAllRanges();
  sel.addRange(range);
\\}
```

#### 栗子

```js
import \\{ focusEndPositionBySelection \\} from '@libs/utils';

focusEndPositionBySelection(refs.textarea);
```



### focusAndSelectAll

> 聚焦并选择全部

| 参数 | 类型        | 默认值    | 是否必填 | 描述                  |
| ---- | ----------- | --------- | -------- | --------------------- |
| el   | HTMLElement | undefined | 是       | 要聚焦和全选的dom对象 |

#### 返回值

undefined

#### 代码

```js
/**
 * 全选
 * @param \\{HTMLElement\\} 聚焦的实例
 */
export function focusAndSelectAll(el) \\{
  el.focus();
  const len = el.value.length;
  if (
    typeof el.selectionStart == 'number' &&
    typeof el.selectionEnd == 'number'
  ) \\{
    el.selectionStart = 0;
    el.selectionEnd = len;
  \\} else if (document.selection) \\{
    const sel = el.createTextRange();
    sel.moveStart('character', 0); //设置开头的位置
    sel.moveEnd('character', len); //设置结束的位置
    sel.collapse();
    sel.select();
  \\}
\\}
```



### getUuid

> 获取uuid

#### 返回值

一个uuid

#### 代码

```js
/**
 * 获取uuid
 */
export function getUuid() \\{
  const s = [];
  const hexDigits = '0123456789abcdef';
  for (let i = 0; i < 36; i++) \\{
    s[i] = hexDigits.substr(Math.floor(Math.random() * 0x10), 1);
  \\}
  // bits 12-15 of the time_hi_and_version field to 0010
  s[14] = '4';
  // bits 6-7 of the clock_seq_hi_and_reserved to 01
  s[19] = hexDigits.substr((s[19] & 0x3) | 0x8, 1);
  s[8] = s[13] = s[18] = s[23] = '-';

  return s.join('');
\\}

```

#### 栗子

```js
const uuid = getUuid()
```
