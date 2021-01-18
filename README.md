# ingTools 

**TBSP2.0**开发辅助插件（For IDEA），针对日常开发提供便捷支持。

IDEA版本要求：2017.3-2019.1

参考链接： [IDEA插件开发官方SDK](http://www.jetbrains.org/intellij/sdk/docs/welcome.html)

交流QQ群：`933819491`

> 注意：使用中，若出现问题请反馈至[wucp26649@hundsun.com](wucp26649@hundsun.com)或钉钉`26649`

## 1. 安装插件

> 本插件下载请移步至 [这里](https://plugins.jetbrains.com/plugin/13472-ingtools/)，建议下载**最新版本**

### 1.1 打开设置

![image-20200520202621568](README.assets/image-20200520202621568.png)

### 1.2 搜索本插件

![image-20200520154522227](README.assets/image-20200520154522227.png)

### 1.3 点击安装后重启即可

## 2. 功能介绍

### 2.1 代码跳转

> InterImplTestEnumProvider

#### 2.1.1 跳转关系

![image-20200520162702837](README.assets/image-20200520162702837.png)

> 以交易码为关联关系，实现各层间的连接

#### 2.1.2 如何使用？

初次使用需要配置交易码类：

![image-20200520145432487](README.assets/image-20200520145432487.png)

点击OK后，然后重新打开2.1.1图中任一类代码即可，**建议重启IDEA更好**。

配置好之后就是这样的：

接口类中：

![1572009099975](README.assets/1572009099975.png)

上面三种图标对应三种跳转关系，点击他们就能直接跳转了。

交易码枚举类中：

![1572009240293](README.assets/1572009240293.png)

req和resp的相互跳转：

![1572009495729](README.assets/1572009495729.png)

> 注意：可能有时候无法出现跳转图标，建议清理缓存并重启IDEA

### 2.2 IEnum重复code提示

> IEnumCodeRepeatedAnnotator

![1572009846994](README.assets/1572009846994.png)

> 仅针对实现了`IEnum`的枚举有效

### 2.3 生成类的field

> GenerateFields

对于类字段较多的情况，就可以这么玩：

![gif](README.assets/generateFields.gif)

> 从文档中复制字段定义内容，可直接生成类字段。三列分别对应字段名、注释、类型，注意选择分隔符是`Tab`还是`空格` ，其中，第二列不选，则模式注释是属性名，第三列可不选，则默认为`String·`类型

用法为在类体内单击右键，弹出菜单：

![1572053982685](README.assets/1572053982685.png)

### 2.4 枚举查找

> EnumFinder

提供本地快速枚举查找：
![1572053982686](README.assets/enumFinder.gif)

> 使用前需要配置本地枚举类jar包路径

### 2.5 字段对比

> CompareFields

需求经常改，字段总是变，都搞不清哪些字段动过了，看看这个吧：

![1572053982687](README.assets/compareFields.gif)

> 左右两栏分别为当前类中字段和文档列字段（当然，需要手动copy出来），点击Compare就能比出来谁多谁少了

### 2.6 元数据核查

> MetadataChecker

提供对req类中含`TValidator`字段的一键查询，结果会显示在表中，库中没有的记录租户号为`null`，使用前要配置好数据源。建议开发人员写完req类后，就进行此校验操作，从而尽量避免属性名重复。

用法：打开类后，右键选择菜单

![image-20200520205617123](README.assets/image-20200520205617123.png)

![1572053982688](README.assets/metadataChecker.gif)

![1572058900835](README.assets/1572058900835.png)

> 注意：入库操作，仅针对库中无此字段的情况，此操作仅仅是新增记录，**修改已有元数据不会执行更新操作**。表格编辑完后，若仍然处于焦点状态，此行数据不会被入库操作发现，需要点击其他地方先让表格失去焦点，再点击入库按钮。

另外：

> 这里仅是对单个req的元数据有出库操作，实际开发中不可能一个个req的去做，怎么对所有req类元数据出库操作呢？继续往下看**2.11**吧

注意，此功能需要配置数据库信息：

![image-20200520145829355](README.assets/image-20200520145829355.png)

### 2.7 CSV生成
> Generate CSV

#### 2.7.1 生成至类同目录

![1572059820480](README.assets/1572059820480.png)

> 在类文件上右键菜单，选择`Generate CSV`， 再选择类型，对应CSV文件就会在同目录下生成

#### 2.7.2 生成至指定目录

> 打开Project面板，点击目标目录后，再将光标置于类名处，右键生成，文件会直接生成在选中的目录下

![image-20200520201551516](README.assets/image-20200520201551516.png)

### 2.8 国际化文件生成
> Generate i18n File

#### 手动生成

![1572060115696](README.assets/1572060115696.png)

> 在错误枚举类上选择本功能，同目录下就就会生成对应`properties`文件。注意可能存在**编码问题**，此时只要将文件内容复制出来，覆盖到原国际化文件中即可

#### 自动生成

>  自动提示更新国际化文件需要配置*错误枚举类*和*国际化文件位置*

![image-20200520150103211](README.assets/image-20200520150103211.png)

当错误枚举类编辑时，会出现通知，点击`好的`就行啦

![image-20200520150300358](README.assets/image-20200520150300358.png)

### 2.9 交易码SQL文件生成
> Generate trCode insert sql

在交易码枚举类上执行，将各个枚举转换成对应的SQL插表语句，注意某些值需要根据需要自行修改

![1572060486796](README.assets/1572060486796.png)

### 2.10 字典SQL文件生成
> Generate comDict insert sql

系统字典不能满足需要的情况下，产品内部会定义其他枚举字典，其对应的SQL入库语句便可由此生成

![1572072315820](README.assets/1572072315820.png)

> 在含有字典枚举的**包** 上执行本操作，注意枚举名必须是`Gxxxxx`格式，且实现了`IEnum`接口

另外，鉴于`COM_DICT`表中有`REMARK`字段，强烈建议在枚举类中增加该属性以便生成SQL时，`REMARK`字段能够有此备注，若枚举类中无`remark`属性，则该SQL中`REMARK`字段值为此枚举类名（这样并没有什么意义）

![1572072787331](README.assets/1572072787331.png)

### 2.11 元数据批量导出
> Metadata Helper

前面2.6讲过对单个req类属性元数据的查询和导出操作，这里将展示对所有req类元数据的导出操作

![1572073432410](README.assets/1572073432410.png)

在req包上执行导出：
* Export exists metadata of Req：导出数据库中存在包下的Req类的metadata数据
* Check and export all metadata of Req：检验并导出数据库全部包下Req类的metadata，若有一个不存在，则会抛出错误，此法往往用于检验漏网之鱼

> 注意：只要有`TValidator`注解的属性，就会视为导出对象，使用时请严格遵守注解使用规范

### 2.12 SQL执行器
> SQL Executor

![1572074265639](README.assets/1572074265639.png)

> 原理：逐条执行SQL，每条语句执行互不影响执行结果，注意SQL必须是单行的。此功能常用于多次往数据库导入数据且不知道有哪些数据重复的场景，注意每行必须是完整的SQL，不能跨行

### 2.13 复制包下所有类名
> Copy all class name

![1572074696986](README.assets/1572074696986.png)

> 集中跑单测类时，不用一个个类名复制到`RunnerMain`中了，直接在测试类包上执行本操作即可，**注意去掉`RunnerMain`类自身**

### 2.14 模板代码生成

#### 2.14.1 生成实现类

> Generate Impl

![1572075513158](README.assets/1572075513158.png)

在**服务接口类**中按下`alt+insert`键，弹出选项：

* Generate Impl：生成实现类模板代码，格式如下，#XXX为占位符

```
// 500
```

#### 2.14.2 生成测试类

> Generate Test

* Generate Test：生成测试类模板代码，格式如下

```
// 500
```

>  操作时选择要实现的方法和指定生成文件所在的包即可，**注意要先配置交易码枚举类，见2.1.2**

若还想生成测试类的同时，建好csv路径，请添加配置：

![image-20200520150546593](README.assets/image-20200520150546593.png)

![image-20200520151329535](README.assets/image-20200520151329535.png)



### 2.15 Example分析
> Analyze Example

针对多人协作开发的场景，同条件查询可能写成多种情况

```java
//第一种：
UserExample example = new UserExample();
example.createCriteria()
	.andNameEqualsTo("A")
   	.andAgeEqualsTo(10)
    .andGenderEqualsTo("M");
//第二种：
UserExample example = new UserExample();
example.createCriteria()
	.andAgeEqualsTo(10)
    .andNameEqualsTo("A")
    .andGenderEqualsTo("M");
//第三种：
UserExample example = new UserExample();
example.createCriteria()
    .andGenderEqualsTo("M")
    .andAgeEqualsTo(10)
    .andNameEqualsTo("A");
//等等。。。
```

如上，其实都归为相同的条件查询，仅仅是组合顺序不同，这给建立表索引等带来一定困扰，逐个审查代码来统一似乎工作量太大。试试这个吧：

![1572076566353](README.assets/1572076566353.png)

![1572076589403](README.assets/1572076589403.png)

菜单栏选择`Analyze`，再选择`Analyze Example`，在弹出的选择框中选择DAO层（Entity，Example，Mapper所在包）的包和服务实现层的包（使用了Example作查询的类所在的包，一般为业务实现层）

![1572077195964](README.assets/1572077195964.png)

如上，各个Example的使用情况就统计出来了，针对同条件而不同顺序的语句，方便进行代码统一调整

* 红箭头节点：对应一类Example，子节点为为用到的查询条件（两个即以上的，单个的忽略），单击可直接复制实体类对应的建索引SQL，建议先调整好所有此类Example引用的代码语句再执行
* 绿箭头节点：某类Example的查询条件（两个及以上同时出现的），显示实为第一个子节点的查询条件组合顺序，单击可复制本条件组合的建索引SQL，子节点为具体的代码使用语句
* 蓝箭头节点：条件查询代码语句块，**点击可直接跳转到代码**

> 注意先调整好查询条件代码，再复制对应的索引SQL，否则无实际意义，选包时尽可能缩小包的范围，以加快执行速度

还有：

> 这个功能还不是很完善，如果你根据弹出的树状图，调整了代码，再点击树状图时可能出现卡死现象，因为没有设置代码监听来更新树状图，所以请直接关闭弹窗，再重新执行一遍`Analyze Example`

### 2.16 out.xml和in.xml中重复值提示

out.xml中：

![1573722387749](README.assets/1573722387749.png)

> 验重属性包括：`trCode`, `outCode`, `serviceId`，重复的项会有如图背景色，鼠标悬浮时会提示

---
in.xml中：

![image-20200520210712408](README.assets/image-20200520210712408.png)

> 验重属性包括：`trCode`


### 2.17 getXXX()null提醒

> ReqGetterCallWarningAnnotator

![1574153344795](README.assets/1574153344795.png)

![1574153494694](README.assets/1574153494694.png)



> 原理：判断属性上是否有`@TValidator(notNUll = true)`

### 2.18 生成ResultMap

> Generate ResultMap

![image-20200520173034493](README.assets/image-20200520173034493.png)

打开类后，按下快捷键`alt+insert`弹出选项

### 2.19 对象间属性复制

> Copy Fields' Value
>
> 告别BeanUtils#copyProperties

![image-20200520180439152](README.assets/image-20200520180439152.png)

按下`alt+insert`, 先`Copy Fields' Value`

![image-20200520180500877](README.assets/image-20200520180500877.png)

弹出属性选择框，选择你要复制的属性（`Ctrl+A`可全选），然后输入源对象名称，OK即可

![image-20200520180846568](README.assets/image-20200520180846568.png)

### 2.20 生成req和resp类

> Generate Req and Resp

![image-20200520200227441](README.assets/image-20200520200227441.png)

Name为类名，可在前用`.`设置包名，注意类名必须是Req后缀结尾，若不是则会自动补上Req后缀，如图；

![image-20200520200500386](README.assets/image-20200520200500386.png)

结果：

![image-20200520200517471](README.assets/image-20200520200517471.png)

### 2.21 接口文档生成（Markdown）

> Generate API Doc

在接口类或包上执行

![image-20200520193304417](README.assets/image-20200520193304417.png)

> 需要配置数据库连接，用于获取元数据相关的数据

结果预览：

![image-20200520193613028](README.assets/image-20200520193613028.png)

## 更多

> 未尽事宜请联系作者咨询，欢迎提出宝贵意见和反馈！

