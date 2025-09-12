---
title: TypeScript
date: 2019-10-12 19:25:55
categories: 
- 前端知识
tags:
- TypeScript
---

### 什么是Typescript？

Typescript是**强类型的Javascript超集**，支持ES6语法，支持面向对象编程的概念，如类、接口、继承、泛型等。Typescript并不直接在浏览器上运行，需要编译器编译成纯Javascript来运行。



### 说说Typescripy和Javascript的区别？

![img](https:////upload-images.jianshu.io/upload_images/16021827-9f2935d0f3da0cf7.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

### 说说Typescript的优缺点？

**优点：**

1：快速简单，易于学习。

2：编译时提供错误检查， 在代码运行前就会进行错误提示。

3：支持所有的JS库。

4：支持ES6，提供了ES6所有优点和更高的生产力。

5：使用继承提供可重用性。

6：有助于代码结构。

7：通过定义模块来定义命名空间。

**缺点：**

1：需要长时间的来编译代码。

2：在使用第三方库时，需要有三方库的定义文件，并不是所有三方库都提供了定义文件，提供的定义文件是否准确也值得商榷。



### Typescript有哪些基础类型？

1：number

2：string

3：boolean

4：Symbol

5：Array

6：Tuple(元组)

7：enum(枚举)

8：object

9：never

表示那些永不存在的值类型。如总是抛出异常或者根本不会有返回值的函数的返回值类型。

10：void

与any相反表示没有任何类型。函数没有返回值时用void。

11：null和undefined

它们是所有类型的子类型。当你指定structNullChecks时，它们只能赋值给void或者它们自己本身。

12：any



## TS所有常用知识点

TypeScript 是 JavaScript 的超集，通过静态类型检查和丰富的类型系统增强了代码的可维护性。以下是 TypeScript 的核心知识点和常用特性，结合代码示例详细说明：

------

### 一、基础类型

TypeScript 内置基础类型，提供明确的类型注解。

```typescript
let isDone: boolean = false;    // 布尔
let count: number = 42;         // 数字
let name: string = "Alice";     // 字符串
let list: number[] = [1, 2, 3]; // 数组
let tuple: [string, number] = ["Alice", 30]; // 元组
enum Color \\{ Red, Green = 2 \\}; // 枚举
let notSure: any = 4;          // 任意类型（慎用）
let u: undefined = undefined; // undefined
let n: null = null;           // null
function warn(): void \\{ console.log("Warning!"); \\} // 无返回值
```

------

### 二、类型推断与联合类型

TypeScript 能自动推断类型，也支持联合类型。

```typescript
let inferred = "hello"; // 类型推断为 string
let union: string | number; // 联合类型
union = "text";  // OK
union = 100;     // OK
```

------

### 三、接口（Interface）

定义对象结构、函数类型或类的契约。

```typescript
// 对象接口
interface User \\{
  name: string;
  age?: number;   // 可选属性
  readonly id: number; // 只读属性
\\}

// 函数接口
interface SearchFunc \\{
  (source: string, keyword: string): boolean;
\\}

// 类接口
interface ClockInterface \\{
  currentTime: Date;
  setTime(d: Date): void;
\\}
```

------

### 四、类（Class）

TypeScript 支持 ES6 类语法，并扩展了访问修饰符。

```typescript
class Animal \\{
  private name: string; // 私有属性
  constructor(name: string) \\{ this.name = name; \\}
  public move(distance: number = 0) \\{
    console.log(`$\\{this.name\\} moved $\\{distance\\}m.`);
  \\}
\\}

class Dog extends Animal \\{
  constructor(name: string) \\{ super(name); \\}
  bark() \\{ console.log("Woof!"); \\}
\\}

// 抽象类
abstract class Shape \\{
  abstract getArea(): number; // 抽象方法
\\}
```

------

### 五、泛型（Generics）

提供类型参数化，增强代码复用性。

```typescript
function identity<T>(arg: T): T \\{ return arg; \\}
identity<string>("hello"); // 显式指定类型
identity(42);              // 类型推断为 number

// 泛型接口
interface GenericArray<T> \\{
  [index: number]: T;
\\}
let arr: GenericArray<number> = [1, 2, 3];
```

------

### 六、高级类型

#### 1. 交叉类型（Intersection Types）

```typescript
type Admin = \\{ name: string; privileges: string[] \\};
type Employee = \\{ name: string; startDate: Date \\};
type AdminEmployee = Admin & Employee; // 合并类型
```

#### 2. 类型别名（Type Aliases）

```typescript
type StringOrNumber = string | number;
type Callback = (data: string) => void;
```

#### 3. 索引类型（Index Types）

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K) \\{
  return obj[key];
\\}
```

#### 4. 映射类型（Mapped Types）

```typescript
type Readonly<T> = \\{ readonly [P in keyof T]: T[P] \\};
type Partial<T> = \\{ [P in keyof T]?: T[P] \\};
```

#### 5. 条件类型（Conditional Types）

```typescript
type IsString<T> = T extends string ? true : false;
type A = IsString<"hello">; // true
```

------

### 七、类型守卫与类型断言

#### 1. 类型守卫（Type Guards）

```typescript
function isString(value: any): value is string \\{
  return typeof value === "string";
\\}

if (isString(input)) \\{
  console.log(input.toUpperCase()); // 类型被缩小为 string
\\}
```

#### 2. 类型断言

```typescript
let value: any = "hello";
let strLength: number = (value as string).length; // 方式1
let strLength2: number = (<string>value).length; // 方式2（JSX 中不可用）
```

------

### 八、模块与命名空间

#### 1. 模块（ES Modules）

```typescript
// math.ts
export function add(a: number, b: number): number \\{ return a + b; \\}

// app.ts
import \\{ add \\} from "./math";
console.log(add(2, 3));
```

#### 2. 命名空间（Namespace）

```typescript
namespace MyMath \\{
  export function add(a: number, b: number) \\{ return a + b; \\}
\\}
console.log(MyMath.add(1, 2));
```

------

### 九、配置（tsconfig.json）

关键配置项：

```json
\\{
  "compilerOptions": \\{
    "target": "ES6",          // 编译目标版本
    "module": "CommonJS",     // 模块系统
    "strict": true,           // 启用严格类型检查
    "outDir": "./dist",       // 输出目录
    "esModuleInterop": true   // 改善模块兼容性
  \\},
  "include": ["src/**/*.ts"]
\\}
```

------

### 十、工具类型（Utility Types）

TypeScript 内置常用工具类型：

```typescript
type PartialUser = Partial<User>;           // 所有属性变为可选
type RequiredUser = Required<User>;         // 所有属性变为必选
type ReadonlyUser = Readonly<User>;         // 所有属性变为只读
type UserRecord = Record<"id" | "name", string>; // 定义键值类型
type UserPick = Pick<User, "name" | "age">; // 选择属性
type UserOmit = Omit<User, "id">;           // 排除属性
```

------

### 十一、装饰器（Decorators）

实验性功能，需在 `tsconfig.json` 中启用：

```json
\\{
  "compilerOptions": \\{
    "experimentalDecorators": true
  \\}
\\}
```

示例：

```typescript
function log(target: any, key: string, descriptor: PropertyDescriptor) \\{
  const originalMethod = descriptor.value;
  descriptor.value = function (...args: any[]) \\{
    console.log(`Calling $\\{key\\} with args: $\\{args\\}`);
    return originalMethod.apply(this, args);
  \\};
\\}

class Calculator \\{
  @log
  add(a: number, b: number) \\{ return a + b; \\}
\\}
```

------

### 十二、声明合并（Declaration Merging）

允许合并同名的接口、类或命名空间：

```typescript
interface User \\{ name: string; \\}
interface User \\{ age: number; \\}
const user: User = \\{ name: "Alice", age: 30 \\}; // 合并后的接口
```

------

### 十三、Mixins 模式

通过组合多个类的行为实现复用：

```typescript
type Constructor<T = \\{\\}> = new (...args: any[]) => T;

function Timestamped<TBase extends Constructor>(Base: TBase) \\{
  return class extends Base \\{
    timestamp = Date.now();
  \\};
\\}

const UserWithTimestamp = Timestamped(User);
const user = new UserWithTimestamp();
```

------

### 十四、实践示例：React 组件

TypeScript 与 React 结合：

```typescript
interface Props \\{
  title: string;
  count: number;
\\}

const Counter: React.FC<Props> = (\\{ title, count \\}) => \\{
  return (
    <div>
      <h1>\\{title\\}</h1>
      <p>Count: \\{count\\}</p>
    </div>
  );
\\};
```

------

### 十五、常见问题

1. **类型推断错误**：使用 `as` 或类型守卫明确类型。
2. **第三方库无类型定义**：安装 `@types/库名` 或手动声明类型。
3. **泛型约束**：使用 `extends` 限制泛型参数范围。

------

通过掌握以上知识点，您能更高效地使用 TypeScript 构建健壮的前端应用。建议结合官方文档（TypeScript Handbook）深入学习。







### 如何编译Typescript?

tsc xxx.ts



### 如何将多个ts文件合并成一个js文件？

tsc --outfile compact.js file1.ts file2.ts file3.js



### 如何自动编译ts文件并实时修改？

tsc --watch file.ts



### typescript 遇到过什么坑

main.ts 报错（ Cannot find module './App.vue'.）

原因： typescript 不能识别.vue 文件

解决办法： 引入 vue 的 typescript declare 库



### 什么是TS接口？说说它有哪些特性？

TS的核心原则之一就是**对值所具有的结构进行类型检查**。

它有时被称为“鸭式辩型法”或“结构性子类型化”。

其作用就是为这些类型进行命名，或为你的代码或者三方代码定义契约。

**特点：**

1：定义对象、数组、函数、类等。

2：接口可以相互继承

3：接口可以继承类

4：可选属性与额外检查

![img](https:////upload-images.jianshu.io/upload_images/16021827-bb884c0a4ffaf55d.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/960/format/webp)



### 如何理解Typescript中的类？并说说它有什么特性？

Typescript是一种面向对象的Javascript语言，和其他任何面向对象编程的强语言一样，**类是描述某一组对象共有属性状态或行为的实体**。它就是构建具体对象实例的模板和蓝图。

**特性：**

1：继承

2：多态

3：抽象

4：封装

5：实例



### Typescript支持哪些面向对象术语？

1：类

2：继承

3：多态

4：抽象

5：泛化

6：接口封装

7：实例化

等等...



### 如何调用基类中的构造函数？

super()



### 如何实现类的继承？

extends



### Typescript中的模块是什么？

Typescript1.5后为了与ES6术语保持一致，内部模块都称为**命名空间**，外部模块简称**模块**。

模块在自身的作用域里执行，并不是全局作用域。这就意味着模块类的类、函数、对象等对外都是不可见的。除非你通过export导出，import导入。

模块通过使用模块加载器导入另一个模块。在运行时，模块加载器负责在执行模块之前定位和执行模块的所有依赖项。JavaScript中最常用的模块加载器是用于Node.js的CommonJS模块加载器和用于Web应用程序的require.js模块加载器。

**特别说明：**

为了支持CommonJS和AMD语法中的exports，TS提供了export = 语法，引入方式为import xxx = require("xxx")；



### 解释下Typescript的装饰器是什么？

装饰器是一种特殊类型的声明，它能被附加在类、方法、属性、访问符、参数上。

装饰器使用@expression这种方式，expression求值后必须为一个函数，它在运行时调用，被装饰器声明的信息作为参数传入。



### 什么是Mixins?

一种通过重用组件构建类的方法。

不通过类的直接继承来实现，而是将基类作为接口来实现。对于基类实例化部分在子类中实现，基类中原型的部分在子类中进行声明占位，然后通过一个Minxin函数将基类上的原型属性拷贝到子类上。



### TSD是什么？

TSD是Typescript的包管理工具，我们都知道在.ts文件中引入第三方库时，第三库是需要.d.ts声明文件的，否则三方库在.ts中是无法识别报错的。

TSD就是帮我查找对应的三方库TS声明文件并下载安装。

使用过程如下：

1：npm install tsd -g

2: tsd init

3: tsd query xxx三方库 --action install

4：在使用的.ts文件中通过reference指向该声明文件

/// <reference path="typings/jquery/jquery.d.ts" />



### Declare关键字是干嘛用的？

我们在.ts中使用的第三方库时没有.d.ts声明文件的时候，我们可以通过declare来写申明文件。

可以声明该模块，甚至可以直接声明一个值为any的同名的变量，然后我们就可以在代码中直接使用该三方库了。



### 如何让.ts文件自动生成对应的.d.ts声明文件？

tsc --declaration test.ts



### tsconfig.json文件有什么作用？

该文件存在于Typescript项目的根目录里，其作用是指定相关选项告诉ts编译器如何编译ts文件。



### 说说什么Typescript中的泛型？作用是什么？

泛型代表的是泛指某一类型，更像是一个类型变量。由尖括号包裹<T>。

主要作用是**创建逻辑可复用的组件**。

泛型可以作用在函数、类、接口上。

函数：

function greet<T>(name: T) \\{\\}

类：

```
class createObj<T> \\{
  name: T
\\}
```

接口：

```
interface IF<T> \\{
  name: T
\\}
```

泛型还可以被约束，这样就是任意类型了。

```
interface TIF \\{
  length: number
\\}

function test<T extends TIF>(params: T) \\{
  console.log("=========>>>", params.length);
\\}
```

泛型约束之类型参数

```
function getPropoty<T, K extends keyof T>(obj: T, key: K) \\{
  return obj[key];
\\}
```



### 说说接口和类型别名type的区别？

他们很相似，type可以作用于原始值，联合类型，元组以及其它任何你需要手写的类型。

区别一：它并不会真的创建一个新的名字，当你在编译器上将鼠标悬停在定义为该类型别名定义的变量上时返回的是该类型别名引用的对象。相反，接口会创建一个新名字 ，当你把鼠标悬停在该接口定义的变量上时返回的是该接口名。

区别二：类型别名不能extends和implements

区别三：对于元组，联合类型我们一般使用类型别名type。



### 什么是Typescript映射文件？

.map源映射文件

它是编译后的.js与源文件之间的映射文件。调试器使用该文件，使我们可以直接调试Typescript文件而不是编译后的JS文件。



### 什么是类型断言？

类型断言对运行没有什么影响，仅供编译器使用。

向编译器提供我们所希望的分析代码的提示。

表示断言的两种方式：

1：<类型>变量

2：变量 as 类型 （在tsx中只能使用这种方式）



### 什么是Rest参数？

在不使用arguments对象的情况允许我们的函数传递可变数量的参数的另一种实现方式。

表示方式是...params。

**rest参数的规则是：**

1：一个函数只能有一个rest参数。

2：它只能出现在参数列表的最后一个。

3：该参数必须是数组类型。



### 什么是枚举？

枚举可以使我们定义一些带名字的常量，用于清晰的表达意图和创建一组有区别的用例。

枚举主要分为两类。一类是基于数字的，有自增长和反向映射的特性。一类是基于字符串的。

当然还有混合了这两种基础类型的枚举，我们叫做异构枚举。



### 说说TS的模块解析策略，什么是相对导入？什么是非相对导入？

![img](https:////upload-images.jianshu.io/upload_images/16021827-a213202c03d84f74.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

![img](https:////upload-images.jianshu.io/upload_images/16021827-d7eb37c8503111ee.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

可以通过moduleResolution属性来设置解析模式。



### 什么是声明合并？

声明合并是编译器将2个或多个同名声明合并为一个，合并后的声明拥有被合并声明的所有特性。

目前除了类不能与其他类和变量合并外，其他声明都是可以相互合并的。



### 什么是Typescript?

TypeScript是一种由微软开发和维护的免费开源编程语言。它是一个强类型的JavaScript超集，可编译为纯JavaScript。它是一种用于应用级JavaScript开发的语言。对于熟悉c#、Java和所有强类型语言的开发人员来说，TypeScript非常容易学习和使用。

TypeScript可以在任何浏览器、主机和操作系统上执行。TypeScript不是直接在浏览器上运行的。它需要一个编译器来编译和生成JavaScript文件。TypeScript是带有一些附加特性的ES6 JavaScript版本。



### TypeScript和JavaScript有什么不同？

TypeScript与JavaScript的区别如下:

| **编号** | **JavaScript**                                     | **TypeScript**                                          |
| -------- | -------------------------------------------------- | ------------------------------------------------------- |
| 1        | 它是由网景公司在1995年开发的。                     | 它是2012年由安德斯·海尔斯伯格(Anders Hejlsberg)开发的。 |
| 2        | JavaScript源文件在”。js”扩展。                     | TypeScript源文件是”.ts”扩展名。                         |
| 3        | JavaScript不支持ES6。                              | TypeScript 支持ES6。                                    |
| 4        | 它不支持强类型或静态类型。                         | 它支持强类型或静态类型特性。                            |
| 5        | 它只是一种脚本语言。                               | 它支持面向对象的编程概念，如类、接口、继承、泛型等。    |
| 6        | JavaScript没有可选的参数特性。                     | TypeScript有可选的参数特性。                            |
| 7        | 它是解释语言，这就是为什么它在运行时突出显示错误。 | 它编译代码并在开发期间突出显示错误。                    |
| 8        | JavaScript不支持模块。                             | TypeScript支持模块。                                    |
| 9        | 在这里，number和string是对象。                     | 在这里，number和string是接口。                          |
| 10       | JavaScript不支持泛型。                             | TypeScript支持泛型。                                    |



### 我们为什么需要TypeScript？

我们需要TypeScript:

- TypeScript快速、简单，最重要的是，容易学习。
- TypeScript支持面向对象的编程特性，比如类、接口、继承、泛型等等。
- TypeScript在编译时提供了错误检查功能。它将编译代码，如果发现任何错误，它将在运行脚本之前突出显示这些错误。
- TypeScript支持所有JavaScript库，因为它是JavaScript的超集。
- TypeScript通过使用继承来支持可重用性。
- TypeScript使应用程序开发尽可能的快速和简单，并且TypeScript的工具支持为我们提供了自动完成、类型检查和源文档。
- TypeScript支持最新的JavaScript特性，包括ECMAScript 2015。
- TypeScript提供了ES6的所有优点和更高的生产力。
- TypeScript支持静态类型、强类型、模块、可选参数等。



### 列出Typescript的一些特性

![Typescript的一些特性](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5zcmNtaW5pLmNvbS93cC1jb250ZW50L3VwbG9hZHMvMjAxOS8xMi80ZTg4NzNhMjkyZTQ5OGUucG5n?x-oss-process=image/format,png)

 

### 列出使用Typescript的一些优点?

TypeScript有以下优点。

- 它提供了可选静态类型的优点。在这里，Typescript提供了可以添加到变量、函数、属性等的类型。
- Typescript能够编译出一个能在所有浏览器上运行的JavaScript版本。
- TypeScript总是在编译时强调错误，而JavaScript在运行时指出错误。
- TypeScript支持强类型或静态类型，而这不是在JavaScript中。
- 它有助于代码结构。
- 它使用基于类的面向对象编程。
- 它提供了优秀的工具支持和智能感知，后者在添加代码时提供活动提示。
- 它通过定义模块来定义名称空间概念。



### Typescript的缺点是什么?

TypeScript有以下缺点:

- TypeScript需要很长时间来编译代码。
- TypeScript不支持抽象类。
- 如果我们在浏览器中运行TypeScript应用程序，需要一个编译步骤将TypeScript转换成JavaScript。
- Web开发人员使用了几十年的JavaScript，而TypeScript不是都是新东西。
- 要使用任何第三方库，必须使用定义文件。并不是所有第三方库都有可用的定义文件。
- 类型定义文件的质量是一个问题，即如何确保定义是正确的?



### TypeScript的不同组件是什么?

TypeScript主要有三个组件。这些都是- –

![TypeScript所有组件](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5zcmNtaW5pLmNvbS93cC1jb250ZW50L3VwbG9hZHMvMjAxOS8xMi8wYzdlODA2MzFjMDQxNTYucG5n?x-oss-process=image/format,png)

#### 语言language

该语言由新语法、关键字、类型注释等元素组成，允许我们编写TypeScript。

#### 编译器compiler

TypeScript编译器是开源的、跨平台的，是用TypeScript编写的。它将用TypeScript编写的代码转换为JavaScript代码。它执行从TypeScript代码到JavaScript代码的解析和类型检查。它还可以帮助将不同的文件连接到单个输出文件，并生成源映射。

#### 语言服务language service

语言服务提供信息，帮助编辑器和其他工具提供更好的辅助功能，如自动重构和智能感知。



### Typescript是谁开发的，目前稳定的Typescript版本是什么？

typescript是由Anders Hejlsberg开发的，他也是c#语言开发团队的核心成员之一。typescript于2012年10月1日发布，被标记为0.8版。它是由Microsoft在Apache 2许可下开发和维护的。它是为开发大型应用程序而设计的。

目前稳定的TypeScript版本是3.2，于2018年9月30日发布。Typescript编译成简单的JavaScript代码，可以在任何支持ECMAScript 2015框架的浏览器上运行。它支持最新的和不断发展的JavaScript特性。

 

### 说说安装Typescript的最低要求。或者我们如何获得TypeScript并安装它？

TypeScript可以通过npm (node .js包管理器)在node的帮助下进行安装和管理。要安装TypeScript，首先要确保npm安装正确，然后运行以下命令在系统上全局安装TypeScript。

```
$ npm install -g typescript  
```

它安装一个命令行代码“tsc”，它将进一步用于编译我们的Typescript代码。确保检查系统上安装的Typescript版本。

安装TypeScript需要以下步骤:

- 下载并运行节点的.msi安装程序。
- 输入命令“node -v”检查安装是否成功。
- 在终端窗口中输入以下命令安装Typescript: $ npm install -g Typescript



### 列出在Typescript中的内置类型

在Typescript中，内置的数据类型也称为原始数据类型。这些数据如下所示。

![typescript内置数据类型02](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5zcmNtaW5pLmNvbS93cC1jb250ZW50L3VwbG9hZHMvMjAxOS8xMi8xNWI4MjI2MGI0YzdkZDQucG5n?x-oss-process=image/format,png)

**数字类型**: 用于表示数字类型值。TypeScript中的所有数字都存储为浮点值。

**语法**: let标识符:number = value;

**字符串类型**: 它表示存储为Unicode UTF-16代码的字符序列。我们通过将字符串括在单引号或双引号中来在脚本中包含字符串。

**语法**: let标识符:字符串= ” “;

**布尔类型**: 用于表示逻辑值。当我们使用布尔类型时，我们只得到真或假的输出。布尔值是一个真值，它指定条件是否为真。

**语法**: let标识符:bool =布尔值;

**Null类型**: Null表示值未定义的变量。不能直接引用空类型值本身。空类型没有用处，因为我们只能为它分配一个空值。

**语法**: let num: number = null;

**未定义类型**: 它是未定义字面量的类型。未定义的类型表示所有未初始化的变量。它是没有用的，因为我们只能分配一个未定义的值给它。这种内置类型是所有类型的子类型。

**语法**: let num: number =未定义;

**Void类型**: Void是不返回任何类型值的函数的返回类型。如果没有可用的数据类型，则使用它。

**语法**: let unusable:void =未定义;



### Typescript中的变量是什么？如何在Typescript中创建变量？

变量是存储位置，用于存储要被程序引用和使用的值/信息。它充当程序中值的容器。可以使用var关键字声明它。它应该在使用前声明。在Typescript中声明变量时，应该遵循某些规则-

- 变量名必须是字母或数字。
- 变量名不能以数字开头。
- 变量名不能包含空格和特殊字符，除了下划线(_)和美元($)符号。

我们可以通过以下四种方式之一声明一个变量:

- 在一条语句中声明类型和值。语法:var [identifier]: [type-annotation] = value;
- 声明没有值的类型。语法:var [identifier]: [type-annotation];
- 在没有类型的情况下声明它的值。语法:var [identifier] = value;
- 声明没有值和类型。语法:var(标识符);



### 如何编译Typescript文件？

下面是将Typescript文件编译成JavaScript时所遵循的命令。

```
$ tsc <TypeScript File Name>  
```

例如，编译“hello .ts”。

```
$ tsc helloworld.ts  
```

结果是helloworld.js。



### 是否可以将多个.ts文件合并成一个.js文件？如果是，那么如何做？

是的，有可能。为此，我们需要添加——outFILE [OutputJSFileName]编译选项。

```
$ tsc --outFile comman.js file1.ts file2.ts file3.ts  
```

上面的命令将编译所有这三个.ts文件和结果将存储在一个comman.js文件中，在这种情况下，当我们不提供输出文件名像下面的命令。

```
$ tsc --outFile file1.ts file2.ts file3.ts  
```

然后file2.ts和file3.ts将被编译，并将输出放在file1.ts中，现在是file1.ts包含JavaScript代码。



### 能否自动编译.ts文件，并实时修改.ts文件？

这是可以的，自动实时根据.ts文件变化自动编译.ts文件是可以的。这可以通过使用——watch compiler选项来实现

```
tsc --watch file1.ts  
```

上面的命令首先编译file1为file1.js，并注意文件的变化，如果检测到任何更改，它将再次编译文件。这里，我们需要确保在使用——watch选项运行时命令提示符不能关闭。



### TS的接口是什么意思？参照TS来解释它们。

接口是在我们的应用程序中充当契约的结构。它定义了要遵循的类的语法，这意味着实现接口的类必须实现它的所有成员。它不能被实例化，但是可以被实现它的类对象引用。无论对象是否具有特定的结构，TypeScript编译器都使用接口进行类型检查(也称为“duck typing”鸭子类型或“结构化子类型”)。

语法:

```
interface interface_name \\{    
          // 字段声明

          // 方法声明
\\}    
```

接口只是声明方法和字段，它不能用来建造任何东西。不需要将接口转换为JavaScript来执行，它们对运行时JavaScript没有任何影响。因此，它们的唯一目的是在开发阶段提供帮助。



### 你如何理解Typescript中的类？列出类的一些特性。

我们知道，TypeScript是一种面向对象的JavaScript语言，支持OOP编程特性，比如类、接口等。与Java一样，类是用于创建可重用组件的基本实体。它是一组具有公共属性的对象。类是创建对象的模板或蓝图。它是一个逻辑实体。“class”关键字用于在Typescript中声明一个类。

例子:

```
class Student \\{    
    studCode: number;    
    studName: string;    
    constructor(code: number, name: string) \\{    
            this.studName = name;    
            this.studCode = code;    
    \\}    

    getGrade() : string \\{    
        return "A+" ;    
    \\}    
\\}    
```

类的特征是-

- 继承
- 封装
- 多态性
- 抽象



### 本地Javascript支持模块吗？

不。目前，本地JavaScript不支持模块。为了在Javascript中创建和使用模块，我们需要一个像CommonJS这样的外部模块。



### TypeScript支持哪些面向对象的术语？

TypeScript支持以下面向对象的术语。

- 模块
- 类
- 接口
- 继承
- 数据类型
- 成员函数



### 如何从TypeScript的子类调用基类构造函数？

super()函数的作用是: 从子类中调用父类或基类构造函数。



### 如何在TypeScript中实现继承？

继承是一种从另一个类获取一个类的属性和行为的机制。它是OOPs语言的一个重要方面，并且具有从现有类创建新类的能力，继承成员的类称为基类，继承这些成员的类称为派生类。

继承可以通过使用extend关键字来实现。我们可以通过下面的例子来理解它。

```
class Shape \\{     
   Area:number     
   constructor(area:number) \\{     
      this.Area = area    
   \\}     
\\}     

class Circle extends Shape \\{     
   display():void \\{     
      console.log("圆的面积: "+this.Area)     
   \\}     
\\}    

var obj = new Circle(320);     

obj.display()  
```



### Typescript中的模块是什么？

模块是创建一组相关变量、函数、类和接口等的强大方法。它可以在它们自己的范围内执行，而不是在全局范围内。换句话说，在模块中声明的变量、函数、类和接口不能在模块外部直接访问。

**创建一个模块**

可以使用export关键字创建模块，也可以在其他模块中使用import关键字。

```
module module_name\\{  
    class xyz\\{  
        export sum(x, y)\\{  
            return x+y;  
         \\}  
    \\}  
\\}  
```



### 内部模块和外部模块有什么区别？

内部模块与外部模块的区别如下:

| **编号** | 内部模块                                                     | 外部模块                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1        | 内部模块用于将类、接口、函数和变量逻辑地分组到一个单元中，并可以导出到另一个模块中。 | 外部模块用于隐藏模块定义的内部语句，并且只显示与声明的变量相关的方法和参数。 |
| 2        | 内部模块在Typescript的早期版本中。但是在最新版本的TypeScript中使用名称空间仍然支持它们。 | 外部模块在最新版本的TypeScript中称为模块。                   |
| 3        | 内部模块是其他模块(包括全局模块和外部模块)的本地或导出成员。 | 外部模块是使用外部模块名称引用的单独加载的代码体。           |
| 4        | 内部模块使用指定其名称和主体的moduledeclaration来声明。      | 外部模块被编写为一个单独的源文件，其中包含至少一个导入或导出声明。 |
| 5        | 例子: module Sum \\{    export function add(a, b) \\{     console.log(“Sum: ” +(a+b));    \\}  \\} | 例子: export class Addition\\{   constructor(private x?: number, private y?: number)\\{   \\}   Sum()\\{     console.log(“SUM: ” +(this.x + this.y));   \\} \\} |



### Typescript中的名称空间是什么？如何在Typescript中声明名称空间？

名称空间是用于对功能进行逻辑分组的一种方式。名称空间用于在内部维护typescript的遗留代码。它封装了共享某些关系的特性和对象。名称空间也称为内部模块。名称空间还可以包括接口、类、函数和变量，以支持一组相关功能。

注意: 名称空间可以在多个文件中定义，并允许将每个文件都定义在一个地方。它使代码更容易维护。

**用于创建名称空间的语法**

```
namespace <namespace_name> \\{    



           export interface I1 \\{ \\}    



           export class c1\\{ \\}    



\\}    
```



### 解释在TypeScript中的装饰器？

修饰符是一种特殊类型的声明，可以应用于类、方法、访问器、属性或参数。修饰符只是以@expression符号为前缀的函数，其中表达式必须求值为一个函数，该函数将在运行时用有关修饰声明的信息调用。

TypeScript装饰器以声明的方式将注释和元数据添加到现有代码中。装饰器是为ES7提出的一个实验性特性。它已经被一些JavaScript框架使用，包括Angular 2。装饰器在未来的版本中可能会改变。

要启用对decorator的实验支持，我们必须在命令行或在我们的tsconfig.json中启用experimental aldecorators编译器选项:

命令行

```
$tsc --target ES5 --experimentalDecorators    
```

**tsconfig.json**

```
\\{    
    "compilerOptions": \\{    
        "target": "ES5",    
        "experimentalDecorators": true    
    \\}    
\\}    
```



### 什么是混合mixin？

在Javascript中，mixin是一种从可重用组件构建类的方法，通过组合称为mixin的更简单的部分类来构建它们。

这个想法很简单，不是类a扩展类B来获得它的功能，而是函数B获取类a并返回一个新类，这个类具有这个添加的功能。函数B是一个混合函数。



### TypeScript类中属性/方法的默认可见性是什么？

Public是TypeScript类中属性/方法的默认可见性。



### TypeScript是如何在函数中支持可选参数的？

与JavaScript不同，如果我们试图调用一个函数而不提供其函数签名中声明的参数的确切数量和类型，那么TypeScript编译器将抛出一个错误。为了克服这个问题，我们可以通过使用问号符号(‘?’)来使用可选参数。这意味着可以或不可以接收值的参数可以附加一个’?”“可选的。

```
function Demo(arg1: number, arg2? :number) \\{              

\\}因此，arg1总是必需的，而arg2是一个可选参数  
```

因此，arg1总是必需的，而arg2是一个可选参数。

注意: 可选参数必须遵循要求的参数。如果我们想让arg1成为可选的，而不是arg2，那么我们需要改变顺序，arg1必须放在arg2之后。

```
function Demo(arg2: number, arg1? :number) \\{  

\\}  
```



### JavaScript不支持函数重载，但TypeScript是否支持函数重载？

是的，TypeScript支持函数重载。但是它的实现很奇怪，当我们在TypeScript中执行函数重载时，我们只能实现一个带有多个签名的函数。

```
//带有字符串类型参数的函数  
function add(a:string, b:string): string;    
//带有数字类型参数的函数
function add(a:number, b:number): number;    
//函数定义
function add(a: any, b:any): any \\{    
    return a + b;    
\\}    
```

在上面的例子中，前两行是函数重载声明。它有两次重载，第一个签名的参数类型为string，而第二个签名的参数类型为number。第三个函数包含实际实现并具有any类型的参数。任何数据类型都可以接受任何类型的数据。然后，实现检查所提供参数的类型，并根据供应商参数类型执行不同的代码段。



### 可以调试任何TypeScript文件吗？

是的。要调试任何TypeScript文件，我们需要.js源映射文件。因此，使用—sourcemap标志编译.ts文件以生成源映射文件。

```
$ tsc -sourcemap file1.ts  
```

这将创建file1.js和file1.js.map，而file1.js的最后一行是源映射文件的引用。

```
//# sourceMappingURL=file1.js.map  
```



### 什么是TypeScript定义管理器？为什么我们需要它？

TypeScript定义管理器(TSD)是一个包管理器，用于直接从社区驱动的DefinitelyTyped库中搜索和安装TypeScript定义文件。

假设我们想在.ts文件中使用一些jQuery代码。

```
$(document).ready(function() \\{ //Your jQuery code \\});  
```

现在，当我们尝试使用tsc编译它时，它会给出一个编译时错误: 找不到名称“$”。因此，我们需要通知TypeScript编译器“$”属于jQuery。要做到这一点，TSD就要发挥作用。我们可以下载jQuery类型定义文件并将其包含在.ts文件中。以下是实现这一目标的步骤:

首先,安装TSD中。

```
$ npm install tsd -g  
```

在TypeScript目录中，通过运行创建一个新的TypeScript项目

```
$ tsd init  
```

然后安装jQuery的定义文件。

```
tsd query jquery --action install  
```

上面的命令将下载并创建一个包含以“.d.ts”结尾的jQuery定义文件的新目录。现在，通过更新TypeScript文件以指向jQuery定义来包含定义文件。

```
/// <reference path="typings/jquery/jquery.d.ts" />  
$(document).ready(function() \\{ //To Do  
\\});  
```

现在，再次编译。这次将生成js文件，没有任何错误。因此，TSD的需要帮助我们获得所需框架的类型定义文件。



### 什么是TypeScript Declare关键字?

我们知道所有的JavaScript库/框架都没有TypeScript声明文件，但是我们希望在TypeScript文件中使用它们时不会出现编译错误。为此，我们使用declare关键字。在我们希望定义可能存在于其他地方的变量的环境声明和方法中，可以使用declare关键字。

例如，假设我们有一个名为myLibrary的库，它没有TypeScript声明文件，在全局命名空间中有一个名为myLibrary的命名空间。如果我们想在TypeScript代码中使用这个库，我们可以使用以下代码:

```
declare var myLibrary;  
```

TypeScript运行时将把myLibrary变量赋值为任意类型。这是一个问题，我们不会得到智能感知在设计时，但我们将能够使用库在我们的代码。



### 如何从任何.ts文件生成TypeScript定义文件?

我们可以使用tsc编译器从任何.ts文件生成TypeScript定义文件。它将生成一个TypeScript定义，使我们的TypeScript文件可重用。

```
tsc --declaration file1.ts  
```



### 什么是tsconfig.son文件吗？

tsconfig.son文件是json格式的文件。tsconfig.json文件中，我们可以指定各种选项告诉编译器如何编译当前项目。目录中存在tsconfig.json文件，表明该目录是TypeScript项目的根目录。 下面是一个示例tsconfig.json文件。

```
\\{  
   "compilerOptions": \\{  
      "declaration": true,      
      "emitDecoratorMetadata": false,      
      "experimentalDecorators": false,      
      "module": "none",      
      "moduleResolution": "node"  
      "removeComments": true,  
      "sourceMap": true  
   \\},  

   "files": [  
      "main.ts",  
      "othermodule.ts"  
    ]  
\\}  
```



### 解释TypeScript中的泛型？

TypeScript泛型是一个提供创建可重用组件方法的工具。它能够创建可以处理多种数据类型而不是单一数据类型的组件。泛型在不影响性能或生产率的情况下提供类型安全性。泛型允许我们创建泛型类、泛型函数、泛型方法和泛型接口。

在泛型中，类型参数写在开(<)和闭(>)括号之间，这使得它是强类型集合。泛型使用一种特殊类型的类型变量<T>，它表示类型。泛型集合只包含类似类型的对象。

```
function identity<T>(arg: T): T \\{      
    return arg;      
\\}      

let output1 = identity<string>("myString");      
let output2 = identity<number>( 100 );    
console.log(output1);    
console.log(output2);     
```



### TypeScript是否支持所有面向对象的原则？

是的，TypeScript支持所有面向对象的原则。面向对象编程有四个主要原则:

- 封装,
- 继承,
- 抽象,
- 多态性。



### 如何检查TypeScript中的null和undefined ？

通过使用一个缓冲检查，我们可以检查空和未定义:

```
if (x == null) \\{  

\\}  
```

如果我们使用严格的检查，它将总是对设置为null的值为真，而对未定义的变量不为真。

例子

```
var a: number;  
var b: number = null;  
function check(x, name) \\{  
    if (x == null) \\{  
        console.log(name + ' == null');  
    \\}  
    if (x === null) \\{  
        console.log(name + ' === null');  
    \\}  
    if (typeof x === 'undefined') \\{  
        console.log(name + ' is undefined');  
    \\}  
\\}  
check(a, 'a');  
check(b, 'b');  
```

输出

```
"a == null"  
"a is undefined"  
"b == null"  
"b === null"  
```



### 我们可以在后端使用TypeScript吗？如果可以，如何使用？

是的，我们可以在后端使用TypeScript。我们可以通过下面的例子来理解它。在这里，我们选择Node.js，并具有一些额外的类型安全性和该语言带来的其他抽象。

安装TypeScript编译器

```
npm i -g typescript  
```

TypeScript编译器接受tsconfig.json文件中的选项，此文件确定将构建的文件放在何处。

```
\\{  
  "compilerOptions": \\{  
    "target": "es5",  
    "module": "commonjs",  
    "declaration": true,  
    "outDir": "build"  
  \\}  
\\}  
```

编译ts文件

```
tsc  
```

运行

```
node build/index.js  
```



### TS的“接口”和“type”语句有什么区别？

```
nterface X \\{  
    a: number  
    b: string  
\\}  

type X = \\{  
    a: number  
    b: string  
\\};  
```

| **编号** | **接口**                                  | **Type****类型**                                             |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| 1        | 接口声明总是引入指定的对象类型。          | 类型别名声明可以为任何类型(包括基元类型、联合类型和交集类型)引入名称。 |
| 2        | 接口可以在extends或implements子句中命名。 | 对象类型文字的类型别名不能在“扩展”或“实现”子句中命名。       |
| 3        | 接口创建一个到处使用的新名称。            | 类型别名不创建新名称。                                       |
| 4        | 一个接口可以有多个合并声明。              | 对象类型字面量的类型别名不能有多个合并声明。                 |



### TypeScript中的环境是什么？何时使用它？

环境声明告诉编译器其他地方存在的实际源代码。如果这些源代码在运行时不存在，而我们尝试使用它们，则它将中断而不会发出警告。

环境声明文件类似于docs文件。如果源更改，则还需要保持文档更新。如果环境声明文件未更新，那么我们将得到编译器错误。

Ambient声明使我们能够安全轻松地使用现有流行的JavaScript库，例如jquery，angularjs，nodejs等。



### 什么是TypeScript映射文件？

- TypeScript Map文件是一个源映射文件，其中包含有关我们原始文件的信息。
- .map文件是源映射文件，可让工具在发出的JavaScript代码和创建它的TypeScript源文件之间进行映射。
- 许多调试器可以使用这些文件，因此我们可以调试TypeScript文件而不是JavaScript文件。



### 什么是TypeScript中的类型断言？

类型断言的工作方式类似于其他语言中的类型转换，但是它不像其他语言一样执行C＃和Java那样的类型检查或数据重组。类型转换附带运行时支持，而类型断言对运行时没有影响。但是，类型断言仅由编译器使用，并向编译器提供有关我们希望如何分析代码的提示。

例

```
let empCode: any = 111;     
let employeeCode = <number> code;     
console.log(typeof(employeeCode)); // : number  
```



### TypeScript的as语法是什么？

as是TypeScript中类型断言的附加语法，引入as-语法的原因是原始语法(<type>)与JSX冲突。

例子

```
et empCode: any = 111;     
let employeeCode = code as number;   
```

当使用带有JSX的TypeScript时，只允许as风格的断言。



### 什么是JSX？我们可以在TypeScript中使用JSX吗？

JSX只不过是带有不同扩展名的Javascript。Facebook提出了这个新的扩展，以便与JavaScript中类似xml的HTML实现区分开来。

JSX是一种可嵌入的类似xml的语法。它将被转换成有效的JavaScript。JSX随着React框架而流行起来。TypeScript支持嵌入、类型检查和直接将JSX编译成JavaScript。

要使用JSX，我们必须做两件事。

- 使用.tsx扩展名命名文件
- 启用jsx选项



### 什么是Rest参数？

rest参数用于向函数传递零个或多个值。它是通过在参数前加上三个点字符(‘…’)来声明的。它允许函数在不使用arguments对象的情况下拥有可变数量的参数。当我们有不确定数量的参数时，这是非常有用的。

rest参数要遵循的规则:

- 一个函数中只允许有一个rest参数。
- 它必须是数组类型。
- 它必须是参数列表中的最后一个参数。

```
function sum(a: number, ...b: number[]): number \\{    
 let result = a;    
 for (var i = 0; i < b.length; i++) \\{    
 result += b[i];    
 \\}    

 console.log(result);    
\\}    

let result1 = sum(3, 5);    
let result2 = sum(3, 5, 7, 9);   
```



### 解释TypeScript的Enum枚举类型？

枚举或枚举是一种数据类型，允许我们定义一组命名常量。使用枚举可以更容易地记录意图，或者创建一组不同的案例。它是相关值的集合，可以是数值或字符串值。

例子

```
enum Gender \\{  
  Male,  
  Female  
  Other  
\\}  

console.log(Gender.Female); // : 1  
// 我们还可以通过enum值的number值来访问它
console.log(Gender[1]); // : Female  
```



### 解释相对模块和非相对模块的导入

| **非相对**                                                   | **相对**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 非相对导入可以相对于baseUrl解析，也可以通过路径映射解析。换句话说，我们在导入任何外部依赖项时使用非相对路径。 **例子****:** import * as $ from “jquery”; import \\{ Component \\} from “@angular/core”; | 相对导入可以用于我们自己的模块，这些模块保证在运行时维护它们的相对位置。相对导入以/、./或../开头。 例子: import Entry from “./components/Entry”; import \\{DefaultHeaders\\} from “../constants/http”; |



### 什么是匿名函数？

匿名函数是声明时没有任何命名标识符的函数。这些函数是在运行时动态声明的。与标准函数一样，匿名函数可以接受输入和返回输出。匿名函数在初始创建之后通常是不可访问的。

例子

```
let myAdd = function(x: number, y: number): number \\{   
return x + y;   
\\};  

console.log(myAdd())  
```



### 什么是声明合并？

声明合并是编译器随后合并两个或多个独立声明的过程。将具有相同名称的声明声明为单个定义。这个合并的定义具有两个原始声明的特性。

最简单也是最常见的声明合并类型是接口合并。在最基本的层次上，merge将两个声明的成员机械地连接到一个具有相同名称的接口中。

例子

```
interface Cloner \\{  
    clone(animal: Animal): Animal;  
\\}  

interface Cloner \\{  
    clone(animal: Sheep): Sheep;  
\\}  

interface Cloner \\{  
    clone(animal: Dog): Dog;  
    clone(animal: Cat): Cat;  
\\}  
```

这三个接口将合并为一个单独的声明

```
interface Cloner \\{  
    clone(animal: Dog): Dog;  
    clone(animal: Cat): Cat;  
    clone(animal: Sheep): Sheep;  
    clone(animal: Animal): Animal;  
\\}  
```

注: 在TypeScript中不是所有的合并都允许。目前，类不能与其他类或变量合并。



### TypeScript中的方法重写是什么?

如果子类(子类)具有与父类中声明的相同的方法，则称为方法覆盖。换句话说，在派生类或子类中重新定义基类方法。

方法重写的规则

- 该方法必须具有与父类相同的名称
- 该方法必须具有与父类相同的参数。
- 必须有一个IS-A关系(继承)。

例子

```
class NewPrinter extends Printer \\{  
    doPrint(): any \\{  
        super.doPrint();  
        console.log("Called Child class.");  
    \\}  

    doInkJetPrint(): any \\{  
        console.log("Called doInkJetPrint().");  
    \\}  
\\}

let printer: new () => NewPrinter;  
printer.doPrint();  
printer.doInkJetPrint();  
```



### Lambda/箭头函数是什么？

ES6版本的TypeScript提供了定义匿名函数的简写语法，也就是用于函数表达式。这些箭头函数也称为Lambda函数。lambda函数是没有名称的函数，箭头函数省略了function关键字。

例子

```
let sum = (a: number, b: number): number => \\{    
            return a + b;    
\\}    

console.log(sum(20, 30)); //returns 50    
```

在上面，?=>?是一个lambda操作符，(a + b)是函数的主体，(a: number, b: number)是内联参数。

ypeScript 是 Microsoft 开发的JavaScript 的开源超集，用于在不破坏现有程序的情况下添加附加功能。

由于其独特的优势，例如,静态类型和许多速记符号，TypeScript 现在被前端和全栈开发人员广泛用于大型项目。



### TypeScript 的主要特点是什么？

- 跨平台：TypeScript 编译器可以安装在任何操作系统上，包括 Windows、macOS 和 Linux。
- ES6 特性：TypeScript 包含计划中的 ECMAScript 2015 (ES6) 的大部分特性，例如箭头函数。
- 面向对象的语言：TypeScript 提供所有标准的 OOP 功能，如类、接口和模块。
- 静态类型检查：TypeScript 使用静态类型并帮助在编译时进行类型检查。因此，你可以在编写代码时发现编译时错误，而无需运行脚本。
- 可选的静态类型：如果你习惯了 JavaScript 的动态类型，TypeScript 还允许可选的静态类型。
- DOM 操作：您可以使用 TypeScript 来操作 DOM 以添加或删除客户端网页元素。



### 使用 TypeScript 有什么好处？

- TypeScript 更具表现力，这意味着它的语法混乱更少。
- 由于高级调试器专注于在编译时之前捕获逻辑错误，因此调试很容易。
- 静态类型使 TypeScript 比 JavaScript 的动态类型更易于阅读和结构化。
- 由于通用的转译，它可以跨平台使用，在客户端和服务器端项目中。



### TypeScript 的内置数据类型有哪些？

数字类型：用于表示数字类型的值。TypeScript 中的所有数字都存储为浮点值。

```cs
let identifier: number = value;
```

布尔类型：一个逻辑二进制开关，包含true或false

```cs
let identifier: string = " ";
```

Null 类型： Null 表示值未定义的变量。

```cs
let identifier: bool = Boolean value;
```

未定义类型：一个未定义的字面量，它是所有变量的起点。

```typescript
let num: number = null;
```

void 类型：分配给没有返回值的方法的类型。

```javascript
let unusable: void = undefined;
```



### TypeScript 目前的稳定版本是什么？

当前的稳定版本是 4.2.3。



### TypeScript 中的接口是什么？

接口为使用该接口的对象定义契约或结构。

接口是用关键字定义的interface，它可以包含使用函数或箭头函数的属性和方法声明。

```typescript
interface IEmployee \\{
    empCode: number;
    empName: string;
    getSalary: (number) => number; // arrow function
    getManagerName(number): string; 
\\}
```



### TypeScript 中的模块是什么？

TypeScript 中的模块是相关变量、函数、类和接口的集合。

你可以将模块视为包含执行任务所需的一切的容器。可以导入模块以轻松地在项目之间共享代码。

```cpp
module module_name\\{
	class xyz\\{
	export sum(x, y)\\{
		return x+y;
	\\}
\\}
```



### 后端如何使用TypeScript？

你可以将 Node.js 与 TypeScript 结合使用，将 TypeScript 的优势带入后端工作。

只需输入以下命令，即可将 TypeScript 编译器安装到你的 Node.js 中：

```nginx
npm i -g typescript
```



### TypeScript 中的类型断言是什么？

TypeScript 中的类型断言的工作方式类似于其他语言中的类型转换，但没有 C# 和 Java 等语言中可能的类型检查或数据重组。类型断言对运行时没有影响，仅由编译器使用。

类型断言本质上是类型转换的软版本，它建议编译器将变量视为某种类型，但如果它处于不同的形式，则不会强制它进入该模型。



### 如何在 TypeScript 中创建变量？

你可以通过三种方式创建变量：var，let，和const。
var是严格范围变量的旧风格。你应该尽可能避免使用，var因为它会在较大的项目中导致问题。

```typescript
var num:number = 1;
```

let是在 TypeScript 中声明变量的默认方式。与var相比，let减少了编译时错误的数量并提高了代码的可读性。

```typescript
let num:number = 1;
```

const创建一个其值不能改变的常量变量。它使用相同的范围规则，let并有助于降低整体程序的复杂性。

```typescript
const num:number = 100;
```



### 在TypeScript中如何从子类调用基类构造函数？

你可以使用该super()函数来调用基类的构造函数。

```typescript
class Animal \\{
  name: string;
  constructor(theName: string) \\{
    this.name = theName;
  \\}
    
  move(distanceInMeters: number = 0) \\{
    console.log(`$\\{this.name\\} moved $\\{distanceInMeters\\}m.`);
  \\}
\\}

class Snake extends Animal \\{
  constructor(name: string) \\{
    super(name);
  \\}

  move(distanceInMeters = 5) \\{
    console.log("Slithering...");
    super.move(distanceInMeters);
  \\}
\\}
```



### 解释如何使用 TypeScript mixin

Mixin 本质上是在相反方向上工作的继承。Mixins 允许你通过组合以前类中更简单的部分类设置来构建新类。

相反，类A继承类B来获得它的功能，类B从类A需要返回一个新类的附加功能。



### TypeScript 中如何检查 null 和 undefined？

你可以使用 juggle-check，它检查 null 和 undefined，或者使用 strict-check，它返回true设置为null的值，并且不会评估true未定义的变量。

```typescript
//juggle
if (x == null) \\{  

\\}
var a: number;  
var b: number = null;  
function check(x, name) \\{  
    if (x == null) \\{  
        console.log(name + ' == null');  
    \\}  
    if (x === null) \\{  
        console.log(name + ' === null');  
    \\}  
    if (typeof x === 'undefined') \\{  
        console.log(name + ' is undefined');  
    \\}  
\\}  

check(a, 'a');  
check(b, 'b');
```



### TypeScript 中的 getter/setter 是什么？你如何使用它们？

Getter 和 setter 是特殊类型的方法，可帮助你根据程序的需要委派对私有变量的不同级别的访问。

Getters 允许你引用一个值但不能编辑它。Setter 允许你更改变量的值，但不能查看其当前值。这些对于实现封装是必不可少的。

例如，新雇主可能能够了解get公司的员工人数，但无权set了解员工人数。

```cs
const fullNameMaxLength = 10;
class Employee \\{
  private _fullName: string = "";
  get fullName(): string \\{
    return this._fullName;
  \\}
  set fullName(newName: string) \\{
    if (newName && newName.length > fullNameMaxLength) \\{
      throw new Error("fullName has a max length of " + fullNameMaxLength);
    \\}
    this._fullName = newName;
  \\}
\\}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) \\{
  console.log(employee.fullName);
\\}
```



### 如何允许模块外定义的类可以访问？

你可以使用export关键字打开模块以供在模块外使用。

```typescript
module Admin \\{
  // use the export keyword in TypeScript to access the class outside
  export class Employee \\{
    constructor(name: string, email: string) \\{ \\}
  \\}
  let alex = new Employee('alex', 'alex@gmail.com');
\\}

// The Admin variable will allow you to access the Employee class outside the module with the help of the export keyword in TypeScript
let nick = new Admin.Employee('nick', 'nick@yahoo.com');
```



### 如何使用 Typescript 将字符串转换为数字？

与 JavaScript 类似，你可以使用parseInt或parseFloat函数分别将字符串转换为整数或浮点数。你还可以使用一元运算符+将字符串转换为最合适的数字类型，“3”成为整数，3而“3.14”成为浮点数3.14。

```typescript
var x = "32";
var y: number = +x;
```



### 什么是 .map 文件，为什么/如何使用它？

甲.map文件是源地图，显示原始打字稿代码是如何解释成可用的JavaScript代码。它们有助于简化调试，因为你可以捕获任何奇怪的编译器行为。

调试工具还可以使用这些文件来允许你编辑底层的 TypeScript 而不是发出的 JavaScript 文件。



### TypeScript 中的类是什么？你如何定义它们？

类表示一组相关对象的共享行为和属性。

例如，我们的类可能是Student，其所有对象都具有该attendClass方法。另一方面，John是一个单独的 type 实例，Student可能有额外的独特行为，比如attendExtracurricular.

你使用关键字声明类class：

```typescript
class Student \\{    
    studCode: number;    
    studName: string;    
    constructor(code: number, name: string) \\{    
            this.studName = name;    
            this.studCode = code; 
    \\}
```



### TypeScript 与 JavaScript 有什么关系？

TypeScript 是 JavaScript 的开源语法超集，可编译为 JavaScript。所有原始 JavaScript 库和语法仍然有效，但 TypeScript 增加了 JavaScript 中没有的额外语法选项和编译器功能。

TypeScript 还可以与大多数与 JavaScript 相同的技术接口，例如 Angular 和 jQuery。



### TypeScript 中的 JSX 是什么？

JSX 是一种可嵌入的类似于 XML 的语法，允许你创建 HTML。TypeScript 支持嵌入、类型检查和将 JSX 直接编译为 JavaScript。



### TypeScript 支持哪些 JSX 模式？

TypeScript有内置的支持preserve，react和react-native。

- preserve 保持 JSX 完整以用于后续转换。
- react不经过 JSX 转换，而是react.createElement作为.js文件扩展名发出和输出。
- react-native结合起来preserve，react因为它维护所有 JSX 和输出作为.js扩展。



### 如何编译 TypeScript 文件？

你需要调用 TypeScript 编译器tsc来编译文件。你需要安装 TypeScript 编译器，你可以使用npm.

```sql
npm install -g typescript

tsc <TypeScript File Name>
```



### TypeScript 中有哪些范围可用？这与JS相比如何？

- 全局作用域：在任何类之外定义，可以在程序中的任何地方使用。
- 函数/类范围：在函数或类中定义的变量可以在该范围内的任何地方使用。
- 局部作用域/代码块：在局部作用域中定义的变量可以在该块中的任何地方使用。



### TypeScript 中的箭头/lambda 函数是什么？

胖箭头函数是用于定义匿名函数的函数表达式的速记语法。它类似于其他语言中的 lambda 函数。箭头函数可让你跳过function关键字并编写更简洁的代码。



### 解释rest参数和声明rest参数的规则。

其余参数允许你将不同数量的参数（零个或多个）传递给函数。当你不确定函数将接收多少参数时，这很有用。其余符号之后的所有参数...都将存储在一个数组中。
例如：

```cs
function Greet(greeting: string, ...names: string[]) \\{
    return greeting + " " + names.join(", ") + "!";
\\}

Greet("Hello", "Steve", "Bill"); // returns "Hello Steve, Bill!"
Greet("Hello");// returns "Hello !"
```

rest 参数必须是参数定义的最后一个，并且每个函数只能有一个 rest 参数。



### 什么是三斜线指令？有哪些三斜杠指令？

三斜线指令是单行注释，包含用作编译器指令的 XML 标记。每个指令都表示在编译过程中要加载的内容。三斜杠指令仅在其文件的顶部工作，并且将被视为文件中其他任何地方的普通注释。

- /// <reference path="..." /> 是最常见的指令，定义文件之间的依赖关系。
- /// <reference types="..." />类似于path但定义了包的依赖项。
- /// <reference lib="..." />允许您显式包含内置lib文件。



### Omit类型有什么作用？

Omit是实用程序类型的一种形式，它促进了常见的类型转换。Omit允许你通过传递电流Type并选择Keys在新类型中省略来构造类型。

```xml
Omit<Type, Keys>
```

例如：

```typescript
interface Todo \\{
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
\\}
type TodoPreview = Omit<Todo, "description">;
```



### TypeScript中如何实现函数重载？

要在 TypeScript 中重载函数，只需创建两个名称相同但参数/返回类型不同的函数。两个函数必须接受相同数量的参数。这是 TypeScript 中多态性的重要组成部分。

例如，你可以创建一个add函数，如果它们是数字，则将两个参数相加，如果它们是字符串，则将它们连接起来。

```typescript
function add(a:string, b:string):string;
function add(a:number, b:number): number;
function add(a: any, b:any): any \\{
    return a + b;
\\}
add("Hello ", "Steve"); // returns "Hello Steve" 
add(10, 20); // returns 30
```



### 如何让接口的所有属性都可选？

你可以使用partial映射类型轻松地将所有属性设为可选。



### 什么时候应该使用关键字unknown？

unknown，如果你不知道预先期望哪种类型，但想稍后分配它，则应该使用该any关键字，并且该关键字将不起作用。



### 什么是装饰器，它们可以应用于什么？

装饰器是一种特殊的声明，它允许你通过使用@<name>注释标记来一次性修改类或类成员。每个装饰器都必须引用一个将在运行时评估的函数。

例如，装饰器@sealed将对应于sealed函数。任何标有 的@sealed都将用于评估sealed函数。

```javascript
function sealed(target) \\{
  // do something with 'target' ...
\\}
```

它们可以附加到：

- 类声明
- 方法
- 配件
- 特性
- 参数

注意：默认情况下不启用装饰器。要启用它们，你必须experimentalDecorators从tsconfig.json文件或命令行编辑编译器选项中的字段。



### ts中type和interface的区别？

#### 相同点：

（1） 两者都可以定义对象和函数。

interface:

```
 interface Person\\{
  name: string;
  age: number;
\\}
interface SetPerson \\{
  (name: string, age: number): void;
\\}
```


type:

```
type Person= \\{
  name: string;
  age: number
\\};
type SetPerson = (name: string, age: number)=> void;
```

(2) 都可以继承。
interface 定义的对象用extends继承，type用&继承。二者之间可以用前面提到的自己的语法互相继承。

#### 不同点：

（1）interface可以声明合并，即声明了多个同样名称的接口可以合并成一个，而type不行。

```
interface Pesron\\{
  name: string;
  age: number;
\\}
interface Person\\{
  sex: string;
\\}
/*
Person接口为 \\{
  name: string;
  age: number;
  sex: string ;
\\}
*/
```

(2) type可以声明：基本类型的别名、联合类型、元组等类型，而interface不行。

```
 // 别名
type Empty=null;
// 联合类型
interface Person1\\{
	sayHi();
\\}
interface Person2\\{
	eat();
\\}
type Person = Person1 | Person2;
type ex = number | string;
// 元组 数组中元素的数据类型都一般是相同的（any[] 类型的数组可以不同），如果存储的元素数据类型不同，则需要使用元组。
type tuple=[1,'good'];
//type 语句中可以使用 typeof 获取实例的类型进行赋值
let tem = new Number();
type B = typeof tem;
```

(3)还有其他复杂操作，泛型等。



### ts中interface和class的区别? 分别什么时候使用？

A2: interface和class都能定义数据模型。区别：……
区别：interface只是用来声明对象类型或方法，不做实现；而class是类的声明并实现。

简单的数据模型，直接用于展示的，用 interface 进行定义；
比较复杂的数据模型，有字段属性定义以及一些方法，就需要使用 class 。里面还有constructor构造函数。
interface 只在编译时用于类型检查，class 编译完成之后实际上就是 javascript 中的原型（prototype）。
接口可以通过extends继承类，类可以通过implements去实现接口。有个很好的例子帮助理解。



### ts中的泛型有什么了解？

#### 不用泛型的话，这个函数可能是下面这样：

```
function identity(arg: number): number \\{
    return arg;
\\}
```

或者，我们使用any类型来定义函数：

```
function identity(arg: any): any \\{
    return arg;
\\}
```

any的情况，可以是任何类型。因此，我们需要一种方法使返回值的类型与传入参数的类型是相同的。 这时，就用到了T，类型变量，它是一种特殊的变量，只用于表示类型而不是值。

```
function identity<T>(arg: T): T \\{
    return arg;
\\}
```

这样就可以跟踪函数里使用的类型信息。

#### 泛型的使用方法有两种：

此处参考官方文档改写。
(1) 尖括号的形式：
let output = identity< string> (“myString”);// type of output will be ‘string’
这里明确的指定了T是string类型，并做为一个参数传给函数，使用了<>括起来。

(2) 利用了类型推论，即编译器会根据传入的参数自动地帮助我们确定T的类型：
let output = identity(“myString”); // type of output will be ‘string’



### typescript 基础类型

对象类型

```
const test:\\{
    name:string,
    age:number
\\} = \\{
    name:'comix',
    age:19
\\}
复制代码
```

数组类型

```
const testArry :string[] = ['123','232']
复制代码
```

类类型

```
class Person\\{\\}
const test:Person = new Person()
复制代码
```

函数类型

```
const test:() => string = () => \\{
   return 'xiao'
\\}
复制代码
```



### type与interface 的区别

ts中定义类型的两种方式:

接口（interface） 类型别名（type alias）

interface只能定义对象类型, type声明的方式可以定义组合类型、交叉类型和原始类型

相同点： 都可以描述一个对象或函数

```
interface User \\{
 name: string
 age: number
\\}
 
interface SetUser \\{
 (name: string, age: number): void;
\\}
复制代码
type User = \\{
 name: string
 age: number
\\};
 
type SetUser = (name: string, age: number): void;
```

不同点：

- type 可以声明基本类型别名，联合类型，元组等类型
- interface 能够声明合并，type不可以