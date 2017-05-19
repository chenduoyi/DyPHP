# 字符串函数
## substr_count
记录某个字符在字符串中出现的次数
$str=' yauiopajaql';
echo substr_count($str,'a');
// 输出3, 表示a出现了3次

## strpos
判断字符串中是否包含某值
$pos = strpos($mystring, $findme);
$pos 要用 === false 表示不包含