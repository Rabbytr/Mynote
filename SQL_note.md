## 创建表
create table "tablename"

("column1" "data type" [constraint],

"column2" "data type" [constraint],

"column3" "data type" [constraint]);

[ ] = optional

dataType:primary key	auto_increment

#### 几种常见的数据类型：

char(size) ：固定长度的字符串型。Size是圆括号中指定的参数，它可以由用户随意设置，但是不能超过255个字节。

varchar(size) ：变长度的字符串型。它的最大长度是由括号中的参数size设定的。

number(size)：数值型。最大数字的位数由括号中的参数size设置。

date ：日期数值型。

number(size,d) ：数值型。它的最大数字的位数由括号中的参数sieze设定，而括号中的参数d是设置小数点的位数。

----

## 删除表
drop table "tablename";

---

## select语句
```
select "col1"[,"col2",etc] from "tablename" [where "condition"];
如:
select password,id from users where id = 2017;
```
#### 高级
SELECT [ALL | DISTINCT] column1[,column2]

FROM table1[,table2]

[WHERE "conditions"]

[GROUP BY "column-list"]

[HAVING "conditions]

[ORDER BY "column-list" [ASC | DESC] ]

##### 在WHERE子句中可以有以下的条件选择：
* = 等于
* \> 大于
* < 小于
* <> 不等于

---

## 插入数据
insert into "tablename"

(first_column,...last_column)

values (first_value,...last_value);

[] = optional

---

## 更新数据
update "tablename"

set "columnname" = "newvalue"[,"nextcolumn" = "newvalue2"...]

where "columnname" OPERATOR "value" [and|or "column" OPERATOR "value"];

[] = optional  

如：
```
update users set password=99999 where id =2017;
```
---

## 删除记录
delete from "tablename"

where "columnname" OPERATOR "value" [and|or "column" OPERATOR "value"];

[ ] = optional

## 增加字段
alter table tname add cname ctype;

## 删除字段
alter table tname drop cname;

## 调整字段位置
alter table user modify id type first;
