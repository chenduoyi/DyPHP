## dwz图片上传, 分两种, 一种是表单提交的图片上传, 一种是富文本编辑器里的图片上传
富文本编辑器的图片上传, 简单, 只需要指定下上传时对应的接收方法和上传类型即可
<textarea name="content" class="editor" rows="28" cols="57" upImgUrl="__APP__/Common/uploadImg" upImgExt="jpg,jpeg,gif,png">{$vo.content}</textarea>
当然, 控制器里的图片接收方法需要有.

表单提交的图片上传, 相对麻烦一点. 因为需要在选择了图片之后, 就进行异步上传, 并且返回图片地址. 表单提交时将图片地址提交过来的处理方式.
```
<div class="unit">
    <label>文章配图：</label>
    <neq name="vo[cover_img]" value=""><img src="{$vo.cover_img}" alt="" ></neq>

    <!-- 图片上传按钮 -->
    <input id="fileupload" type="file" name="filedata" data-url="__APP__/Common/uploadImg" multiple customvalid=" customvalidImg(element)" >
    <input id="img" type="hidden" <neq name="vo[cover_img]" value="" > value="1" </neq>>
    <!-- 图片展示模块 -->
    <div class="files">
    </div>
    <div style="clear:both;"></div>
    <!-- 图片上传进度条模块 -->
    <div class="up_progress">
    <div class="progress-bar"></div>
    </div>
    <div style="clear:both;"></div>
    <br/>
    <label>&nbsp;&nbsp;</label>
    <button type="submit" style="display:none;">上传</button>
</div>
```
外加JS触发代码
```
<script src="__PUBLIC__/dwz/js/jquery.fileupload.js"></script>
<script type="text/javascript">
//图片上传
$("#fileupload").fileupload({
	dataType: 'json',
	add: function (e, data) {
		var numItems = $('.files .images_zone').length;
		if(numItems>=1){
			alert('提交照片不能超过1张');
			return false;
		}
		$('.up_progress .progress-bar').css('width','0px');
		$('.up_progress').show();
		$('.up_progress .progress-bar').html('Uploading...');
		data.submit();
	},
	done: function (e, data) {
		$('.up_progress').hide();
		$('.upl').remove();
		var d = data.result;
		if(d.status==0){
			alert("上传失败");
		}else{
			$("#img").val("1");
			var imgshow = '<div class="images_zone"><input type="hidden" name="cover_img" value="'+d.msg+'" /><span><img src="'+d.msg+'"  /></span><a href="javascript:;">删除</a></div>';
			jQuery('.files').append(imgshow);
		}
	},
	progressall: function (e, data) {
		var progress = parseInt(data.loaded / data.total * 100, 10);
		$('.up_progress .progress-bar').css('width',progress + '%');
	}
});

//图片删除
$('.files').on({
	mouseenter:function(){
		$(this).find('a').show();
	},
	mouseleave:function(){
		$(this).find('a').hide();
	},
},'.images_zone');

$('.files').on('click','.images_zone a',function(){
	$(this).parent().remove();
});

$("#del").live('click', function(event) {
	$("#selectShape").show();
	$("#organization").html('');
	$("input[name='organization']").val();
	$("#del").remove();
}); 

function customvalidImg(element){
	if(!$("#img").val()){
		if ($("input[name='cover_img']").val()=='' || $("input[name='cover_img']").length==0) {
			$(element).attr('title', '请上传图片');
			return false;
		}
	}
	return true;
}
</script>
```