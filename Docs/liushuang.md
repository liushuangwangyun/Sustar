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
