//不直接通过http请求, 上传的图片信息没有传过去
//$res = get_interface('User/getShopAuthentic', $data);

//将接收到的图片信息, 压入data数组内, 此数组已包含图片信息
$data['door_pic'] = '@'.realpath($_FILES['door_pic']['tmp_name']).";type=".$_FILES['door_pic']['type'].";filename=".$_FILES['door_pic']['name'];
$data['business_pic'] = '@'.realpath($_FILES['business_pic']['tmp_name']).";type=".$_FILES['business_pic']['type'].";filename=".$_FILES['business_pic']['name'];

//将具备图片信息的data数组, 通过get_interface请求过去, 仍后台接口仍然接收不到图片
//$res = get_interface('User/getShopAuthentic', $data);

//使用curl请求接口
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://'.$http_host. '/api/v1/User/getShopAuthentic');
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_SAFE_UPLOAD, false);
curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
curl_exec($ch);
curl_close($ch);

echo $res;
exit;