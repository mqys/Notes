# basic SQL usage

SQL (Structured Query Language)

```
# 检索
SELECT

# 排序
ORDER BY (ASC | DESC)

# 过滤数据
WHERE (BETWEEN, IS NULL, != / <>) (AND, OR, IN, NOT) (LIKE)

# 通配符
% 任何字符, 任意次数
_ 单个字符
[] 字符集, 可以使用^来表示否定

# 数据处理函数
文本处理函数: LENGTH(), LOWER(), RTRIM()
日期时间处理函数: DATEPART()
数值处理函数: EXP(), SQRT()

# 聚集函数 (可对参数使用 ALL | DISTINCT)
AVG()
COUNT()
MAX()
MIN()
SUM()

# 分组数据
GROUP BY
HAVING (WHERE过滤行, HAVING过滤分组)

# 子查询
略

# 联结
内部联结(等值联结)
自联结
自然联结(每个列只返回一次, 用到的内部联结都是自然联结)
外部联结(包含没有关联行的行) (left, right, full)

# 组合查询
UNION

# 插入
INSERT
eg. INSERT INTO Customers(cust_id, cust_name) VALUES('111', 'jack');
复制表: SELECT * INTO CustCopy FROM Customers; 

# 更新和删除
UPDATE, DELETE
eg. UPDATE Customers SET cust_name = 'rose' WHERE cust_id = '111';

# 创建和操纵表
CREATE TABLE, ALTER TABLE(ADD / DROP COLUMN), DROP TABLE

# 视图
CREATE VIEW OrderView as SELECT ...

# 管理事务处理
COMMIT, ROLLBACK, BEGIN TRANSACTION

# 游标 CURSOR
在检索出的结果行中前进或后退一行或多行

# 约束  
ADD CONSTRAINT CHECK (...);

# 索引
CREATE INDEX cust_name_index ON Customers(cust_id);

# 触发器
CREATE TRIGGER ...
```