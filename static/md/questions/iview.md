---
title: iview
date: 2024-05-01 11:11:11
categories: 
- 前端问题
tags:
- iview
---

### iview inoput type=textarea 禁止拉伸

设置 :maxRows.minRows相同即可

```
<Input v-model="formValidate.remark" type="textarea" :rows="3" :autosize="\\{maxRows: 3,minRows: 3\\}" placeholder="请输入"/>
```



### 限制输入两位小数

第二行可以使用type="number"来代替

```
 <Input @on-keyup="(event)=>\\{
        event.target.value=event.target.value.replace(/[^0-9.]/g,'');
        num=event.target.value.match(/\d+\.?\d\\{0,2\\}/,'');\\}" 
    placeholder="请输入" 
    v-model="num"
	clearable />
```



### 表单校验prop动态切换

```
<!-- 根据fee_file动态切换prop判断是否必填，:key避免dom复用导致不生效 -->
<FormItem label="费用凭证" :prop="fee_file?'file':''" :key="fee_file">
	<SingleUpload v-model="formModel.other_amount[index].file" ></SingleUpload>
</FormItem>
```



### resetFields重置表单不生效

内容必须要在每个form-item里加上prop属性，并且与你v-model的值相同才可以

```
<Form ref="formCustom" :model="formCustom" label-position="top">
    <FormItem label="姓名：" prop="name">
         <Input type="text" v-model="formCustom.name"/>
     </FormItem>
     <FormItem label="学号：" prop="xh">
         <Input type="text" v-model="formCustom.xh"/>
     </FormItem>
</Form>

this.$refs.formCustom.resetFields();  
```



### DatePicker日期时间范围选择器问题

截止日期的时间默认是00：00：00，为提升用户体验以及实际场景需要，避免出现不必要的疏漏，将默认截止时间设置为23：59：59

```
<DatePicker :value="rangeArr" type="datetimerange" @on-change="handleAddTime" editable placeholder="申请时间"></DatePicker>

import utils from '@/utils';

rangeArr: [], // 日期时间范围选择器，控制显示的值

handleAddTime(time)\\{
   const [rangeStr, rangeArr] = utils.handleDateTimeRange(time)
   this.searchData.created_at = rangeStr;
   this.rangeArr = rangeArr;
\\}
```

utils.js

```
// 处理日期时间选择范围
utils.handleDateTimeRange = (time) => \\{
  let rangeStr, rangeArr
  console.log(time);
  if (time[0])\\{
    // 选择了范围
    const head = time[1].slice(0, 11)
    const tail = time[1].slice(11, 19)
    console.log(head, tail);
    if (tail === '00:00:00') \\{
      time[1] = head + '23:59:59'
    \\}
    rangeStr = time.join('~')
  \\} else \\{
    // 清空了范围，数组两个元素为空
    rangeStr = ''
  \\}
  rangeArr = time
  console.log(rangeStr, rangeArr);
  return [rangeStr, rangeArr]
\\}
```



###  DatePicker日期选择器禁用

普通

```
<DatePicker 
    @on-change="handleMonthChange"
    :options="options"
    type="month"
    placeholder="请选择核算月份">
</DatePicker>

data()\\{
        return\\{
            options: \\{
                // 设置不可选择的日期，参数为当前的日期，需要返回 Boolean 是否禁用这天
                disabledDate (date) \\{
                    return date && date.valueOf() > Date.now()
                \\}
            \\}
        \\}
    \\},
    
handleMonthChange(date)\\{
	this.formModel.time = date;
\\}
```

复杂

```
<DatePicker 
    @on-change="handleMonthChange"
    :value="formModel.month"
    :options="options"
    :disabled="disabled"
    type="month"
    :placeholder="placeholder">
</DatePicker>

data()\\{
        return\\{
            monthData:[], // 格式['2022-08','2022-07']
            disabled:true, // 没有选择付款公司就禁用选择器
            placeholder:'请先选择付款公司',
            options: \\{
                // 设置不可选择的日期，参数为当前的日期，需要返回 Boolean 是否禁用这天
                // 在disabledDate函数内访问不到this（值为 undefined）,用 bind 绑定
                disabledDate: (function (date) \\{
                    let y = date.getFullYear();
                    let m = date.getMonth() + 1;
                    if (m < 10) \\{
                        m = '0' + m;
                    \\}
                    let yearMonth = y + "-" + m
                    // console.log(yearMonth)
                    return date && !this.monthData.includes(yearMonth)
                    // return date && date.valueOf() > Date.now()||(yearMonth!=='2022-08'&&yearMonth!=='2022-07')
                \\}).bind(this)
            \\}
        \\}
    \\},
    
getMonthList(key)
    .then(res=>\\{
        this.monthData = res.month;
        this.disabled = false
        this.placeholder = '请选择报税月份'
        this.formModel.month = '';
    \\})
    .catch(err=>\\{
    	console.log(err);
    \\})
    
handleMonthChange(date)\\{
	this.formModel.month = date;
\\}
```



### 表格使用render函数

```
<Table stripe :columns="columns" :data="list"></Table>

columns: [
                \\{
                    title: '验收材料',
                    key: 'source_name'
                \\},
                \\{
                    title: '操作',
                    key: 'action',
                    width: 180,
                    align: 'center',
                    render: (h, params) => \\{
                        return h('div',
                            \\{
                                class:\\{
                                    action: true
                                \\}
                            \\}, 
                            [
                                // 预览
                                ( params.row.Review === '待审核' ) && h('div', 
                                \\{
                                    class:\\{
                                        item: true
                                    \\},
                                    on: \\{
                                        click: () => \\{
                                            console.log(params);
                                            this.handlePreviewTaskFile(params.row)
                                        \\}
                                    \\}
                                \\},
                                [
                                    h('xc-icon', \\{
                                        props: \\{
                                            iconClass: 'detail'
                                        \\}
                                    \\}, ''),
                                    h('p', \\{\\}, '预览')
                                ]),
                                // 下载
                                h('div', 
                                \\{
                                    class:\\{
                                        item: true
                                    \\},
                                    on: \\{
                                        click: () => \\{
                                            this.show(params.index)
                                        \\}
                                    \\}
                                \\},
                                [
                                    h('xc-icon', \\{
                                        props: \\{
                                            iconClass: ''
                                        \\}
                                    \\}, ''),
                                    h('p', \\{\\}, '下载')
                                ]),
                                // 删除
                                h('div', 
                                \\{
                                    class:\\{
                                        item: true
                                    \\},
                                    on: \\{
                                        click: () => \\{
                                            this.show(params.index)
                                        \\}
                                    \\}
                                \\},
                                [
                                    h('xc-icon', \\{
                                        props: \\{
                                            iconClass: 'delete'
                                        \\}
                                    \\}, ''),
                                    h('p', \\{\\}, '删除')
                                ])
                            ]
                        );
                    \\}
                \\}
            ],
```

