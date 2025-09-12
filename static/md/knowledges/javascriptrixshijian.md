---
title: JavaScript日期时间
date: 2020-03-26 21:10:40
categories: 
- 前端知识
tags:
- JavaScript
---

### js获取当前年月日

```
var date = new Date();

date .getYear(); //获取当前年份(2位)

date .getFullYear(); //获取完整的年份(4位)

date .getMonth(); //获取当前月份(0-11,0代表1月)

date .getDate(); //获取当前日(1-31)

date .getDay(); //获取当前星期X(0-6,0代表星期天)

date .getTime(); //获取当前时间(从1970.1.1开始的毫秒数)

date .getHours(); //获取当前小时数(0-23)

date .getMinutes(); //获取当前分钟数(0-59)

date .getSeconds(); //获取当前秒数(0-59)

date .getMilliseconds(); //获取当前毫秒数(0-999)

date .toLocaleDateString(); //获取当前日期

var mytime=date .toLocaleTimeString(); //获取当前时间

date .toLocaleString( ); //获取日期与时间
```



### 比较两个日期

`getTime()` 是 JavaScript `Date` 对象的一个方法，它返回从 1970 年 1 月 1 日 UTC 00:00:00 起到调用此方法的日期对象所表示的时间的毫秒数。这个值通常被称为“时间戳”，并且对于比较日期和执行涉及时间的计算非常有用，因为它提供了一个统一的数值表示形式。

当你需要比较两个日期或者计算它们之间的差值时，使用 `getTime()` 方法是有必要的。这是因为 `Date` 对象在默认情况下并不直接支持比较运算符（如 `>` 或 `<`），除非它们被转换成相同的形式。通过将日期转换为其时间戳，你可以直接使用这些运算符进行比较。

下面是一个例子，展示了如何使用 `getTime()` 方法来比较两个日期：

```javascript
let date1 = new Date('2024-01-01');
let date2 = new Date('2024-01-02');

if (date1.getTime() < date2.getTime()) \\{
    console.log('date1 在 date2 之前');
\\} else \\{
    console.log('date1 在 date2 之后或与之相同');
\\}
```

然而，在现代 JavaScript 中，直接比较 `Date` 对象实际上会自动调用 `getTime()` 方法，所以你可以直接比较 `Date` 对象而无需显式地调用 `getTime()`：

```javascript
let date1 = new Date('2024-01-01');
let date2 = new Date('2024-01-02');

if (date1 < date2) \\{
    console.log('date1 在 date2 之前');
\\} else \\{
    console.log('date1 在 date2 之后或与之相同');
\\}
```

这使得代码更简洁，但理解 `getTime()` 的功能仍然很重要，尤其是在需要获取或设置特定时间戳的场景中。



### 日期时间格式`'YYYY-MM-DD HH:mm:ss'`

```
/**
 * @description 用户点击弹窗的“确认”按钮，执行创建预约的操作
 */
const confirmSchedule = async () => \\{
  if (!currentGroup.value) return
  console.log('日期和时间', scheduleDateArr.value, scheduleTimeArr.value)

  // 组合日期和时间数组为一个标准的 Date 对象
  const [year, month, day] = scheduleDateArr.value
  const [hour, minute] = scheduleTimeArr.value
  const selectedDateTime = new Date(
    `$\\{year\\}-$\\{month\\}-$\\{day\\}T$\\{hour\\}:$\\{minute\\}:00`
  )

  // 前端校验：预约时间不能早于当前时间
  if (selectedDateTime < new Date()) \\{
    showToast('预约时间不能早于当前时间')
    return
  \\}

  showLoadingToast(\\{ message: '预约中', duration: 0 \\})
  try \\{
    // 格式化日期时间为YYYY-MM-DD HH:mm:ss
    const startTime =
      `$\\{year\\}-$\\{month.padStart(2, '0')\\}-$\\{day.padStart(2, '0')\\} ` +
      `$\\{hour.padStart(2, '0')\\}:$\\{minute.padStart(2, '0')\\}:00`
    const \\{ success \\} = await createScheduleCode(\\{
      empGroupId: currentGroup.value.empGroupId,
      startTime
    \\})
    if (success) \\{
      closeToast()
      showToast('预约成功')
      // 成功后，刷新当前员工组的预约列表
      await fetchScheduledList(currentGroup.value, true)
    \\}
  \\} catch (error) \\{
    console.error('创建预约失败', error)
  \\}
\\}
```

