视图\(html+css+js\)模板  
数据\(mysql\)      存储数据的容器或者逻辑  
后台语言\(php\)     组织者  
b/s架构的应用

http是一种无状态协议，不会帮你记录任何客户端和服务器的连接状态  
php md5加密md5\(""\)32位字符串 
`where type="something"` 只选择某类型
`order by something desc`倒序排序某类型
`order by something desc 0-3`倒序排序某类型只显示0到3
`empty(var)`判断是否为空
`explode()`把字符串打散为数组
`echo phpinfo()`返回php信息  
`file_get_contents("demo.html")`以字符形式返回内容
`file_put_contents("demo.html")`以字符形式插入内容

`perg_match()`
单入口文件 安全 可调度 
模板引擎:使用户界面与业务数据（内容）分离而产生的，它可以生成特定格式的文档，用于网站的模板引擎就会生成一个标准的HTML文档。
`$_REQUSTE['']`接受无论post,get
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

```
mvc 部署目录
├─comple 模板引擎(自动生成)
├─libs 配置文件目录
│ ├─smarty 模板引擎
│ ├─db.class 配置函数，数据库操作核心函数
│ ├─route 单文件入口
├─module 模块目录
│ ├─admin 后台模块目录
│ ├─index 前台模块目录
├─template 前台目录
│ ├─admin 后台模版目录
│ ├─index 前台模版目录
├─index.html 入口
```


#### 典型的Web MVC流程：

1.Controller截获用户发出的请求；  
2.Controller调用Model完成状态的读写操作；  
3.Controller把数据传递给View；  
4.View渲染最终结果并呈献给用户。

core.php
```php

<?php

class db{
    //配置项
    public $hostname="localhost"; //初始化服务器地址
    public $dbname="1603class"; // 数据库名
    private $username="root"; //用户名
    private $password=""; //用户密码
    public $tablename=""; //要操作的表格的名称、默认空
    private $connect; //连接数据库
    public $fileds;  //保存整理的sql操作语句

    /*初始化函数
     * @param  string  要操作的数据库的表名，必须传参
     * */
    function __construct($tablename)
    {
        if(!isset($tablename)){
            echo "请传入您要操作的表名";
            exit;
        }
        $this->tablename=$tablename;
        $this->config();
    }

    /*连接数据库
     * */
    public function config(){
        $this->connect=mysqli_connect($this->hostname,$this->username,$this->password,$this->dbname);
        if(mysqli_connect_error()){
            echo "连接 MYSQL 失败";
            $this->connect->close();
            exit;
        };
        $this->connect->query("set names utf8");
        $this->fileds['filed']=$this->fileds['filed']?$this->fileds['filed']:"*";
        $this->fileds['where']=$this->fileds['order']=$this->fileds['limit']="";
    }

    /*
     * @param    string  sql  可以传入sql语句
     * @param    string  key  查找的字段名
     * @example  select('name')
     *           select('name,sex')
     *           select('select * from table');
     * @return   返回一个数组，数组中保存查询到的结果
     * */
    public function select($opt=""){
        $sql=empty($opt)?"select ".$this->fileds['filed']." from ".$this->tablename." ".$this->fileds['where']." ".$this->fileds["order"]." ".$this->fileds["limit"]:$opt;

        if(strpos($sql,"select")===false){
            $sql="select ".$sql." from ".$this->tablename." ".$this->fileds['where'];

        }

        $result=$this->connect->query($sql);

        while($row=$result->fetch_assoc()){
            $arr[]=$row;
        }

        return $arr;
    }

    /*@param    string  查找的字段
      @example  filed('name,age')  【select】
      @example  filed("name='zhangsan',age='12'") 【update】
      @example  filed("name='zhangsan';age='12'")  【insert】
      @example  filed("name='zhangsan'")  【update,insert】
    */
    public function filed($opt=""){
        $sql=$opt=$opt?$opt:"*";


        if(strpos($sql,";")){
            $keys="";
            $values="";
            $arr=explode(";",$sql);
            foreach($arr as $v){
                $temp=explode("=",$v);
                $keys.=$temp[0].",";
                $values.=$temp[1].",";
            }

            $keys=substr($keys,0,-1);
            $values=substr($values,0,-1);

            $sql="(".$keys.") values (".$values.")";
        };

        $this->fileds['filed']=$sql;
        return $this;
    }

    /*
     * @param   [string]
     * @example where('id=1')
     * @return  当前对象的指针
     * */
    public function where($opt=""){
        $this->fileds["where"]=$opt==""?"":"where ".$opt;
        return $this;
    }
    /*
         * @param    string
         * @example  order("age desc")
         * @return   当前对象的指针
         * */
    public function order($opt=""){
        $this->fileds["order"]=$opt==""?"":"order by ".$opt;
        return $this;
    }

    /*
     * @param    string (index,length)
     * @example  limit("0,2")
     * @return   当前对象的指针
     * */
    public function limit($opt=""){
        $this->fileds["limit"]=$opt==""?"":"limit ".$opt;
        return $this;
    }

    /*
     * @param   [string](sql,string)
     * @example update();
     * @example update("name='zhangsan' , age='12'");
     * @example update("name='zhangsan' , age='12' where id=1");
     * @example update("update table set name='zhangsan',age='12' where id=1");
     * @return  操作影响的行数 -1表示执行sql语句失败
     * */
    public function update($opt=""){
        $sql=empty($opt)?"update ".$this->tablename." set ".$this->fileds["filed"]." ".$this->fileds['where']:$opt;

        if(strpos($sql,'update')===false){
            if(strpos($sql,"where")){
                $sql="update ".$this->tablename." set ".$sql;
            }else{
                $sql="update ".$this->tablename." set ".$sql." ".$this->fileds['where'];
            }

        }

        $this->connect->query($sql);
        return $this->connect->affected_rows;
    }

    /*
     * @param    string  sql
     * @param    string  string
     * @example  delete();
     * @example  delete('id=3');
     * @example  delete("delete from table where name='zhangsan'");
     * @return   操作影响的行数 -1表示执行sql语句失败
     * */
    public function delete($opt=""){
        $sql=empty($opt)?"delete from ".$this->tablename." ".$this->fileds['where']:$opt;


        if(strpos($sql,"delete")===false){
            $sql="delete from ".$this->tablename." where ".$sql;
        }

        $this->connect->query($sql);

        return $this->connect->affected_rows;
    }

    /*
     * @param   [string](sql,string)
     * @example insert();
     * @example insert("name='zhangsan'");
     * @example insert("name='zhangsan' ; age='12'");
     * @example insert("insert into table (name,age) values ('zhangsan','12')")
     * @return  操作影响的行数 -1表示执行sql语句失败
     * */
    public function insert($opt=""){

        if(empty($opt)){
            if(strpos($this->fileds["filed"],"=")){
                $temp=explode("=",$this->fileds["filed"]);
                $sql="insert into ".$this->tablename." (".$temp[0].") values (".$temp[1].")";
            }else{
                $sql="insert into ".$this->tablename." ".$this->fileds['filed'];
            }
        }else{
            $sql=$opt;
        }


        if(strpos($sql,"insert")===false){
            if(strpos($sql,";")){
                $this->filed($sql);
                $sql="insert into ".$this->tablename." ".$this->fileds["filed"];
            }else if(strpos($sql,"=")){
                $temp=explode("=",$sql);
                $sql="insert into ".$this->tablename." (".$temp[0].") values (".$temp[1].")";
            }
        }

        $this->connect->query($sql);

        return $this->connect->affected_rows;
    }

}
/*
 * //测试
$db=new db("stu");
//    $arr=$db->select("select name from stu where id=0");
//    $arr=$db->insert("insert into table (name,age) values ('zhangsan','12')");
//    $arr=$db->where("id=0")->delete();
$arr=$db->filed("age='10'")->where("id=10")->update("name='zhangsan'");

var_dump($arr);*/



?>
 ```
