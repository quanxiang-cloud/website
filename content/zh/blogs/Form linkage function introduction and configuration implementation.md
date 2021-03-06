---
title: '表单联动之功能介绍及配置实现'
tag: '表单, 前端, 低代码'
keywords: '表单, 表单联动, 快速查询, 前端, 低代码, low-code'
description: '实际业务场景中用到表单联动的地方比较多，最典型的例子就是地区联动，如省级下拉框选择四川省，市级下拉框则只能选择四川省对应的城市。当然表单联动还有很多使用场景，这里不一一叙述，它们都有一个共性，即用户输入某信息后，能够快速的查询匹配、填写相关数据。'
createTime: '2021-09-17'
author: '祁苗'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/cover.png'
---

# 功能介绍



实际业务场景中用到表单联动的地方比较多，最典型的例子就是地区联动，如省级下拉框选择四川省，市级下拉框则只能选择四川省对应的城市。当然表单联动还有很多使用场景，这里不一一叙述，它们都有一个共性，即用户输入某信息后，能够快速的查询匹配、填写相关数据。



概括的说，表单联动就是表单数据通过关联其他表单中**满足一定条件**的数据获得，主要用于快速填写信息、快速查询信息。



举个例子，用户在【商品定价表】中输入商品名称，定价文本框自动填入`该商品`的价格。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/1.png" width = 60%/>

<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/2.png" width = 60%/>
</div>

# 配置思路



为了实现上述案例，假设现在有【商品信息表 A】包含商品名称、商品编号、商品定价、生产日期等字段，【商品价格表 B】包含商品、价格两个字段。我们需要对【商品价格表 B】中的商品定价文本框进行联动配置，让用户在输入商品名称的时候，定价文本框自动填入`该商品`的价格。



全象云低代码平台配置联动表单的实现思路如下：

1. 选择数据联动表单【商品信息表 A】。
2. 配置数据排序规则，选择字段对符合条件的关联数据行之行升序/降序操作。
3. 配置数据联动的条件。本示例为：【商品信息表 A】的商品名称 ==【商品价格表 B】的商品名称。
4. 配置数据关联项。本示例为：定价文本框联动显示为关联数据表 A 中的集体某个数据项。

**说明：**<br>
查询得到满足条件的关联数据可能有多条，此时需要通过配置数据排序去确定这条唯一匹配的关联数据。

配置完成并保存后，用户端则根据此配置规则执行数据联动，用户输入商品名称，系统自动填入商品对应的价格。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/3.png" width = 60%/>
</div>

# 配置实现

表单联动配置的逻辑实现如下：

- 监听联动表单值，获取选择表单的字段信息，将当前所选联动表单的字段作为取值规则字段、条件字段、表单值时的比较字段、显示值字段的可选项。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/4.png" width = 60%/>
</div>

- 监听条件字段的变化并渲染操作符，过滤比较值字段。
	
条件字段可能是单行文本、数字、时间日期、下拉框、下拉复选框、单选框/复选框。以上字段的数据类型不同，其对应的操作符也是不同的，比如 number 类型字段的操作符可以匹配“大于”，但是 string 类型的字段却不能匹配“大于”。所以我们需要监听条件字段，根据条件字段的数据类型，去渲染操作符字段的可选项值。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/5.png" width = 60%/>
</div>

- 监听操作符字段值，渲染比较值字段的下拉框选择模式是否为 multiple。

当操作符字段值为[`全部包含`,`不包含`,`属于`,`不属于`]其中之一时，这个条件表达式的比较值字段应该为多选，此时需要设置比较值字段下拉框的 mode 属性为 multiple。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/6.png" width = 60%/>
</div>

- 监听比较值模式（表单值/固定值），渲染比较值字段的 input 类型。

当比较值模式为固定值时，根据条件字段 input 类型，渲染比较值字段的 input。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/7.png" width = 60%/>
</div>

- 当比较值模式为表单值时，渲染比较值字段为 input 为下拉框，并且可选项值为当前表单的字段数组。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/8.png" width = 60%/>
</div>

- 显示字段的可选项值过滤。

根据当前被设置数据关联的字段 input 类型，过滤可选项值，这样才能保证精准的数据关联。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20linkage%20function%20introduction%20and%20configuration%20implementation/9.png" width = 60%/>
</div>

完成一个数据联动规则配置后，前端通过逻辑处理将得到如下 JSON 字符串用于记录当前表单数据联动配置规则，后续在`数据联动实现`的时候，以此 JSON 字符串为目标去执行相应的数据联动，在此基础上得到我们预期的数据联动效果。

    {
      linkedAppID: '', //当前app的id
      linkedTable: { id: '', name: '' }, //联动表单值
      linkedTableSortRules: [], //取值规则
      linkedField: '', // 显示值字段
      targetField: '', // 设置数据联动的字段
      ruleJoinOperator: 'every', //条件满足规则（全部/任一）
      rules: [{
        fieldName: '', // 条件字段值
        compareOperator: '==', //操作符字段值
        compareTo: 'currentFormValue', //比较值数据源类型
        compareValue: '', // 比较值字段
      }]
    }



# 总结



表单联动实质是有条件的数据关联，根据条件字段的值，去获取满足条件的数据，然后将数据按照我们的期望 set 到对应的字段中去，实现快速填写信息、快速查询信息的功能。

表单联动的联动规则执行将在后续的公众号内容中给出，敬请期待。