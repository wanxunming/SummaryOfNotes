### Apex 编程入门：

#### 1.数据类型：（变量的命名规则：1、小写字母开头 2、驼峰命名）

Integer：整数（32位）

Long：长整数（64位）

Double：小数（64位）

Decimal：（任意的精度）

String：（使用单引号的字符串）

Boolen：（true && false）

Bold：（二进制数据，只有在处理文档时使用）

Date	Time	Datetime

Id



#### 2.编写Apex触发器

触发器定义以trigger 关键字开头。然后是触发器的名称、触发器关联的 Salesforce 对象以及触发条件。触发器包含以下语法：

```Apex
trigger TriggerName on ObjectName (trigger_events) {
   code_block
}
```

