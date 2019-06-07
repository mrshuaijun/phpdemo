php
====
##### echo 输出
##### require_once() 引入脚本
##### include_once() 引入脚本
##### $arrayTest = array('0'=> '苹果'， '1' => '测试') 创建数组
##### $_GET('user') 获取get参数
##### $_REQUEST 获取所有请求方法的参数
##### json_encode(array('msg'=>'成功', 'errcode'=>'200')) 返回json数据
##### ('拼接 ' . '哈哈') 字符串拼接
##### mysql_connect("localhost:3306","root","root") 连接数据库
##### mysql_select_db("测试", $con) 选择数据库
##### mysql_query("set names 'utf8'") 设置编码
##### mysql_query("INSERT INTO user (name) VALUES (测试)") 执行sql语句
##### mysql_close($con); 关闭数据库
##### header("Content-type: application/json; charset=utf-8") 设置响应头

##### array_push($arr, array('msg'=>'成功', 'errcode'=>'200')) 追加到数组

# PDO操作数据库
php
```
<?php
header("Content-Type: text/html;charset=utf-8");
$dbms = "mysql";
$host = "localhost";
$dbName = "phptest";
$user = "root";
$pass = "root";
$dsn = "$dbms:host=$host;dbname=$dbName";
try{
	$dbh = new PDO($dsn,$user,$pass);
	echo "success连接成功";
	// foreach($dbh->query("SELECT * FROM user WHERE id=1") as $row){
		// print_r($row);
		
	// }
	$query = "insert into `user`(`name`, `realname`) values ('lau', 'chuanjun')";
	$res = $dbh->exec($query);
	echo "数据库添加成功, 受影响的行数".$res;
	$dbh = null;
}catch(PDOException $e){
	die("Error:". $e.getMessage()."</br/>");
}
?>

```

