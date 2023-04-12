## POSTGRES 基本命令


- 帮助 `help`
- `\h 加上命令 直接显示这个命令怎么用`

### 对数据库的操作
- 创建新的用户  `CREATE USER user_name;` 
  - `psql -U postgres -c "CREATE USER blog WITH PASSWORD '123456';"`

- 新加一个表 属于 某个用户`psql -U postgres -c "CREATE DATABASE blog OWNER blog ENCODING 'UTF8';"`


- 增加  `CREATE DATABASE db_name;`
- 删除  `DROP DATABASE IF EXISTS db_name;`
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
- 插入 `INSERT INTO db_table (字段, 字段) VALUES (字段对应的记录), (字段对应的记录) ; `*逗号隔开插入多个数据*
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

 `\i 文件`  从文件中执行命令 *(import)*

 **注意在 windows 下 需要用正斜杠....**

 `postgres=# \i C:/Users/IT/Desktop/temp/test.sql` 还是要把 `linux` 学好 [狗头]


`\! [command]              在 shell中执行命令或启动一个交互式shell`


`\e [FILE] [LINE]       使用外部编辑器编辑查询缓存区(或文件)` 在`shell`里面直接编译 文件  这个可以用 尤其是在 windows 里面。*(edit)*



`psql`是`PostgreSQL` 的交互式客户端工具。
`\? options` 显示 psql 命令的帮助 

`-f, --file=文件名        从文件中执行命令然后退出`

在 windows 下 操作 
`C:\Users\IT>psql -U postgres -f C:/Users/IT/Desktop/temp/test.sql`


**在 windows 下面执行 postgres 相关的指令的时候 都是 命令 -U postgres**  指定到特定的超级管理员 



## 数据库的转储备份


<ul>
<li>有三种方法<ul>
<li>sql dump(转储)</li>
<li>文件系统层面的备份</li>
<li>持续文档化</li>
</ul>
</li>
<li>我们先看看这个sql dump(转储)</li>
</ul>



备注 以下都是 在 `windows` 下执行 


sql dump(转储) 

备份


`pg_dump -U postgres oeasydb > oeasydb.sql`

恢复


`psql -U postgres oeasydb < oeasydb.sql`


`psql -U postgres --set ON_ERROR_STOP=on dbname< dumpfile` 设置恢复的时候 遇到错误就不执行 



**可以加上参数
让本次恢复过程作为一个事务(Transaction)
要么全做
要么不做**

`psql -U postgres -1 dbname < dumpfile`


`psql -U postgres --single-transaction dbname < dumpfile`


在恢复的时候 必须保证这个数据库要存在(其他名称也可以 其实就是执行 SQL  语句)


复制命令

`COPY login FROM stdin;`


`111    222`


`\.`


**导出数据表**


<ul>
<li>然后执行COPY命令<ul>
<li>列之间的分割符是<kbd>Tab</kbd></li>
<li>行之间的分隔符是<kbd>回车</kbd></li>
<li>结束输入的分隔符是<code>\.</code></li>
</ul>
</li>
</ul>

oeasydb=# \h COPY
命令：       COPY
描述：       在档案和数据表间复制数据
语法：
COPY 表名 [ ( 列名称 [, ...] ) ]
    FROM { '文件名' | PROGRAM '命令' | STDIN }
    [ [ WITH ] ( 选项 [, ...] ) ]
    [ WHERE 条件 ]

COPY { 表名 [ ( 列名称 [, ...] ) ] | ( 查询 ) }
    TO { '文件名' | PROGRAM '命令' | STDOUT }
    [ [ WITH ] ( 选项 [, ...] ) ]

选项可以是下列内容之一:

    FORMAT 格式_名称
    FREEZE [ 布尔 ]
    DELIMITER '分隔字符'
    NULL '空字符串'
    HEADER [ 布尔 | MATCH ]
    QUOTE '引用字符'
    ESCAPE '转义字符'
    FORCE_QUOTE { ( 列名称 [, ...] ) | * }
    FORCE_NOT_NULL ( 列名称 [, ...] )
    FORCE_NULL ( 列名称 [, ...] )
    ENCODING 'encoding_name(编码名)'


带标题复制 `oeasydb=# COPY login TO  'E:/wd-brucechen/database_bak/bakagain.csv' WITH CSV HEADER TRUE;`一般导出成 csv 文件格式。

`psql -U postgres -c, --command=命令       执行单一命令(SQL或内部指令)然后结束`


**导入数据表**

`COPY login FROM file WITH CSV HEADER;`


在数据库中 使用 `SELECT` 被称作 投影， `SELECT`出来的默认是不去重复的，加上`DISTINCT` 就可以去重 `SELECT DISTINCT name FROM COMPANY;`  


