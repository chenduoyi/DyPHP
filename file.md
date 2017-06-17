<?php
namespace Home\Controller;
use Think\Controller;
// use Think\Cache\Driver\Redis;
class IndexController extends Controller {
    public function index() {
        $handle=opendir('./kline');
        //定义用于存储文件名的数组
        $array_file = array();
        $kline_modle = M('trading_data_kline');
        while (false !== ($file = readdir($handle))) {
            if ($file != "." && $file != "..") {
                $file_data = file_get_contents('./kline/' . $file);
                $data = explode("\n",trim($file_data));
                foreach ($data as $k=>$v) {
                    $k_arr = explode(',',$v);
                    $k_data['product_code'] = $k_arr[0];
                    $k_data['date'] = $k_arr[2];
                    $k_data['open'] = $k_arr[3];
                    $k_data['high'] = $k_arr[5];
                    $k_data['low'] = $k_arr[4];
                    $k_data['close'] = $k_arr[6];
                    $k_data['volume'] = $k_arr[7];
                    $k_data['create_time'] = time();
                    $is_exist = $kline_modle->where(array('product_code'=>$k_arr[0],'date'=>$k_arr[2]))->count();
                    if (!$is_exist) {
                        $kline_modle->add($k_data);
                    }
                }
            }
        }
    }
}