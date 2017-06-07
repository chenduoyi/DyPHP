# dwz 弹窗搜索,翻页及刷新
## 翻页头部
```
<!-- <include file="Public:pagerForm" /> -->
<form id="pagerForm" action="{:U('Member_management/transfer_manage',array('id'=>$_GET['id']))}" method="post">
	<input type="hidden" name="pageNum" value="1"/>
	<input type="hidden" name="_order" value="{$_REQUEST._order}"/>
	<input type="hidden" name="_sort" value="{$_REQUEST._sort}"/>
</form>
```
## 搜索表单
```
<form rel="pagerForm" onsubmit="return dwzSearch(this, 'dialog');" action="{:U('Member_management/transfer_manage',array('id'=>$_GET['id']))}" method="post">
```
## 展示表单
```
<table class="table" width="100%" layoutH="208" targetType="dialog">
页码
<div class="panelBar">
	<div class="pages">
		<span>共{$totalCount}条</span>
	</div>
	<div class="pagination" targetType="dialog" totalCount="{$totalCount}" numPerPage="{$numPerPage}" pageNumShown="10" currentPage="{$currentPage}"></div>
</div>
```
## 注意点:
- 翻页方法, 获取不到方法, 需在页面里直接写上
- targetType="dialog"
- onsubmit="return dwzSerach(this,'lailog');"
## 页面刷新 
```
<script type="text/javascript">
    $("#bt_refresh").click(function(){
        var dialog = $.pdialog.getCurrent();
        $.pdialog.reload(dialog.data("url"));
    });
</script>
```