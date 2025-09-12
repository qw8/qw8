---
title: JavaScript字符串
date: 2020-01-06 21:10:40
categories: 
- 前端知识
tags:
- JavaScript
- 字符串
---

# JavaScript 28个常用字符串方法及使用技巧

原文链接https://juejin.cn/post/7010928535053271077，预计阅读16分钟

今天再来看一些JavaScript基础知识，基础太重要了。还清楚的记得，今年春招的时候，某大厂面试官狠狠的嘲讽我 JavaScript 的API都记不住🤣太尴尬了，主要还是用的太少了，所以平时还是要多用多积累。今天我们就来看看JavaScript中有哪些常用的字符串方法！文章内容较多，建议先收藏再学习！

![JS字符串方法.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d56c8218f0154011855b78607c7bd3e8~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

### 1. 获取字符串长度

JavaScript中的字符串有一个length属性，该属性可以用来获取字符串的长度：

今天再来看一些JavaScript基础知识，基础太重要了。还清楚的记得，今年春招的时候，某大厂面试官狠狠的嘲讽我 JavaScript 的API都记不住🤣太尴尬了，主要还是用的太少了，所以平时还是要多用多积累。今天我们就来看看JavaScript中有哪些常用的字符串方法！文章内容较多，建议先收藏再学习！

![JS字符串方法.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d56c8218f0154011855b78607c7bd3e8~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

### 1. 获取字符串长度

JavaScript中的字符串有一个length属性，该属性可以用来获取字符串的长度：

```javascript
const str = 'hello';
str.length   // 输出结果：5
```

### 2. 获取字符串指定位置的值

charAt()和charCodeAt()方法都可以通过索引来获取指定位置的值：

- charAt() 方法获取到的是指定位置的字符；
- charCodeAt()方法获取的是指定位置字符的Unicode值。

#### （1）charAt()

charAt() 方法可以返回指定位置的字符。其语法如下：

```javascript
string.charAt(index)
```

index表示字符在字符串中的索引值：

```javascript
const str = 'hello';
str.charAt(1)  // 输出结果：e 
```

我们知道，字符串也可以通过索引值来直接获取对应字符，那它和charAt()有什么区别呢？来看例子：

```javascript
const str = 'hello';
str.charAt(1)  // 输出结果：e 
str[1]         // 输出结果：e 
str.charAt(5)  // 输出结果：'' 
str[5]         // 输出结果：undefined
```

可以看到，当index的取值不在str的长度范围内时，str[index]会返回undefined，而charAt(index)会返回空字符串；除此之外，str[index]不兼容ie6-ie8，charAt(index)可以兼容。

#### （2）charCodeAt()

`charCodeAt()`：该方法会返回指定索引位置字符的 Unicode 值，返回值是 0 - 65535 之间的整数，表示给定索引处的 UTF-16 代码单元，如果指定位置没有字符，将返回 **NaN**：

```javascript
let str = "abcdefg";
console.log(str.charCodeAt(1)); // "b" --> 98
```

通过这个方法，可以获取字符串中指定Unicode编码值范围的字符。比如，数字0～9的Unicode编码范围是: 48～57，可以通过这个方法来筛选字符串中的数字，当然如果你更熟悉正则表达式，会更方便。

### 3. 检索字符串是否包含特定序列

这5个方法都可以用来检索一个字符串中是否包含特定的序列。其中前两个方法得到的指定元素的索引值，并且只会返回第一次匹配到的值的位置。后三个方法返回的是布尔值，表示是否匹配到指定的值。

注意：这5个方法都对大小写敏感！

#### （1）indexOf()

`indexOf()`：查找某个字符，**有则返回第一次匹配到的位置**，否则返回-1，其语法如下：

```javascript
string.indexOf(searchvalue,fromindex)
```

该方法有两个参数：

- searchvalue：必需，规定需检索的字符串值；
- fromindex：可选的整数参数，规定在字符串中开始检索的位置。它的合法取值是 0 到 string.length - 1。如省略该，则从字符串的首字符开始检索。

```javascript
let str = "abcdefgabc";
console.log(str.indexOf("a"));   // 输出结果：0
console.log(str.indexOf("z"));   // 输出结果：-1
console.log(str.indexOf("c", 4)) // 输出结果：9
```

#### （2）lastIndexOf()

`lastIndexOf()`：查找某个字符，有则返回最后一次匹配到的位置，否则返回-1

```javascript
let str = "abcabc";
console.log(str.lastIndexOf("a"));  // 输出结果：3
console.log(str.lastIndexOf("z"));  // 输出结果：-1
```

该方法和indexOf()类似，只是查找的顺序不一样，indexOf()是正序查找，lastIndexOf()是逆序查找。

#### （3）includes()

`includes()`：该方法用于判断字符串是否包含指定的子字符串。如果找到匹配的字符串则返回 true，否则返回 false。该方法的语法如下：

```javascript
string.includes(searchvalue, start)
```

该方法有两个参数：

- searchvalue：必需，要查找的字符串；
- start：可选，设置从那个位置开始查找，默认为 0。

```javascript
let str = 'Hello world!';

str.includes('o')  // 输出结果：true
str.includes('z')  // 输出结果：false
str.includes('e', 2)  // 输出结果：false
```

#### （4）startsWith()

`startsWith()`：该方法用于检测字符串**是否以指定的子字符串开始**。如果是以指定的子字符串开头返回 true，否则 false。其语法和上面的includes()方法一样。

```javascript
let str = 'Hello world!';

str.startsWith('Hello') // 输出结果：true
str.startsWith('Helle') // 输出结果：false
str.startsWith('wo', 6) // 输出结果：true
```

#### （5）endsWith()

`endsWith()`：该方法用来判断当前字符串**是否是以指定的子字符串结尾**。如果传入的子字符串在搜索字符串的末尾则返回 true，否则将返回 false。其语法如下：

```javascript
string.endsWith(searchvalue, length)
```

该方法有两个参数：

- searchvalue：必需，要搜索的子字符串；
- length： 设置字符串的长度，默认值为原始字符串长度 string.length。

```javascript
let str = 'Hello world!';

str.endsWith('!')       // 输出结果：true
str.endsWith('llo')     // 输出结果：false
str.endsWith('llo', 5)  // 输出结果：true
```

可以看到，当第二个参数设置为5时，就会从字符串的前5个字符中进行检索，所以会返回true。

### 4. 连接多个字符串

concat() 方法用于连接两个或多个字符串。该方法不会改变原有字符串，会返回连接两个或多个字符串的新字符串。其语法如下：

```javascript
string.concat(string1, string2, ..., stringX)
```

其中参数 string1, string2, ..., stringX 是必须的，他们将被连接为一个字符串的一个或多个字符串对象。

```javascript
let str = "abc";
console.log(str.concat("efg"));          //输出结果："abcefg"
console.log(str.concat("efg","hijk")); //输出结果："abcefghijk"
```

虽然concat()方法是专门用来拼接字符串的，但是在开发中使用最多的还是加操作符+，因为其更加简单。

### 5. 字符串分割成数组

split() 方法用于把一个字符串分割成字符串数组。该方法不会改变原始字符串。其语法如下：

```javascript
string.split(separator,limit)
```

该方法有两个参数：

- separator：必需。字符串或正则表达式，从该参数指定的地方分割 string。
- limit：可选。该参数可指定返回的数组的最大长度。如果设置了该参数，返回的子串不会多于这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。

```javascript
let str = "abcdef";
str.split("c");    // 输出结果：["ab", "def"]
str.split("", 4)   // 输出结果：['a', 'b', 'c', 'd'] 
```

如果把空字符串用作 separator，那么字符串中的每个字符之间都会被分割。

```javascript
str.split("");     // 输出结果：["a", "b", "c", "d", "e", "f"]
```

其实在将字符串分割成数组时，可以同时拆分多个分割符，使用正则表达式即可实现：

```javascript
const list = "apples,bananas;cherries"
const fruits = list.split(/[,;]/)
console.log(fruits);  // 输出结果：["apples", "bananas", "cherries"]
```



### 6. 截取字符串

substr()、substring()和 slice() 方法都可以用来截取字符串。

#### （1） slice()

slice() 方法用于提取字符串的某个部分，并以新的字符串返回被提取的部分。其语法如下：

```javascript
string.slice(start,end)
```

该方法有两个参数：

- start：必须。 要截取的片断的起始下标，第一个字符位置为 0。如果为负数，则从尾部开始截取。
- end：可选。 要截取的片段结尾的下标。若未指定此参数，则要提取的子串包括 start 到原字符串结尾的字符串。如果该参数是负数，那么它规定的是从字符串的尾部开始算起的位置。

上面说了，如果start是负数，则该参数规定的是从字符串的尾部开始算起的位置。也就是说，-1 指字符串的最后一个字符，-2 指倒数第二个字符，以此类推：

```javascript
let str = "abcdefg";
str.slice(1,6);   // 输出结果："bcdef" 
str.slice(1);     // 输出结果："bcdefg" 
str.slice();      // 输出结果："abcdefg" 
str.slice(-2);    // 输出结果："fg"
str.slice(6, 1);  // 输出结果：""
```

注意，该方法返回的子串**包括开始处的字符**，但**不包括结束处的字符**。

#### （2） substr()

substr() 方法用于在字符串中抽取从开始下标开始的指定数目的字符。其语法如下：

```javascript
string.substr(start,length)
```

该方法有两个参数：

- start 必需。要抽取的子串的起始下标。必须是数值。如果是负数，那么该参数声明从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。
- length：可选。子串中的字符数。必须是数值。如果省略了该参数，那么返回从 stringObject 的开始位置到结尾的字串。

```javascript
let str = "abcdefg";
str.substr(1,6); // 输出结果："bcdefg" 
str.substr(1);   // 输出结果："bcdefg" 相当于截取[1,str.length-1]
str.substr();    // 输出结果："abcdefg" 相当于截取[0,str.length-1]
str.substr(-1);  // 输出结果："g"
```

#### （3） substring()

substring() 方法用于提取字符串中介于两个指定下标之间的字符。其语法如下：

```javascript
string.substring(from, to)
```

该方法有两个参数：

- from：必需。一个非负的整数，规定要提取的子串的第一个字符在 string 中的位置。
- to：可选。一个非负的整数，比要提取的子串的最后一个字符在 string 中的位置多 1。如果省略该参数，那么返回的子串会一直到字符串的结尾。

**注意：** 如果参数 from 和 to 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）。如果 from 比 to 大，那么该方法在提取子串之前会先交换这两个参数。并且该方法不接受负的参数，如果参数是个负数，就会返回这个字符串。

```javascript
let str = "abcdefg";
str.substring(1,6); // 输出结果："bcdef" [1,6)
str.substring(1);   // 输出结果："bcdefg" [1,str.length-1]
str.substring();    // 输出结果："abcdefg" [0,str.length-1]
str.substring(6,1); // 输出结果 "bcdef" [1,6)
str.substring(-1);  // 输出结果："abcdefg"
```

注意，该方法返回的子串**包括开始处的字符**，但**不包括结束处的字符**。

```
/**
 * @description 从 'YYYY-MM-DD HH:mm:ss' 格式中提取 'MM-DD HH:mm'
 * @param \\{string\\} dateTimeString - 日期时间字符串
 * @returns \\{string\\} 格式化后的时间
 */
const formatTime = (dateTimeString: string): string => \\{
  if (!dateTimeString) \\{
    return ''
  \\}
  // "2025-10-11 10:30:00" -> "10-11 10:30"
  return dateTimeString.substring(5, 16)
\\}
```



### 7. 字符串大小写转换

toLowerCase() 和 toUpperCase()方法可以用于字符串的大小写转换。

#### （1）toLowerCase()

`toLowerCase()`：该方法用于把字符串转换为小写。

```javascript
let str = "adABDndj";
str.toLowerCase(); // 输出结果："adabdndj"
```

#### （2）toUpperCase()

`toUpperCase()`：该方法用于把字符串转换为大写。

```javascript
let str = "adABDndj";
str.toUpperCase(); // 输出结果："ADABDNDJ"
```

我们可以用这个方法来将字符串中第一个字母变成大写：

```javascript
let word = 'apple'
word = word[0].toUpperCase() + word.substr(1)
console.log(word) // 输出结果："Apple"
```

### 8. 字符串模式匹配

replace()、match()和search()方法可以用来匹配或者替换字符。

#### （1）replace()

`replace()`：该方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。其语法如下：

```javascript
string.replace(searchvalue, newvalue)
```

该方法有两个参数：

- searchvalue：必需。规定子字符串或要替换的模式的 RegExp 对象。如果该值是一个字符串，则将它作为要检索的直接量文本模式，而不是首先被转换为 RegExp 对象。
- newvalue：必需。一个字符串值。规定了替换文本或生成替换文本的函数。

```javascript
let str = "abcdef";
str.replace("c", "z") // 输出结果：abzdef
```

执行一个全局替换, 忽略大小写:

```javascript
let str="Mr Blue has a blue house and a blue car";
str.replace(/blue/gi, "red");    // 输出结果：'Mr red has a red house and a red car'
```

**注意：** 如果 regexp 具有全局标志 g，那么 replace() 方法将替换所有匹配的子串。否则，它只替换第一个匹配子串。

#### （2）match()

`match()`：该方法用于在字符串内检索指定的值，或找到一个或多个正则表达式的匹配。该方法类似 indexOf() 和 lastIndexOf()，但是它返回指定的值，而不是字符串的位置。其语法如下：

```javascript
string.match(regexp)
```

该方法的参数 regexp 是必需的，规定要匹配的模式的 RegExp 对象。如果该参数不是 RegExp 对象，则需要首先把它传递给 RegExp 构造函数，将其转换为 RegExp 对象。

**注意：** 该方法返回存放匹配结果的数组。该数组的内容依赖于 regexp 是否具有全局标志 g。

```javascript
let str = "abcdef";
console.log(str.match("c")) // ["c", index: 2, input: "abcdef", groups: undefined]
```

#### （3）search()

`search()`方法用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串。其语法如下：

```javascript
string.search(searchvalue)
```

该方法的参数 regex 可以是需要在 string 中检索的子串，也可以是需要检索的 RegExp 对象。

**注意：** 要执行忽略大小写的检索，请追加标志 i。该方法不执行全局匹配，它将忽略标志 g，也就是只会返回第一次匹配成功的结果。如果没有找到任何匹配的子串，则返回 -1。

**返回值：** 返回 str 中第一个与 regexp 相匹配的子串的起始位置。

```javascript
let str = "abcdef";
str.search(/bcd/)   // 输出结果：1
```

### 9. 移除字符串收尾空白符

trim()、trimStart()和trimEnd()这三个方法可以用于移除字符串首尾的头尾空白符，空白符包括：空格、制表符 tab、换行符等其他空白符等。

#### （1）trim()

trim() 方法用于移除字符串首尾空白符，该方法不会改变原始字符串：

```javascript
let str = "  abcdef  "
str.trim()    // 输出结果："abcdef"
```

注意，该方法不适用于null、undefined、Number类型。

#### （2）trimStart()

trimStart() 方法的的行为与`trim()`一致，不过会返回一个**从原始字符串的开头删除了空白的新字符串**，不会修改原始字符串：

```javascript
const s = '  abc  ';

s.trimStart()   // "abc  "
```

#### （3）trimEnd()

trimEnd() 方法的的行为与`trim()`一致，不过会返回一个**从原始字符串的结尾删除了空白的新字符串**，不会修改原始字符串：

```javascript
const s = '  abc  ';

s.trimEnd()   // "  abc"
```

### 10. 获取字符串本身

valueOf()和toString()方法都会返回字符串本身的值，感觉用处不大。

#### （1）valueOf()

`valueOf()`：返回某个字符串对象的原始值，该方法通常由 JavaScript 自动进行调用，而不是显式地处于代码中。

```javascript
let str = "abcdef"
console.log(str.valueOf()) // "abcdef"
```

#### （2）toString()

`toString()`：返回字符串对象本身

```javascript
let str = "abcdef"
console.log(str.toString()) // "abcdef"
```

### 11. 重复一个字符串

repeat() 方法返回一个新字符串，表示将原字符串重复n次：

```javascript
'x'.repeat(3)     // 输出结果："xxx"
'hello'.repeat(2) // 输出结果："hellohello"
'na'.repeat(0)    // 输出结果：""
```

如果参数是小数，会向下取整：

```javascript
'na'.repeat(2.9) // 输出结果："nana"
```

如果参数是负数或者Infinity，会报错：

```javascript
'na'.repeat(Infinity)   // RangeError
'na'.repeat(-1)         // RangeError
```

如果参数是 0 到-1 之间的小数，则等同于 0，这是因为会先进行取整运算。0 到-1 之间的小数，取整以后等于-0，repeat视同为 0。

```javascript
'na'.repeat(-0.9)   // 输出结果：""
```

如果参数是NaN，就等同于 0：

```javascript
'na'.repeat(NaN)    // 输出结果：""
```

如果repeat的参数是字符串，则会先转换成数字。

```javascript
'na'.repeat('na')   // 输出结果：""
'na'.repeat('3')    // 输出结果："nanana"
```

### 12. 补齐字符串长度

padStart()和padEnd()方法用于补齐字符串的长度。如果某个字符串不够指定长度，会在头部或尾部补全。

#### （1）padStart()

`padStart()`用于头部补全。该方法有两个参数，其中第一个参数是一个数字，表示字符串补齐之后的长度；第二个参数是用来补全的字符串。

如果原字符串的长度，等于或大于指定的最小长度，则返回原字符串：

```javascript
'x'.padStart(1, 'ab') // 'x'
```

如果用来补全的字符串与原字符串，两者的长度之和超过了指定的最小长度，则会截去超出位数的补全字符串：

```javascript
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'
```

如果省略第二个参数，默认使用空格补全长度：

```javascript
'x'.padStart(4) // '   x'
```

padStart()的常见用途是为数值补全指定位数，笔者最近做的一个需求就是将返回的页数补齐为三位，比如第1页就显示为001，就可以使用该方法来操作：

```javascript
"1".padStart(3, '0')   // 输出结果： '001'
"15".padStart(3, '0')  // 输出结果： '015'
```

#### （2）padEnd()

`padEnd()`用于尾部补全。该方法也是接收两个参数，第一个参数是字符串补全生效的最大长度，第二个参数是用来补全的字符串：

```javascript
'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```

### 13. 字符串转为数字

parseInt()和parseFloat()方法都用于将字符串转为数字。

#### （1）parseInt()

parseInt() 方法用于可解析一个字符串，并返回一个整数。其语法如下：

```javascript
parseInt(string, radix)
```

该方法有两个参数：

- string：必需。要被解析的字符串。
- radix：可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。



当参数 radix 的值为 0，或没有设置该参数时，parseInt() 会根据 string 来判断数字的基数。

```javascript
parseInt("10");			  // 输出结果：10
parseInt("17",8);		  // 输出结果：15 (8+7)
parseInt("010");		  // 输出结果：10 或 8
```

当参数 radix 的值以 “0x” 或 “0X” 开头，将以 16 为基数：

```javascript
parseInt("0x10")      // 输出结果：16
```

如果该参数小于 2 或者大于 36，则 parseInt() 将返回 NaN：

```javascript
parseInt("50", 1)      // 输出结果：NaN
parseInt("50", 40)     // 输出结果：NaN
```

只有字符串中的第一个数字会被返回，当遇到第一个不是数字的字符为止:

```javascript
parseInt("40 4years")   // 输出结果：40
```

如果字符串的第一个字符不能被转换为数字，就会返回 NaN：

```javascript
parseInt("new100")     // 输出结果：NaN
```

字符串开头和结尾的空格是允许的：

```javascript
parseInt("  60  ")    // 输出结果： 60
```

#### （2）parseFloat()

parseFloat() 方法可解析一个字符串，并返回一个浮点数。该方法指定字符串中的首个字符是否是数字。如果是，则对字符串进行解析，直到到达数字的末端为止，然后以数字返回该数字，而不是作为字符串。其语法如下：

```javascript
parseFloat(string)
```

parseFloat 将它的字符串参数解析成为浮点数并返回。如果在解析过程中遇到了正负号（+ 或 -）、数字 (0-9)、小数点，或者科学记数法中的指数（e 或 E）以外的字符，则它会忽略该字符以及之后的所有字符，返回当前已经解析到的浮点数。同时参数字符串首位的空白符会被忽略。

```javascript
parseFloat("10.00")      // 输出结果：10.00
parseFloat("10.01")      // 输出结果：10.01
parseFloat("-10.01")     // 输出结果：-10.01
parseFloat("40.5 years") // 输出结果：40.5
```

如果参数字符串的第一个字符不能被解析成为数字，则 parseFloat 返回 NaN。

```javascript
parseFloat("new40.5")    // 输出结果：NaN
```





# 知识点

### 字符串

- 字符串字面量可以被包围在单引号或双引号中，他可能包含0个或多个字符
- `\`反斜线符号是转义字符
- JS在创建的时候`Unicode`是一个16位的字符集，所以JS中的所有字符都是16位的
- JS没有字符类型，要表示一个字符，只要创建仅包含一个字符的字符串即可 ？？？ **这句话对吗**？？？
- 转义字符允许吧那些正常情况下不被允许的字符插入到字符串中，比如反斜线，引号。。。
- `\u`约定允许指定用数字表示的字符码位

```javascript
"A" === "\u0041"
```

- 字符串有一个`length`属性
- 字符串是不可变的，可以通过+运算符去拼接。
- 一些方法



### 字符串常用操作

- charAt(index):返回指定索引处的字符串
- charCodeAt(index):返回指定索引处的字符的 Unicode 的值
- concat(str1,str2,...):连接多个字符串，返回连接后的字符串的副本
- fromCharCode():将 Unicode 值转换成实际的字符串
- indexOf(str):返回 str 在父串中第一次出现的位置，若没有则返回-1
- lastIndexOf(str):返回 str 在父串中最后一次出现的位置，若没有则返回-1
- match(regex):搜索字符串，并返回正则表达式的所有匹配
- replace(str1,str2):str1 也可以为正则表达式，用 str2 替换 str1
- search(regex):基于正则表达式搜索字符串，并返回第一个匹配的位置
- slice(start,end)：返回字符索引在 start 和 end（不含）之间的子串
- split(sep，limit)：将字符串分割为字符数组，limit 为从头开始执行分割的最大数量
- substr(start，length)：从字符索引 start 的位置开始，返回长度为 length 的子串
- substring(from,to)：返回字符索引在 from 和 to（不含）之间的子串
- toLowerCase()：将字符串转换为小写
- toUpperCase()：将字符串转换为大写
- valueOf()：返回原始字符串值



### 一、非变异方法（不会改变原始字符串）

1.split

把一个字符分割成字符串数组 。非变异方法，不会改变原字符串，所以需创建变量去接收。

```
let array = string.split(separator，howmany)
```

separator 必须，字符串或正则表达式，从该参数指定的位置分割

howmany 可选 分割的长度 默认不考虑长度 ","

```
let str = '123';
let newArr = str.split("") 
console.log(newArr) //[1,2,3]
```

2.substr

在字符串中抽取从start下标开始的指定数目的字符

```
str.substr(start,length)
```

start（必需）：要抽取的字符串起始下标，如果是负数，那么位置从尾部开始

length（可选）：字串中的字符数，必修是数值

```
let str = '123';
let newStr = str.substr(1) 
console.log(newStr) //'23'
```

3.substring

提取字符串中介于两个指定下标之间的字符

```
str.substring(start,stop)
```

start：非负整数，开始下标

stop：结束位置，但比提取的最后字符的位置要多1（比如stop为5，提取的最后一个字符下标为4）

```
let str = '123456';
let newStr = str.substring(1,4) 
console.log(newStr) //'234'
```

4.parseInt

解析一个字符串，返回一个整数

```
let str = '123456';
let newStr = parseInt(str) 
console.log(newStr) //123456
```

5.parseFloat

解析一个字符串，返回一个浮点数

```
let str = '123456.5';
let newStr = parseFloat(str) 
console.log(newStr) //123456.5
```

6.+

将字符串类型转为Number类型

```
const obj=\\{
  a:'12'
\\}

console.log(+obj.a) //12(Number类型)
```

7.replace

可将字符串中特定的内容转为自己想要的

```
replace(regexp/substr,replacement)
```

1.使用字符串匹配

```
let str = "Visit Microsoft!"
let newStr = str.replace("Microsoft", "WSchool")
console.log(newStr) //Visit WSchool!
```

2.使用正则匹配

```
var str = "\\\{\\\{ms\\\}\\\}g}}--\\\{\\\{person.nam\\\}\\\}e}}"

str = str.replace(/\\\{\\\{(.+?)\\\}\\\}/g,(args)=>\\{
    //args: \\\{\\\{ms\\\}\\\}g}}   \\\{\\\{person.nam\\\}\\\}e}}
   return '替换的值'
\\})

console.log(str) //替换的值--替换的值
```



### 二、对字符串的检测

1.indexOf()

可以返回指定字符串值或数字在字符串或数组中首次(第一个)出现的位置，有的话会出现对应的下标，没有的话会返回 -1。

扩展：使用正则

（一）除了使用indexOf查找外，还可以使用match()方法

indexOf返回的是下标；match返回的是指定的值，没有就返回null，区分大小写

实例1：通过match检索字符串 

```
let str = "Hello World";
str.match("Hello") //Hello
str.match("hello") //null

//实例2：通过match检索一个正则匹配
let str = '1 plus 2 equal 3';
let regular = /\d+/g
str.match(regular) //1,2,3
```

（二）也可以通过test()方法，去判断是否存在这个字符串

```
let str = "state1"
//加了^与$标志后代表从开头到结尾都要遵循
let regular = /^state\d$/
regular.test(str) //true 只有state+数字才可匹配成功
```

2.includes()

includes()方法除了检测数组，还可以检测字符串；如果存在返回true，不存在返回false

```
let s = 'Hello world!';
s.includes('o') // true
```

\3. startsWith()

检测字符串是否以指定的子字符串开始，对大小写敏感

```
var str = "Hello world, welcome to the Runoob.";
var n = str.startsWith("Hello");  //true
```



### js字符串的替换方法

```
let text = 'abcdaa'
let text1 = text.replace('a', '5') // 替换第一个
let text2 = text.replace(/a/g, '5') // 全部替换
console.log(text1, text2) // 5bcdaa 5bcd55
```



### 单引号和双引号的区别

* 在js中单引号和双引号没有区别，都可以表示字符或字符串。
* json格式的文件必须使用双引号



### 常用的字符串截取方法

1 取字符串的前i个字符
  str=str.substring(0,i);

2 去掉字符串的前i个字符
  str=str.substring(i); 

3 从右边开始取i个字符
  str=str.substring(str.length()-i); 
  str=str.substring(str.length()-i,str.length()); 

4 从右边开始去掉i个字符
  str=str.substring(0,str.Length-i);

5 从开始截取到中间某个指定字符  midChar (该字符出现的第一次)
  str=str.substring(0,str.indexOf(midChar));

6 从开始截取到指定某段字符串结尾  midStr
  str=str.substring(0,str.indexOf(midStr)+midStr.length());

7 如果字符串中有"abc"则替换成"ABC"
  str=str.replace("abc","ABC");



### toLowerCase和toLocaleLowerCase的区别

ECMAScript中涉及字符串大小写转换的方法有4个：toLowerCase()、toLocaleLowerCase()、toUpperCase()和toLocaleUpperCase()。

其中，toLowerCase()和toUpperCase()是两个经典的方法，借鉴自java.lang.String中的同名方法。

而toLocaleLowerCase()和toLocaleUpperCase()方法则是针对特定地区的实现。

对有些地区来说，针对地区的方法与其通用方法得到的结果相同，但少数语言(如土耳其语言)会为Unicode大小写转换应用特殊的规则，这时候就必须使用针对地区的方法来保证实现正确的转换。

一般来说，在不知道自己的代码将在那种语言环境中运行的情况下，还是使用针对地区的方法更稳妥一些。

以下是几个例子：

####  小写转大写

```
let str1 = "AbCdEf"
str1.toUpperCase()
console.log(str1) // 输出：ABCDEF

let str2 = "hijkl"
str2.toLocaleUpperCase()
console.log(str2) // 输出：HIJKL
```

####  大写转小写

```
let str3 = "AbCdEf"
str3.toLowerCase()
console.log(str3) // 输出：abcdef

let str4 = "HIJKL"
str4.toLocaleLowerCase()
console.log(str4) // 输出：hijkl
```



### 什么是模板字符串？

模板字符串是在 JS 中创建字符串的一种新方法。我们可以通过使用反引号使模板字符串化。

```
//ES5 Version
var greet = 'Hi I\'m Mark';

//ES6 Version
let greet = `Hi I'm Mark`;
```

在 ES5 中我们需要使用一些转义字符来达到多行的效果，在模板字符串不需要这么麻烦：

```
//ES5 Version
var lastWords = '\n'
  + '   I  \n'
  + '   Am  \n'
  + 'Iron Man \n';


//ES6 Version
let lastWords = `
    I
    Am
  Iron Man   
`;
```

在ES5版本中，我们需要添加`\n`以在字符串中添加新行。在模板字符串中，我们不需要这样做。

```
//ES5 Version
function greet(name) \\{
  return 'Hello ' + name + '!';
\\}


//ES6 Version
function greet(name) \\{
  return `Hello $\\{name\\} !`;
\\}
```

在 ES5 版本中，如果需要在字符串中添加表达式或值，则需要使用`+`运算符。在模板字符串s中，我们可以使用`$\\{expr\\}`嵌入一个表达式，这使其比 ES5 版本更整洁。



### 字符串转换成对象

```
var obj = JSON.parse(data);
console.log(JSON.stringify(data.data));
```

说明：
①php中json_encode()转换返回给前端页面时，用“.”读取不到，是因为返回的是字符串格式，就是最外层带了引号的json数据格式，可以用`var obj = JSON.parse(data);`转换成对象，也可以用tp框架中的`$this->ajaxReturn()`;
②另外在vue中，有时候打印对象或者数组时，可能会出现看不懂其数据结构，可以用`console.log(JSON.stringify(data.data));`打印出来，再复制出来，格式化结构。



### 复杂数据类型如何转变为字符串

- 首先，会调用 valueOf 方法，如果方法的返回值是一个基本数据类型，就返回这个值
- 如果调用 valueOf 方法之后的返回值仍旧是一个复杂数据类型，就会调用该对象的 toString 方法
- 如果 toString 方法调用之后的返回值是一个基本数据类型，就返回这个值，
- 如果 toString 方法调用之后的返回值是一个复杂数据类型，就报一个错误。



### JavaScript中如何检测一个变量是一个 String 类型？

答案：三种方法（typeof、constructor、Object.prototype.toString.call()）

解析：

```js
①typeof
typeof('123') === "string" // true
typeof '123' === "string" // true

②constructor
'123'.constructor === String // true

③Object.prototype.toString.call()
Object.prototype.toString.call('123') === '[object String]' // true
```







# 提升代码效率：JavaScript includes()方法在字符串处理中的实战策略

### 引言

JavaScript中 includes() 方法是字符串对象的一个内置方法，旨在提供一种简洁而直观的方式，用于检测一个字符串中是否包含指定的子字符串。以下是对其功能、行为和用法的详细描述：

### 基础语法与参数

includes() 方法执行区分大小写的搜索，以确定是否可以在一个字符串中找到另一个字符串，并根据情况返回 true 或 false。 其基本语法如下：

```
string.includes(searchValue[, fromIndex])
```

searchValue: 必需，要查找的子字符串。
fromIndex: 可选，整数，表示开始查找的位置。默认值为 0，即从字符串的起始位置开始查找。

该方法返回一个布尔值：

true: 如果 searchValue 存在于原字符串中。
false: 如果 searchValue 不存在于原字符串中。

#### 使用场景

1. 用户输入验证：检查用户提交的表单数据（如用户名、邮箱地址、密码等）是否包含特定字符或短语，以满足格式要求或防止恶意输入。

```
function isValidUsername(username) \\{
  return username.includes("@") && username.includes(".");
\\}

const email = "user@example.com";
console.log(isValidUsername(email)); // true
```

2. 内容过滤：在处理文本内容时，检测是否包含敏感词、非法字符或特定关键词，以进行内容审核、自动标记或过滤。

```
function containsProfanity(text) \\{
  const profanities = ["swearword1", "swearword2", "etc."];
  return profanities.some(word => text.includes(word));
\\}

const message = "This message contains a swearword!";
console.log(containsProfanity(message)); // true
```

3. 路径处理：在URL、文件路径或目录结构中，检查是否包含特定路径片段、文件扩展名等。

```
function isImageFile(path) \\{
  return path.endsWith(".jpg") || path.endsWith(".png") || path.includes(".jpeg");
\\}

const imagePath = "/images/example.jpg";
console.log(isImageFile(imagePath)); // true
```

4. 数据清洗：清理文本数据，移除或替换包含特定字符或模式的字符串部分。

```
function removeInvalidChars(input) \\{
  const invalidChars = ["\\", "/", "*", "?", "<", ">", "|"];
  for (const char of invalidChars) \\{
    while (input.includes(char)) \\{
      input = input.replace(char, "");
    \\}
  \\}
  return input;
\\}

const dirtyData = "Unsafe*Characters\\In?Here>";
const cleanedData = removeInvalidChars(dirtyData);
console.log(cleanedData); // "UnsafeCharactersInHere"
```

### 实战技巧

1. 不区分大小写查找：虽然 includes() 默认区分大小写，但可以通过将字符串和查找值转换为统一的大小写形式（通常为全小写或全大写）来实现不区分大小写的查找。

```
const str = "Hello, World!";
const searchValue = "world";

if (str.toLowerCase().includes(searchValue.toLowerCase())) \\{
  console.log(`$\\{searchValue\\} is found (case-insensitive).`);
\\}
```

2. 从指定位置开始查找：虽然 includes() 本身不支持从指定索引开始查找，但可以通过截取子字符串实现类似效果。

```
const str = "Hello, world! How are you?";
const searchFromIndex = 7;
const searchValue = "world";

if (str.slice(searchFromIndex).includes(searchValue)) \\{
  console.log(`$\\{searchValue\\} is found after index $\\{searchFromIndex\\}.`);
\\}
```

3. 组合使用其他字符串方法：与其他字符串方法（如 trim(), split(), substring(), replace() 等）配合，可以实现更复杂的文本处理逻辑。

```
const sentence = "A quick brown fox jumps over the lazy dog.";
const wordToFind = "fox";

const words = sentence.split(' ');
const isWordPresent = words.some(word => word.includes(wordToFind));

console.log(`The word "$\\{wordToFind\\}" is $\\{isWordPresent ? 'present' : 'absent'\\} in the sentence.`);
```

4.空字符串检查：includes() 认为空字符串是任何字符串（包括空字符串自身）的有效子字符串，因此对空字符串的检查总是返回 true。在检查字符串是否为空时，直接使用 str.length === 0 更为直观。

```
const str = "";
console.log(str.includes("")); // true
```

5.类型安全：虽然 includes() 会尝试将非字符串参数转换为字符串，但在编写代码时，最好确保传入的 searchValue 是预期的字符串类型，以避免潜在的类型转换问题和意外行为。

6.多位置匹配：includes() 只需找到子字符串在一个字符串中的任意位置即可返回 true，它不会返回所有匹配的位置。如果你需要找出所有匹配位置，应使用正则表达式与 match() 或 exec() 方法结合。

7.替代 indexOf() 方法：includes() 方法是对传统 indexOf() 方法的一种更简洁、易读的替代。两者都能检测子字符串是否存在，但 indexOf() 返回的是子字符串的索引（如果存在）或 -1（不存在），而 includes() 直接返回布尔值。在只需要知道是否包含而不关心具体位置的情况下，includes() 更为直接。

### 写在最后

综上所述，includes() 方法在JavaScript字符串处理中具有广泛的应用，无论是简单的包含性检查，还是更复杂的文本分析与处理场景，都能提供简洁高效的解决方案。熟练运用上述技巧，可以帮助你更好地利用 includes() 实现各种字符串相关的任务。

原文链接：https://blog.csdn.net/lg15839654949/article/details/137139114