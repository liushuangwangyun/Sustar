## 2017-7-12

### 制作提问页面

#### 页面要求：

* 可在input中填写问题标题
* 在div中选择问题所属标签
* 文本编辑器，可编辑文档或代码
* 页面整体结构：标题输入文本
              问题所属标签
              文本编辑器
              是否悬赏
              点击提交

#### 今日任务实现

* 熟悉git和github的使用
* 页面可填写提问的标题
* 点击div > input 出现隐藏的ul标签页可以点击选择问题所属的标签，
  选择的标签会自动添加到div > span 中最多选择五个标签，每个标签
  不可重复选择，也可以在后边的文本框中补充自己的标签内容
* 文本编辑器，可对文本或代码进行编辑，如：加粗、倾斜、下划线、添加
  图片等

#### 所遇到的问题

* 如何在隐藏的div中选择问题所属标签并自动添加到相应的位置并且限制个数
   
   ```
   
   $('.tag-a').one("click",function(){
				var a = $(this).text();
					console.log(a);
					$('.biaoqian').prepend("<span class='tag-a center'>" + a + "</span>");
					var b = $('.biaoqian span').length;
					if (b == 5){
						$('.tag-a').unbind("click");
					}
				})

				$('.biaoqian span').click(function(){
					$(this).fadeOut(400,function(){
						$(this).remove();
					})
				})
			 $(function () {
				$('#myTab li:eq(0) a').tab('show');

				$('#biaoqian-input').click(function(){
					$('.tag').slideToggle(400);
				})
        
    ```

## 2017-7-13

### 编写提问页面路由、完善提问页面细节内容

### 今日任务实现

* 问题所属标签点击input出现隐藏的div，鼠标不进入div范围一直悬停，鼠标进入再次移出时会自动消失隐藏
* 点击问题所属的小标签，大标签页会隐藏选中的标签，添加到问题标签所属的input中
* 点击标签后边的小叉会移除，input中的标签并且恢复到原本的大标签页中
* 完成了路由跳转，点击提交跳转到问题页

### 所遇到的问题

* 删除添加小标签的时候，原文的大标签页中的内容无法回复
  1. 删除原本的标签，直接添加，在input中点击移除（有bug，在input中删除的小标签在大标签页中无法再点击添加）
    ```
    $('.remove').find(i).click(function() {
						$(this).parent().remove();
					});

					$('.mb5').click(function(){
						var a = $(this).text();
						console.log(a);
						$('#tags').append("<span class='tag-span center'>" + a + "<i class='remove'> × </i></span>");
						$(this).remove();
					})

					var a = $('.biaoqian');
					var b = $('.tag-a');
					for (var i = 0; i < 5; i++){
						var c = $(this).text();
						b.eq(i).on("click", {value:i},function(event){
							a.appendTo("<span class='tag-span center'>" + a + "<i class='remove'> × </i></span>");
						})
					}
    ```
    
    2. 东朔帮忙，将小标签附有索引值，点击小标签时会隐藏所选内容并获得一个索引值，input点击删除时会根据索引值恢复
       
       bug:在同一页选中的内容删除后会恢复，切换到别的ul页中无法正常恢复
       
       ```
       $(document).on('click', '.remove', function() {
						b--;
						index = $(this).parent('.tag-span').data('value');
						$(this).parent('.tag-span').remove();
						console.log(index);
						$('.mb5').eq(index).fadeIn();
					});
       
     
       
       var b = 0;
					var index = 0;
					$('.tag-a').click(function(){
						if (b < 5) {
							b++;
						var a = $(this).text();
						console.log(a);
						index = $(this).parent('.mb5').index();
						$('#tags').append("<span class='tag-span center'>" + a + "<i class='remove'> × </i></span>");
						// 添加数据
						$('.tag-span').last().data('value', index);				
						$(this).parent('.mb5').fadeOut();				
					console.log('秒',$('.tag-span').last().data('value'));
					}
					});

       ```
### 明日计划内容

* 完成提问页数据库的编写
* 完成问题页面的大致框架
