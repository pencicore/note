# 快速入门

**官网网址**：https://baomidou.com/introduce/



### 部分理解

- MyBaitsPlus是对MyBaits的进一步**封装**，他将单表crud常用的操作替我们实现了出来。节省了开发时间和代码量。同时，使用MyBaitsPlus利用泛型规范了一张表对应一个实体类，并为实体类提供了实用得注释。在一定程度上使得代码更加规范，更易读
- 在数据库表对应得Java实体类中，默认``id``为主键



### 代码实现

##### maven引入

在maven中添加以下内容即可引入MyBaitsPlus依赖

```json
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.5.3.1</version>
        </dependency>
```

##### 继承BaseMapper<>接口

BaseMapper中定义了对单表常用得crud函数，并通过指定泛型确定对应表名和字段名

这样即使该接口什么都没写，但该接口也有与表对应得crud函数

```java
package com.itheima.mp.mapper;

import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import com.itheima.mp.domain.po.User;

public interface UserMapper extends BaseMapper<User> {
}

```



### 常用注解

##### @TableName

> 用于指定表名

**使用场景**：

当实体类名与表名不对应时，可以用@TableName("name_table")将该Java类对应得表名修改为name_table

##### @TableId

> 用于指定表中得主键字段信息

**使用场景**： 

1. 当实体类中主键字段名与数据库主键字段名不相同时，可以用``@TableId(value=“id”)``*（只有value可以省略）*将该字段对应得主键字段改为id
2. MyBaitsPlus中主键在不指定值时默认使用雪花算法不重复随机出一个long long类型得正整数。
   当业务逻辑需要id自增时，可以通过用``@Table(type="AUTO")``设置id为自增。也可以将type设置为``ASSIGN_ID``表示使用雪花算法生成id，设置为``INPUT``表示通过set方法自行输入

##### @TableField

> 用于指定表中得普通字段信息

**使用场景**：

1. 成员变量名与数据库段名不一致或发生冲突，通过``@TableField(value="username")``*（只有value时可省略）*将该字段对应得段名改为username
2. 成员变量不是数据库字段，通过``@TableField(exist=false)``设置在crud操作时将该字段忽略



### 常用配置

![image-20240718204309432](图片\MyBaitsPlus常用配置.jpg)

