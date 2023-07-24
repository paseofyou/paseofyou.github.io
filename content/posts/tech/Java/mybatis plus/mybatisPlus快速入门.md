---
title: "第一章：对象的概念"
date: 2023-05-02T15:19:34+08:00
draft: false
weight: 10
---

## 简介

特性：

- 无侵入、损耗小、强大的 `CRUD `操作、支持 `Lambda` 形式调用、支持主键自动生成、支持 `ActiveRecord `模式、支持自定义全局通用操作、内置代码生成器、内置分页插件、分页插件支持多种数据库、内置性能分析插件、内置全局拦截插件

支持数据库：

- `MySQL`，`Oracle`，`DB2`，`H2`，`HSQL`，`SQLite`，`PostgreSQL`，`SQLServer`，`Phoenix`，`Gauss `，`ClickHouse`，`Sybase`，`OceanBase`，`Firebird`，`Cubrid`，`Goldilocks`，`csiidb`
- 达梦数据库，虚谷数据库，人大金仓数据库，南大通用(华库)数据库，南大通用数据库，神通数据库，瀚高数据库

框架架构

 ![mybatis-plus-framework](mybatisPlus%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/1648542591683561.jpg)

## 快速开始

准备操作：

- 拥有 `Java `开发环境以及相应 IDE、熟悉 `Spring Boot`、熟悉 `Maven`

- 准备一个`mysql`数据库，`Schema`脚本如下：

```sql
DROP TABLE IF EXISTS user;

CREATE TABLE user
(
    id BIGINT(20) NOT NULL COMMENT '主键ID',
    name VARCHAR(30) NULL DEFAULT NULL COMMENT '姓名',
    age INT(11) NULL DEFAULT NULL COMMENT '年龄',
    email VARCHAR(50) NULL DEFAULT NULL COMMENT '邮箱',
    PRIMARY KEY (id)
);
```

`Data `脚本如下:

```sql
DELETE FROM user;

INSERT INTO user (id, name, age, email) VALUES
(1, 'Jone', 18, 'test1@baomidou.com'),
(2, 'Jack', 20, 'test2@baomidou.com'),
(3, 'Tom', 28, 'test3@baomidou.com'),
(4, 'Sandy', 21, 'test4@baomidou.com'),
(5, 'Billie', 24, 'test5@baomidou.com');
```

- 初始化一个Springboot工程，