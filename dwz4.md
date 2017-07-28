注意表单
<form action="__URL__/<eq name='type' value='1'>back_recharge<else />back_withdrawal</eq>/navTabId/__MODULE__/asd/user_finance/?callbackType=closeCurrent" method="post" onsubmit="return validateCallback(this, dialogAjaxDone)">
...
</form>
跳转地址: 使用navTabId/asd两个参数指定, 通常会是就是当前页
回调类型: 指定为 closeCurrent , 关闭当前页面或弹窗
onsubmit : dialogAjaxDone

同时, 刷新当前页面, 注意翻页问题