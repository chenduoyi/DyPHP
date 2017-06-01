//cURL get方式获取网页内容
function jielu_curl_get($url) {
    //创建一个新cURL资源
    $ch = curl_init();
    //设置url
    curl_setopt($ch, CURLOPT_URL, $url);
    //设置header头信息不以数据流输出, (即不要输出header头信息)
    curl_setopt($ch, CURLOPT_HEADER, false);
    //设置返回方式是直接输出还是作为信息流返回
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    //模拟浏览器访问(用于解决'未将对象引用设置到对象的实例。')
    //curl_setopt($ch, CURLOPT_USERAGENT, $_SERVER['HTTP_USER_AGENT']);
    //模拟浏览器来源网站
    //curl_setopt($ch, CURLOPT_REFERER, 'http://www.baidu.com');
    //执行会话
    $data = curl_exec($ch);
    //关闭cURL会话
    curl_close($ch);
    //返回数据
    return $data;
}

//cURL post方式获取网页内容
function jielu_curl_post($url, $post) {
    //创建一个cURL资源
    $ch = curl_init();
    //设置url
    curl_setopt($ch, CURLOPT_URL, $url);
    //设置header头信息
    curl_setopt($ch, CURLOPT_HEADER, false);
    //设置请求方式为post
    curl_setopt($ch, CURLOPT_POST, true);
    //设置post传参
    curl_setopt($ch, CURLOPT_POSTFIELDS, $post);
    //设置返回方式是直接输出还是作为信息流返回
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    //设置http头字段数组
    // curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type:application/x-www-form-urlencoded;charset=utf-8', 'Content-length:'.strlen($post)));
    //模拟浏览器来源网站
    //curl_setopt($ch, CURLOPT_REFERER, 'http://www.baidu.com');
    //模拟浏览器访问(用于解决'未将对象引用设置到对象的实例。')
    // curl_setopt($ch, CURLOPT_USERAGENT, $_SERVER['HTTP_USER_AGENT']);
    //执行会话
    $data = curl_exec($ch);
    //关闭cURL会话
    curl_close($ch);
    //返回数据
    return $data;
}