## POSTGRES 基本命令


- 帮助 `help`
- `\h 加上命令 直接显示这个命令怎么用`

### 对数据库的操作
- 创建新的用户  `CREATE USER user_name;`
- 增加  `CREATE DATABASE db_name;`
- 删除  `DROP DATABASE db_name;`
- 修改 `ALTER DATABASE db_name RENAME TO new_db_name;`
- 显示所有的数据库 `\l *e` 展示以e结尾的数据库 * 表示任意字符  ? 问号表示单个字符  `\l `是表格显示
- 改变显示数据库的格式 变为逐行显示 `\x`


### 对数据表的操作


数据表的组成
| 标题(字段名) | Attribute (COLUMN) |
| ------------ | ------------------ |
| 记录         | Tuple  (ROW)       |
| 记录         | Tuple              |


- 连接数据库 `\c db_name`
- 创建数据表 `CREATE TABLE IF NOT EXISTS table_name(column1 varchar(10), column2 varchar(20));`
- 删除数据表 `DROP TABLE IF EXISTS table_name;`
- 修改数据表 `ALTER TABLE IF EXISTS table_name RENAME TO new_table_name;`
- 

## 常用的指令

**很重要 必须牢记 并熟练使用**

- `\t` 只显示 记录 而 不显示标题
- 查询 `SELECT * FROM db_table;`
- 插入 `INSERT INTO db_table (字段) VALUES (字段对应的记录), (字段对应的记录) ; `*逗号隔开插入多个数据*
- 删除 `DELETE FROM db_table WHERE 条件`
- 更新 `UPDATE films SET kind = 'Dramatic' WHERE kind = 'Drama';`
- **这里有个技巧 就是 在修改和删除之前 先查询一下**
- 



### 关系型 数据表知识
*图片来自 oeasy 老师的 postgres 教程*


关系(relation)表结构 就是二维表
![关系型数据表](https://doc.shiyanlou.com/courses/uid1190679-20220417-1650181142426)

![数据表简单表示](https://doc.shiyanlou.com/courses/uid1190679-20220417-1650185174604)

关系 指的是 什么关系？

行和列构成的
关系(relation)


横着的

- 叫行(row)
- 元组(tuple)
- 记录(record)


竖着

- 叫列(column)
- 领域(field)
- 属性(attribute)


简单地说  竖着的叫 字段  横着的 叫 记录  
每行数据都是一个2元组(2-tuple)



SQL 分类
![SQL 分类](https://doc.shiyanlou.com/courses/uid1190679-20220421-1650505507033)


**DDL 主要操作数据库\数据表  DML 主要操作 数据表**


<ul>
<li>DDL(Data Definition Language) 数据定义语言<ul>
<li>CREATE,DROP,ALTER等等</li>
<li>DDL命令会影响整个数据库或表结构</li>
<li>控制宝库和宝箱结构</li>
</ul>
</li>
<li>DML(Data Manipulate Language) 数据操作语言<ul>
<li>INSERT、DELETE、UPDATE和SELECT等等</li>
<li>但DML命令会影响表中的一个或多个记录</li>
<li>在具体结构里面填充数据</li>
<li>控制宝箱里面的宝贝</li>
</ul>
</li>
</ul>



## 脚本相关


