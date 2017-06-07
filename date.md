# 根据日期, 获取本周,本月,本季,本年的起止日期
```
function get_settlement_cycle($type,$date) {
    if ($type == 1) {
        //周结
        $week = date('w',strtotime($date));  //获取当前周的第几天 周日是 0 周一到周六是 1 - 6 
        $now_start = date('Y-m-d',strtotime("$date - ".($week ? $week - 1 : 6).' days')); //获取本周开始日期，如果$w是0，则表示周日，减去 6 天
        $now_end = date('Y-m-d',strtotime("$now_start +6 days"));  //本周结束日期
    } elseif ($type == 2) {
        //月结
        $now_start = date('Y-m-01',strtotime($date));
        $now_end = date('Y-m-d',strtotime("$now_start +1 month -1 day"));
    } elseif ($type == 3) {
        //季节
        $season = ceil((date('n',strtotime($date)))/3);//当月是第几季度
        $start_month = ($season - 1) * 3 + 1; //季度起始月份
        $start_month = $start_month < 10 ? '0' . $start_month : $start_month;
        $now_start = date('Y-' . $start_month . '-01',strtotime($date));
        $now_end = date('Y-m-d',strtotime("$now_start +3 months -1 day"));
    } elseif ($type == 4) {
        //年结
        $now_start = date('Y-01-01',strtotime($date));
        $now_end = date('Y-m-d',strtotime("$now_start +1 year -1 day"));
    }

    return array($now_start,$now_end);
}
```