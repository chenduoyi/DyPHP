列表页
```
<div class="panelBar">
		<ul class="toolBar">
			<li><a class="add" href="__URL__/add_category" target="dialog" mask="true" width="600" height="500"><span>新增</span></a></li>
			<li><a class="delete" href="__URL__/del_category/id/{sid_user}/navTabId/Product/asd/cat_list"  title="你确定要删除吗？" target="ajaxTodo" warn="请选择编号"><span>删除</span></a></li>
			<li><a class="edit" href="__URL__/add_category/id/{sid_user}" target="dialog" mask="true" warn="请选择编号" width="600" height="500"><span>编辑</span></a></li>
		</ul>
	</div>
```
弹窗页
<form method="post" action="__URL__/add_category/navTabId/Product/asd/cat_list?callbackType=closeCurrent" class="pageForm required-validate" onsubmit="return validateCallback(this, dialogAjaxDone)">

原参考例子
	<!-- <form method="post" action="__URL__/<neq name='vo.id' value=''>update<else />insert</neq>/navTabId/__MODULE__?callbackType=closeCurrent" class="pageForm required-validate" onsubmit="return validateCallback(this, dialogAjaxDone)"> -->

之前认为需要在列表页的新增编辑里, 带上, navTabId, asd参数, 对于ajax请求方式的, 如本例中的删除, 是需要带, 
但是, 对于弹窗页面的新增和编辑来说, 列表里完全可以不写, 写了也没有人管它. 真正起作用的是, 弹窗页里的表单提交, action=xxxx这里, 需要在这里注明, navTabId 及 asd
那什么别人的例子里, 没有写asd, 只写了navTabId呢, 
没有asd, 也就没有了action, 在没有指定action的情况下, 默认访问 index , 而实际运用中, action 不一定是index, 所以必须指定!!