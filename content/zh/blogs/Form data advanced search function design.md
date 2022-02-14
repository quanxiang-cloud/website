---
title: '表单数据高级搜索功能设计'
tag: '表单, 搜索, 数据搜索, 低代码, 前端技术'
keywords: '表单, 搜索, 数据搜索, 低代码, 前端技术, low-code'
description: '搜索是我们在日常上网中使用率非常高的功能，搜索的目的是快速检索到目标数据，用户输入目标数据的一定特征作为搜索条件，进行搜索之后就能得到符合相应特征的数据。输入的特征越多越详细，得到的结果也就会越精确。'
createTime: '2022-01-14'
author: '谭杰'
snapshot: 'https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/cover.png'
---

## 背景

“搜索”是我们在日常上网中使用率非常高的功能，搜索的目的是快速检索到目标数据，用户输入目标数据的一定特征作为搜索条件，进行搜索之后就能得到符合相应特征的数据。输入的特征越多越详细，得到的结果也就会越精确。

不过为了使用的便利性，一般默认的搜索都不会让用户配置太多的条件，所以我们日常接触的搜索都是简化版本的搜索。但是当数据量增大起来之后，为了准确得到目标数据，往往需要配置更多的条件并且调整各个条件之间的关系，这种情况下我们就会发现固定条件和关系的简单搜索已经无法满足需求了，这时候我们就需要更加完整的搜索功能——即“高级搜索”。


## 设计思路

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/1.png" width = 60%/>
</div>



首先讲一下设计思路，如上图我们可以发现搜索语句由多个条件组成，每个条件又由字段、比较符、值组成。那用户只需要根据需求配置每个条件就可以了。这其中有几个需要考虑到的细节：

1. 搜索的条件值类型其实并不统一：例如数字和字符串的比较符就应该不同；
2. 各个条件之间的关系，是需要全部满足还是满足任意一个；

根据这个思路实现的功能界面如下图：


<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/2.png" width = 60%/>
</div>


## 实现技术详解

接下来我们讲讲如何实现，先来看看生成的筛选条件的类型定义：

```tsx
type Condition = {
key: string; // 限定字段的key
op: string; // 操作符
value: FormValue; // value的类型就是表单组件输出的值的类型
}

type FilterTag = 'should' | 'must';

type FilterConfig = {
  condition: Condition[];
  tag: FilterTag;
}
```

这里的含义是：
1. 每一个条件对应一个`Condition`；
2. `FilterTag`代表每个条件之间的关系，should 代表任意一个条件满足时就通过筛选，must 代表满足所有条件时才能通过筛选；
3. 最终的输出是`FilterConfig`;



### 条件配置的实现

为了得到这个`FilterConfig`，我们需要做五步工作：

#### 1. 新建一项空白的条件：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/7.png" width = 60%/>
</div>

#### 2. 选择用作搜索条件的表单字段

第一个下拉选择框是选择你想要用作搜索条件的表单字段，打开下拉框如图所示；

- 下拉框选择的选项 = 表单自有字段 + 系统字段：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/3.png" width = 60%/>
</div>

- 表单字段：

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/4.png" width = 60%/>
</div>


#### 3. 选择操作符

由于不同表单字段的值类型并不一定相同，所有操作符要根据所选表单字段的类型展示相应的操作符集合。

目前低代码平台的表单值类型有：String、Boolean、Number、LabelValue、Datetime、Array<String|Boolean|Number|LabelValue>。根据这几种类型需要提前定义好相应的操作符集合。


```js
const OPERATORS_STRING = [
  {
    label: '等于',
    value: 'eq',
  },
  {
    label: '模糊',
    value: 'like',
  },
];

const OPERATORS_NUMBER = [
  {
    label: '等于',
    value: 'eq',
  },
  {
    label: '大于',
    value: 'gt',
  },
  {
    label: '小于',
    value: 'lt',
  },
  {
    label: '大于等于',
    value: 'gte',
  },
  {
    label: '小于等于',
    value: 'lte',
  },
  {
    label: '不等于',
    value: 'ne',
  },
];

const OPERATORS_DATE = [
  {
    label: '范围',
    value: 'range',
  },
];

const OPERATORS_BOOL = [
  {
    label: '等于',
    value: 'eq',
  },
  {
    label: '不等于',
    value: 'ne',
  },
];

const OPERATORS_ARRAY_MULTIPLE = [
  {
    label: '同时包含',
    value: 'fullSubset',
  },
  {
    label: '包含任一一个',
    value: 'intersection',
  },
];

const OPERATORS_LABEL_VALUE = [
  {
    label: '等于',
    value: 'eq',
  },
  {
    label: '不等于',
    value: 'ne',
  },
];
```

在render的时候用此工具函数就可以得到需要的集合：

```js
function getOperators(type: string) {
  switch (type) {
  case 'array':
    return OPERATORS_ARRAY_MULTIPLE;
  case 'number':
    return OPERATORS_NUMBER;
  case 'datetime':
    return OPERATORS_DATE;
  case 'boolean':
    return OPERATORS_BOOL;
  case 'label-value':
    return OPERATORS_LABEL_VALUE;
  default:
    return OPERATORS_STRING;
  }
}
```

#### 4. 填写搜索条件字段的值

搜索条件字段的值是需要符合该字段的类型要求以及条件限制的。如：选择字段的组件类型为 NumberPicker，且该字段限制数字范围为 0-100， 那么就应该展示一个数字输入框且只能输入 0-100 范围内的数字。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/8.png" width = 60%/>
</div>

条件值输入框的实现代码如下：

```tsx
function FieldSwitch(type) {
  switch (type) {
  case 'CheckboxGroup':
  case 'Select':
  case 'RadioGroup':
  case 'MultipleSelect':
    return (
      <SelectField />
    );
  case 'NumberPicker':
    return (
      <InputNumber />
    );
  case 'DatePicker':
    return (
      <DatePicker.RangePicker />
    );
  case 'CascadeSelector':
    return (
      <CascadeSelector />
    );
  case 'OrganizationPicker':
    return (
      <OrganizationPicker />
    );
  case 'UserPicker':
    return (
      <UserPicker />
    );
  default:
    return <Input />;
  }
}
```

#### 5. 选择各个条件之间的关系

最后一步就是选择各个条件之间的关系了。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/9.png" width = 60%/>
</div>

- 所有：各个条件之间的关系为和（&），同时满足时才会搜索出来；
- 任一：条件之间的关系为或（|），只要满足其中一个条件就会被搜索出来；



如此一来我们点击搜索的时候就能得到一个`FilterConfig`，再将此结构进行一定转换，传递给接口后就可以实现数据的搜索。

PS：表单数据的搜索是用 [Elasticsearch] 实现的，因此会有`FilterConfig` 到 Elasticsearch 的 AST 的一个相互转换，这里的具体实现环节待下回分解。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/5.png" width = 60%/>
</div>


## 总结

普通的搜索不能配置条件之间的关系和条件的比较符号，而我们引入的高级搜索就解决了这个问题，通过各种搜索条件的组合我们就能更加快速的得到目标数据。大大提升了我们工作的效率。

<div align=center>
<img src="https://raw.githubusercontent.com/quanxiang-cloud/website/main/static/images/zh/blogs/Form%20data%20advanced%20search%20function%20design/6.png" width = 60%/>
</div>

### 引用
Elasticsearch：https://www.elastic.co/cn/ 