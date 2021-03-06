##  介绍

**这是一个可以通过JS对象配置就可生成页面的组件，可具有更高的开发便捷性即维护性。**

## 为什么要做这个组件？

**在大多数的B端项目开发中，很多表格及表单页面大致相同，而前端开发编写一个页面需要大量的功能代码及业务代码 而且如果不封装的情况下很难做到复用性(复制粘贴修改部分代码 确实可以复用 但是抛开优雅度不说，维护时会发现成本很高 每个被粘贴的文件都需要手动去改)所以配置生成页面这个组件 应运而生。**

## 这个组件有什么好处

我们先来看两张图片

[![react_cms_image1](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_image1.png?raw=true "react_cms_image1")](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_image1.png?raw=true "react_cms_image1")

[![react_cms_image2](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_image2.png?raw=true "react_cms_image2")](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_image2.png?raw=true "react_cms_image2")

1.上方图片 看起来可能不是一个特别复杂的页面，但是每一个功能点都需要不少的代码去实现
- 搜索区域每一项开发以及搜索重置
- 新建弹窗以及开发弹窗中的每一项（如：输入框 上传 下拉框等等）
- 新建数据保存
- 启用停用
- 表格中查看行信息详情
- 修改行信息数据
- 删除行数据
- 表格分页以及每页显示多少条

全部实现这些功能需要大量的代码，但是使用**Page组件**只需要传入对应的配置就可生成这样的功能页面

2.方便维护，因为项目中很多页面使用了这个Page组件 如果出现bug或者增加页面小功能的时候 只需修改Page组件 那么所有基于Page生成的页面都可映射为最新。

**注：通用功能会慢慢集成进来 复杂功能或复杂业务的页面最好单独开发**

## 配置示例代码请查看src/view/content/use-components/use-page/UsePage.js

## 展示

[![react_cms_config_image1](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_config_image1.png?raw=true "react_cms_config_image1")](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_config_image1.png?raw=true "react_cms_config_image1")

[![react_cms_config_image2](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_config_image2.png?raw=true "react_cms_config_image2")](https://github.com/Betteryourself-tcy/images/blob/master/show_cms_config_image2.png?raw=true "react_cms_config_image2")


## 代码详解

### 创建ref 用于调用子组件方法
```javascript
const pageRef = useRef()
```

### pageConfig

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| pageRequestUrl  | 配置请求接口  | Object  | true  | ——  |
| pageTitleConfig  | 配置页面标题  | Object  | false  | ——  |
| pageSearchConfig  | 配置搜索区域  | Object  | false  | ——  |
| pageTableConfig  | 配置表格  | Object  | true  | ——  |
| pageModalConfig  | 配置弹窗  | Object  | false  | ——  |

### pageRequestUrl

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| curdUrl  | restful风格接口地址  | String  | true  | ——  |
| getMoreParams  | get请求携带其他参数  | Object  | false  | ——  |
| postMoreParams | post请求携带其他参数 | Object  | false  | ——  |
| putMoreParams  | put请求携带其他参数  | Object  | false  | ——  |
| enableUrl  | 启用接口地址  | String  | false  | curdUrl+‘/start’  |
| disabledUrl  | 禁用接口地址  | String  | false  | curdUrl+'/stop'  |

### pageTitleConfig

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| title  | 页面标题  | String  | true  | ——  |

### pageSearchConfig

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| searchItemMarginRight  | 搜索区域每一项右边距  | String  | false  | 28px  |
| searchItemArr  | 搜索区域每一项组成的数组  | Object[]  | true  | ——  |
| connectedSelectArr  | 搜索区域下拉框数据联动数组  | Object[]  | false  | ——  |
| defaultSearchData  | 默认搜索的数据（联动下拉框第一个也可用）  | Object[]  | false  | ——  |
| getSearchDataFun  | 点击搜索按钮时的回调方法（参数：搜索区域数据） | Function  | false（PageSearch单独使用时为true）  | ——  |
| resetSearchDataFun  | 点击重置按钮时的回调方法  | Function | false（PageSearch单独使用时为true）  | ——  |

### connectedSelectAr -> Object

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| label  | 标签名称  | String  | true  | ——  |
| field  | 	后端交互字段  | String  | true  | ——  |
| placeholder  | 站位文本  | String  | false  | 请输入内容  |
| customizeOptionsValueKey  | 自定义 options 中 的value字段  | String  | false  | value  |
| customizeOptionsLabelKey  | 自定义 options 中 的label字段  | String  | false  | label  |
| url  | 获取下拉框数据的接口  | String  | true  | ——  |
| requestKey  | 获取此项下拉框数据时给此项接口传入的key名 值是上个联动输入框选中的值（若是第一个联动下拉框数据 值为requestValue的value） | String  | 第一个联动下拉框为false 其他为true  | ——  |
| requestValue（只有第一个联动下拉框才有的属性）  | 获取第一个下拉框数据时传入的值 | String  | false  | ——  |
| rules  | 校验规则，设置字段的校验逻辑 详见antd官网  | Rule[]  | false  | ——  |

### pageTableConfig

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| isShowAddBtn  | 是否显示添加按钮  | Boolean  | false  | true  |
| isShowCheckDetailsBtn  | 是否显示查看行数据详情按钮  | Boolean  | false  | true  |
| isShowUpdateBtn  | 是否显示修改按钮  | Boolean  | false  | true  |
| isShowRemoveBtn  | 是否显示删除按钮  | Boolean  | false  | true  |
| isShowEnableDisableBtn  | 是否显示启用禁用按钮  | Boolean  | false  | true  |
| isShowEnableDisableBtn  | 是否显示启用禁用按钮  | Boolean  | false  | true  |
| isShowActionColumns  | 是否显示操作列  | Boolean  | false  | true  |
| actionColumnsWidth  | 操作列的宽度，如果表格列数较多，请给每个列添加宽度（columns中的每一项增加width属性）这样表格会增加横向滚动条，操作列悬浮固定在右侧，如果isShowActionColumns为false又想出现横向滚动条的话 可以给columns中其他属性添加fixed属性（详见antd官网）  | Number  | false  | 500  |
| scroll  | 表格是否可滚动，也可以指定滚动区域的宽、高（详见antd官网）  | Object  | false  | { x: 1500, y: 490 } |
| columns  | 表格列的配置描述 详见antd官网  | ColumnsType[]  | true  | ——  |
| accordingRowIsRenderCheckBtnFun  | 根据行数据 是否渲染 查看按钮  | (record) => boolean  | false  | () => true  |
| accordingRowIsRenderUpdateBtnFun  | 根据行数据 是否渲染 修改按钮  | 	(record) => boolean  | false  | () => true |
| accordingRowIsRenderRemoveBtnFun  | 根据行数据 是否渲染 删除按钮  | 	(record) => boolean | false  | () => true  |
| accordingRowIsRenderEDBtnFun  | 根据行数据 是否渲染 启用停用  | 	(record) => boolean | false  | () => true |

### pageModalConfig

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| width  | 弹窗宽度  | Number  | false  | 560  |
| labelCol  | 弹窗中表单label标签布局 详见antd官网  | Object  | false  | { offset: 0, span: 6 }  |
| wrapperCol  | 弹窗表单中需要为输入控件设置布局样式时 使用该属性，用法同 labelCol 详见antd官网  | Object  | false  | { offset: 1, span: 12 }  |
| layout  | 表单布局 可选值 horizontal  vertical  inline  | String  | false  | horizontal  |
| maskClosable  | 点击蒙层是否允许关闭  | Boolean  | false  | true  |
| okText  | 确认按钮文字  | String  | false  | 确定  |
| cancelText  | 取消按钮文字  | String  | false  | 取消  |
| modalItemArr  | 弹窗中每一项组成的数组  | Object[]  | true  | ——  |

### searchItemArr && modalItemArr -> Object

**（一个type对应一个属性配置表 虽会有重复属性解释 但是方便阅读）**

**通用属性**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| type  | 组件类型  | String  | true  | ——  |
| label  | 标签名称  | String  | true  | ——  |
| field  | 后端交互字段  | String 或 Array(rangePicker->['开始日期字段','结束日期字段'])  | true  | ——  |
| disabled  | 是否禁用  | Boolean  | false  | false  |
| rules  | 校验规则，设置字段的校验逻辑 详见antd官网  | 	Rule[]  | false  | ——  |

**type = input \| password**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| placeholder  | 站位文本  | String  | false  | 请输入内容  |
| isNumber  | 是否为数字输入框  | Boolean  | false  | false  |

**type = select**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| placeholder  | 站位文本  | String  | false  | 请选择内容  |
| mode  | 设置 Select 的模式为多选或标签 可选值为 multiple  tags 不传为单选  | String  | false  | ''  |
| customizeOptionsValueKey  | 自定义 options 中 的value字段  | String  | false  | value  |
| customizeOptionsLabelKey  | 自定义 options 中 的label字段  | String  | false  | label  |
| options  | 数据源  | Object[]  | true  | ——  |

**type = radio \| checkbox**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| customizeOptionsValueKey  | 自定义 options 中 的value字段  | String  | false  | value  |
| customizeOptionsLabelKey  | 自定义 options 中 的label字段  | String  | false  | label  |
| options  | 数据源  | Object[]  | true  | ——  |

**type = tree**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| placeholder  | 站位文本  | String  | false  | 请选择内容  |
| customizeOptionsValueKey  | 自定义 options 中 的value字段  | String  | false  | value  |
| customizeOptionsLabelKey  | 自定义 options 中 的label字段  | String  | false  | label  |
| customizeOptionsChildrenKey  | 自定义 options 中 的children字段  | String  | false  | children  |
| options  | 数据源  | Object[]  | true  | ——  |

**type = datePicker \| rangePicker**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| placeholder  | 站位文本  | String  | false  | datePicker->请选择日期；rangePicker->['开始日期','结束日期']  |
| format  | 展示的日期格式 详见antd官网  | String  | false  | 时间戳  |
| showTime  | 增加时间选择功能  | Boolean  | false  | false  |

**type = upload**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| actionUrl  | 	上传的地址  | String  | true  | ——  |
| headers  | 	上传的请求头  | Object  | false  | ——  |
| accept  | 接受上传的文件类型 详见antd官网  | String  | false  |  ——  |
| data  | 传所需额外参数或返回上传额外参数的方法  | Object 或 (file) => object  | false  |  ——  |
| listType  | 上传列表的内建样式，支持三种基本样式 text, picture 和 picture-card  | String  | false  |  picture  |

**type = textArea**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| placeholder  | 站位文本  | String  | false  | 请输入内容  |
| rows  | 	文本域行数  | Number  | false  | 2  |
| maxLength  | 	输入内容最大长度  | Number  | false  | 100  |

**type = cascader**

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| placeholder  | 站位文本  | String  | false  | 请选择内容  |
| multiple  | 	是否多选  | Boolean  | false  | false  |
| expandTrigger  | 	次级菜单的展开方式，可选 'click' 和 'hover'  | String  | false  | click  |
| changeOnSelect  | （单选时生效）当此项为 true时，点选每级菜单选项值都会发生变化  | Boolean  | false  | false  |
| customizeOptionsValueKey  | 自定义 options 中 的value字段  | String  | false  | value  |
| customizeOptionsLabelKey  | 自定义 options 中 的label字段  | String  | false  | label  |
| customizeOptionsChildrenKey  | 自定义 options 中 的children字段  | String  | false  | children  |

### 页面 && 表格 增加按钮权限

```javascript
  if (pageConfig.pageTableConfig) {
    // 页面 && 表格按钮权限 pageAuthorityArr来源于点击导航派发到页面对应的按钮权限数组
    pageConfig.pageTableConfig.pageAuthorityArr = pageAuthorityArr
  }
```

### 添加其他按钮

**页面中其他按钮的回调函数**

```javascript
  const pageBtn1ClickFun = (tableSelectedRowKeys) => {
    console.log('表格中多选选中的数据', tableSelectedRowKeys)

    // 业务逻辑

    // 更新表格数据
    pageRef.current.getTableDataFun()
  }
```

**表格中其他按钮的回调函数**

```javascript
  const tableBtn1ClickFun = (record) => {
    console.log('行信息', record)

    // 业务逻辑

    // 更新表格数据
    pageRef.current.getTableDataFun()
  }
```

**页面中其他按钮**

```javascript
  const renderPageBtn1Fun = () => {
    // Page页其他按钮的权限 如果按钮权限数组pageAuthorityArr中存在'其他按钮'则显示此按钮
    if (btnAuthorityFun(pageAuthorityArr, '其他按钮')) {
      return function (tableSelectedRowKeys) {
        // 返回的按钮 必须添加key属性
        return (
          <Button
            key={1}
            type="primary"
            onClick={() => {
              pageBtn1ClickFun(tableSelectedRowKeys)
            }}
          >
            其他按钮
          </Button>
        )
      }
    }
  }
```

**表格中其他按钮**

```javascript
  const renderTableBtn1Fun = () => {
    // 表格中其他按钮的权限 可结合src\assets\data\menuData.js中数据 梳理逻辑
    if (btnAuthorityFun(pageAuthorityArr, '其他按钮')) {
      return function (record) {
        // 如果'其他按钮'和行信息有权限关联 可拿到record判断 是否返回按钮
        // 返回的按钮 必须添加key属性 table中的其他按钮最好使用字符串作为key值 避免和组件内部按钮key冲突
        return (
          <Button
            key={'a'}
            type="text"
            onClick={() => {
              tableBtn1ClickFun(record)
            }}
          >
            其他按钮
          </Button>
        )
      }
    }
  }
```

```javascript
  if (pageConfig.pageTableConfig) {
    // Page页中其他按钮
    pageConfig.pageTableConfig.pageMoreButtonArr = [renderPageBtn1Fun()]

    // 表格中其他按钮
    pageConfig.pageTableConfig.tableMoreButtonArr = [renderTableBtn1Fun()]
  }
```

## 使用组件

```javascript
  return (
    <div>
      <Page onRef={pageRef} pageConfig={pageConfig}></Page>
    </div>
  )
```

## PageModal单独使用

## 示例代码

```javascript
import React, { memo, useState } from 'react'

import { Button } from 'antd'

import { PageModal } from 'page/children'

const OneTwo = memo(() => {
  const [isModalVisible, setIsModalVisible] = useState(false)

  /**
   *  两种使用方法
   *  一.自动交互
   *    1.新增：传入saveUrl即可
   *    2.修改：传入saveurl和itemId（行id）即可
   *    3.查看：传入itemId modalTitle为查看即可
   *
   *  二.手动交互
   *   1.新增：传入getFormDataFun函数 点击确定时回调 参数为表单获取数据
   *   2.修改：传入getFormDataFun函数 传入defaultFormData回显数据
   *   3.查看：传入defaultFormData回显数据 modalTitle修改为查看
   **/

  const pageModalConfig = {
    saveUrl: '/oneOne/',
    itemId: 1,
    modalTitle: '新增',
    modalItemArr: [
      {
        type: 'input',
        label: '姓名',
        field: 'name',
        placeholder: '请输入姓名'
      }
    ],
    defaultFormData: {
      name: '哈哈哈'
    },
    getFormDataFun(formData) {
      console.log(formData)
    }
  }

  const showModalFun = () => {
    setIsModalVisible(true)
  }

  const closeModalFun = (_, isRequestTableData) => {
    setIsModalVisible(false)
    // isRequestTableData 是否更新表格数据
  }

  return (
    <div>
      <Button type="primary" onClick={showModalFun}>
        打开弹窗
      </Button>
      {isModalVisible && (
        <PageModal
          isModalVisible={isModalVisible}
          pageModalConfig={pageModalConfig}
          onCloseModal={closeModalFun}
        ></PageModal>
      )}
    </div>
  )
})

export default OneTwo
```

## 代码详解

### 创建打开 \| 关闭弹窗控制条件

```javascript
 const [isModalVisible, setIsModalVisible] = useState(false)
```

### pageModalConfig（page->pageModalConfig中其他属性都可用）

| 属性  | 说明  | 类型  | 是否必填  | 默认值  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| saveUrl  | 保存 或 回显的url 用于自动交互时使用  | String  | false  | ——  |
| itemId  | 行id 用于自动交互时使用  | String 或 Number  | false  | ——  |
| defaultFormData  | 回显时传入组件内的数据 用于手动交互时使用  | Object  | false  | ——  |
| getFormDataFun  | 点击保存时回调的方法 参数为表单数据 用于手动交互时使用  | Function  | false  | ——  |

### 关闭弹窗回调函数

```javascript
  const closeModalFun = (_, isRequestTableData) => {
    setIsModalVisible(false)
    // isRequestTableData 是否更新表格数据
  }
```

## 使用组件

```javascript
  return (
    <div>
      <Button type="primary" onClick={showModalFun}>
        打开弹窗
      </Button>
      {isModalVisible && (
        <PageModal
          isModalVisible={isModalVisible}
          pageModalConfig={pageModalConfig}
          onCloseModal={closeModalFun}
        ></PageModal>
      )}
    </div>
  )
```

## PageSearch单独使用

## 示例代码

```javascript
import React, { memo } from 'react';

import { PageSearch } from 'page/children'

const OneThree = memo(() => {

  const pageSearchConfig = {
    // searchItemMarginRight: '50px',
    searchItemArr: [
      {
        type: 'input',
        label: '姓名',
        field: 'name',
        placeholder: '请输入姓名',
      },
      {
        type: 'input',
        label: '手机号',
        field: 'phone',
        placeholder: '请输入手机号',
      },
    ],
    getSearchDataFun(values) {
      console.log('搜索栏数据', values)
    },
    resetSearchDataFun() {
      console.log('点击重置按钮')
    },
  }

  return (
    <div>
      <PageSearch pageSearchConfig={pageSearchConfig}></PageSearch>
    </div>
  );
});

export default OneThree;
```

## 代码详解

### pageSearchConfig（page->pageSearchConfig中属性都可用）

## 使用组件

```javascript
  return (
    <div>
      <PageSearch pageSearchConfig={pageSearchConfig}></PageSearch>
    </div>
  )
```
