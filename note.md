# php 笔记
Nginx报 No input file specified. 的问题解决之路
去掉目录中的.user.ini，访问正常！

## mb_detect_encoding
/* 使用当前的 detect_order 来检测字符编码 */
echo mb_detect_encoding($str);


## ord
(PHP 4, PHP 5)
ord — 返回字符的 ASCII 码值
说明
int ord ( string $string )
返回字符串 string 第一个字符的 ASCII 码值。
该函数是 chr() 的互补函数。

## chr
将ASCII码转换回字符串

## No input file specified.
Nginx报 No input file specified. 的问题
去掉目录中的.user.ini，访问正常！

## 判断是否是在微信中访问
$user_agent = $_SERVER['HTTP_USER_AGENT'];
if (strpos($user_agent, 'MicroMessenger') === false){
    header("Content-type: text/html; charset=utf-8");
    echo '请在微信中打开';
    die();
}