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

# 继承 extends
##### class 类名 extends 父类
## 成员属性
##### 变量修饰符 public private protected
##### self parent

## 对象中成员的访问
```
$引用名 = new 类名
$引用名->成员属性 = 赋值 // 对象属性赋值
echo $引用名-> 成员属性 // 输出对象的属性
$引用名->成员方法(参数) // 调用对象的方法
```

## 特殊对象引用$this
```
<?php
    /**
        类的声明
    */
    class Person {
        public $age;
        public function say($word){
            echo "she say {$word}";
        }
        public function info(){
            $this -> say("Hi");
            return $this -> age;
        }
    }
    $xiaohong = new Person();
    $xiaohong -> age = 22;
    $age = $xiaohong -> info();
    echo $age;
?>
```

## 析构函数
```
<?php
    /**
    * 测试构造方法和析构方法
    */
    class Person {
        public function __construct($name,$age) {
            echo('hello'.$name);
            echo "<hr>";
            $this -> age = $age;
            $this -> name = $name;
        }
        public function data(){
            return $this -> age;
        }
        public function __destruct() {
            // 用途 可以进行资源的释放 如 数据库关闭 读取文件的关闭
            // 对象被销毁的时候执行
            echo "bye bye {$this -> name} <br>";
        }
    }

    new Person('first', 30);
    new Person('second', 30);
?>
```

## 魔术方法 

```
<?php
    /**
    * 学习 public private protected
    */
    class Person {
        private $x = 1;
        private $name = "xiaoming"; // 公有属性
        private $age = 27; //私有属性
        protected $money = 10; //受保护的

        // 私有成员方法 不能在类外部直接访问
        private function getAge() {
            return $this -> age;
        }
        // 被保护的成员方法 不能在类的外部直接访问
        protected function getMoney() {
            return $this -> money;
        }

        public function userCard() {
            echo "name-> ".$this -> name." age->".$this -> getAge()." money-> ".$this -> getMoney();
        }
        public function __set($key, $value) {
            // 魔术方法的set 只针对保护的变量 和私有的变量
            if($key = "name" && $value = "laowang") {
                $this -> name = "xiaowang";
            }
        }
        public function __get($key) {
            if ($key == "age") {
                return "girl not tell you";
            }
        }
        public function __isset($key) {
            if ($key == "age") {
                return "private age";
            }
        }
        public function __unset($key) {

            if ($key == "age") {
                return;
            }
        }
    }
    $xw = new Person();
    $xw -> name = "laowang";
    // echo $xw -> userCard();
    // echo $xw -> age;
    // echo isset($xw -> age);
    unset($xw -> x);
    echo $xw -> x;
?>
```

# 重载和重写
```
<?php
    /**
        父类
    */
    class Person {
        public $name;
        private $age;
        protected $money;
        function __construct($name,$age,$money){
            $this -> name = $name;
            $this -> age = $age;
            $this -> money = $money;
        }

        public function cardInfo() {
            echo "name-> ".$this -> name." age->".$this -> age." money-> ".$this -> money;
        }
    }

    class Yellow extends Person {
        function __construct($name,$age,$money) {
            parent::__construct($name,$age,$money);
        }
        public function cardInfo($pp = "") {
            parent::cardInfo();
            echo $pp;
        }
        public function test(){
            echo $this -> money;
        }
    }

    $s = new Yellow("小王",22,100);
    $s -> cardInfo(1111);
?>
```
# 接口和抽象类
```
<?php 
// 1.接口声明的关键字是interface
// 2.接口可以声明常量 也可以是抽象方法
// 3.接口中的方法都是抽象方法 不用abstract去再次定义
// 4.接口不能被实例化 需要一个类实现它
// 5.一个类不能继承多个类 一个类可以实现多个接口
    interface Person {
        const NAME = "xiaowang";
        public function run();
        public function eat();
    }
    interface Study {
        public function study();

    }

    class Student implements Person,Study {
        const data = 3.234;
        public function run(){
            echo "running";
        }
        public function eat(){
            echo "eating";
        }
        public function study(){
            echo "study";
        }
        public static function test(){
            echo self::data."<br>";
        }
    }
    $xw = new Student();
    Student::test();
    echo Student::data;
 ?>

```