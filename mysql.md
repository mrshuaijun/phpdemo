## 查询数据库
```
show databases;
```

## 使用数据库
```
use [数据库名字]
```
## 时间类型
##### DATE 日期 年-月-日
##### DATETIME 年-月-日 时-分-秒
##### TIME 时 分 秒
##### TIMESTAMP 时间戳
##### YEAR 只显示年份

## 查询数据
```
SELECT count(*) FROM db_test.t_student
where gender = 'M';
```

## 函数
```
count() // 查总数
min() //查最小值
max() // 最大值
sum() // 求和
sqrt() // 求平方根
rand() //得到随机数
concat() // 拼接字符串
```

## 条件筛选
```
// 筛选出 1998-01-01 到 1998-12-31 之间的数据
SELECT * from t_student
where birthdate >= '1998-01-01'
AND birthdate <= '1998-12-31';

SELECT * from t_student
where birthdate BETWEEN '1998-01-01' AND '1998-12-31'
// between和and需搭配使用
```

## 模糊查询
```
select * from t_student
where name like '王%'
// 查询王开头的数据

select * from t_student
where name like '%王'
// 查询王结尾的数据

select * from t_student
where name like '%王%'
// 查询带王的数据
```

## order by 排序
```
SELECT * FROM t_student
ORDER BY birthdate desc
// desc 倒序
// asc 正序

```
## 连表查询
```
SELECT t_student.id,t_student.name, t_class.class_name FROM t_student,t_class
WHERE t_student.class_id = t_class.class_id

// 左连接
SELECT t_student.id,t_student.name, t_class.class_name FROM t_student LEFT JOIN t_class
ON t_student.class_id = t_class.class_id

```