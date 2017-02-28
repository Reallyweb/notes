视图\(html+css+js\)模板  
数据\(mysql\)      存储数据的容器或者逻辑  
后台语言\(php\)     组织者  
b/s架构的应用

http是一种无状态协议，不会帮你记录任何客户端和服务器的连接状态  
php md5加密md5\(""\)32位字符串  
echo phpinfo\(\);返回php信息  
主键：快速检索

```css
* {
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
```

当你设置一个元素为 box-sizing: border-box; 时，此元素的内边距和边框不再会增加它的宽度。让有边框的盒子正常使用百分比宽度。  
分类表

| id | 分类的名称 | 父分类 | 分类的地址 |
| :--- | :--- | :--- | :--- |
| 1 | 女装 | 0 | url |
| 2 | 新闻 | 0 | url |

内容表

| id | 分类的id | 标题 | 内容 | 图片地址 |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 内裤 | 文字 | url |
| 2 | 1 | 内衣 | 文字 | url |
| 3 | 2 | 习大大 | 文字 | url |

详情表

# MVC\(编程架构\)

MVC\(model模型 view视图 controller控制器\)

* 模型Model – 管理大部分的业务逻辑和所有的数据库逻辑。模型提供了连接和操作数据库的抽象层。
* 控制器Controller - 负责响应用户请求、准备数据，以及决定如何展示数据。
* 视图View – 负责渲染数据，通过HTML方式呈现给用户。
![](/assets/web_mvc.gif)

#### 典型的Web MVC流程：

1.Controller截获用户发出的请求；  
2.Controller调用Model完成状态的读写操作；  
3.Controller把数据传递给View；  
4.View渲染最终结果并呈献给用户。

core.php
```php
<?php 

   class db{
        public $hostname="localhost";//初始化服务器域名
        public $dbname="1603class";// 数据库名称
        private $username="root";
        private $password="";
        public $tablename="";  //要操作的表格的名称
        private $connect; //连接db
        public $files;  //保存一系列sql语句组合

//        实例化db的时候可以传参数，表名
        function __construct($tablename)
        {
            if(!isset($tablename)){
                echo "请传入您要操作的表名";
                exit;
            }
            $this->tablename=$tablename;
//            连接数据库
            $this->connect=new mysqli($this->hostname,$this->username,$this->password,$this->dbname);
            $this->connect->query("set names utf8");

//            初始化参数
            $this->files['filed']=$this->files['filed']?$this->files['filed']:"*";
            $this->files['where']="";

        }

        public function select($opt=""){
//            组装sql语句
            $sql=$opt===""?"select ".$this->files['filed']." from ".$this->tablename." ".$this->files['where']:"";

//            执行sql语句
            $result=$this->connect->query($sql);

//            保存查询到的每一行数据到数组中
            $arr=array();
            while($row=$result->fetch_assoc()){
                $arr[]=$row;
            }

            return $arr;
        }

//        $this->files['filed'] 表示查找谁 select与from中间的
        public function filed($opt=""){
//            $sql=$opt===""?"*":$opt;
            $sql=$opt=$opt?$opt:"*";
            $this->files['filed']=$sql;
            return $this;
        }

//      $this->files['where']  表示在那  where
        public function where($opt=""){
            $this->files["where"]=$opt==""?"":"where ".$opt;
            return $this;
        }

    }

$db=new db("stu");
$arr=$db->filed()->where("id=46")->select();
var_dump($arr);

 ?>
 ```
