当业务上需要两个数组进行合并时, 
有一个函数 array_merge, 还有一个是数组运算符 +, 
这两个处理方法情况是不一样的, 具体情况是如下:
首先, 一个前提条件是, array_merge 与 数组联合( 数组 +) 运算, 都是对数组进行操作的, 
也就是说传入的参数都必须是数组, 如果不是数组, 就会出问题!
```
$a1 = null;
$a2 = array(1,2,3,4,5);
$a3 = array('a'=>'aaa','b'=>'bbb','c'=>'ccc');
$a4 = array('a'=>'AAA','bbb','ccc');

$arr = array_merge($a1, $a2); //---> null
$arr = $a1 + $a2; //--->fatal error
```
对于array_merge来说, 比如说是null, 字符串等其他类型, 合并时会一个warning级别的错误
```Warning: array_merge(): Argument #1 is not an array in D:\xampp\htdocs\test\index.php on line 12```
得到的结果是null

对于联合运算来说, 如果不是数组, 会报fatal错误, 致命错误, 中断执行了
```Fatal error: Unsupported operand types in D:\xampp\htdocs\test\index.php on line 13```
即, 传递了不支持的数据类型

解决办法, 在不确定参数的类型时, 可以使用(array)转换一下数据类型, 保证传进去的参数一定是数组, 就不会出错了.
```
$arr = array_merge((array)$a1, (array)$a2);  //--->Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 ) 
$arr = (array)$a1 + (array)$a2;  //--->Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 )
 ```

在解决了数据类型的问题之后, 再来看, array_merge 与 数组联合+ 两者之间的区别
常用的array_merge, 是后面的覆盖前面的, 关联键名时, 即字符串为键名时, 后面数组的值会覆盖前面的. 
如果是索引数字键时, 后面的不会覆盖前面的, 会附加到后面. 如, 左边有, 0=>'aaa', 右边也有0=>'bbb', 
最终会变成, 0=>'aaa', 1=>'bbb', 右边的那个相同的键会往后面继续加进来.
示例:
```
$a1 = array('a');
$a2 = array(1,2,3,4,5);
$a3 = array_merge((array)$a1,(array)$a2);
print_r($a3);
Array ( [0] => a [1] => 1 [2] => 2 [3] => 3 [4] => 4 [5] => 5 ) 
```
键名0已经存在, 但不会覆盖, 左边用了0, 右边的就从1开始索引, 变成从1 索引到5了.
```
$a1 = array('a'=>'aaaa');
$a2 = array('a'=>'bbbb',1,2,3,4,5);
$a3 = array_merge((array)$a1,(array)$a2);
print_r($a3);
Array ( [a] => bbbb [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 ) 
```
关联键名, a, 同时存在, 后面的覆盖前面的, 所以 a的值, 变成了bbbb了, 其余的不影响

数组联合, 即 + 运算, 把右边的数组, 附加到 左边的数组, 
如果左边本身就有的键名(不管是索引键名0,1,2,3, 还是,关联键名'a','b','c'), 
只要左边已经存在了,  就以左边自己的为主, 右边的忽略;

最后附带说一下, 
索引数组 - 带有数字索引的数组
关联数组 - 带有指定键的数组


