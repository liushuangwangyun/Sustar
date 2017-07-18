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

## 2017-7-14

### 编写提问页面的数据库, 编写回复前台页面

### 今日任务实现

* 基本完成数据库的设计大致内容如下

**问题**

中文名字 | 英文名字 | type | 是否必填 | defaults | 备注
-------|------ |----|-------|--------|---
id　　　| id | object | 是 |        |
问题的标题| title | String | 是 |  |
问题的内容|questioncontent|String| 是　|   |   
提问者的id|personid| String| 是　|    | 
关注该问题的人数与id|focusperson|Array| 　| [ ]  |讲提问者与回答者与评论者加入其中,人数通过长度获取
每个回答的id|answerid|Array|  | [ ]|
问题的状态（暂无回答、有回答但未解决、问题已解决）|state|String| 是　|noanswer| 用三个字符串表示，noanswer,answerforming，resolved
问题所属的标签|tag|Array|   | [] | 存放标签的id
问题的浏览次数|questionview|Number|    | 0 | 
提问的时间|questiondate|Date|   |      |提交问题时获取
问题获得的赞数|praise|Number|   |  0  |
问题的代码|code|--------------------------
最后更新时间|lastdate|Date|    |     |有人回答或者评论时获取覆盖

* 编写回复页面,页面显示:提问的标题,提问的内容,提问内容的所属标签,提问者的用户名和用户头像
* 点击按钮收藏,点赞
* div插入文本编辑器可对输入内容进行简单编辑

### 所遇到的问题

1. 在页面上显示提出问题的当时时间
2. 在页面上显示保存用户浏览量

   注:问题还没有解决明天继续
   
 ### 明日计划内容
 
 * 完成回复页面的编写
 * 完成问题解决
 * 完成数据库的读取

## 2017-7-15

### 编写回复页面,404页面,我的资产页面

### 今日任务实现

* 回复页面:从数据库中读取问题标题 "h2",问题内容"p",问题所属标签"span",提问者的用户名和头像"span""img"
         
	 回复区域用的是插件文本编辑器,自动添加到div中,回复者的用户名和头像
* 404:插如404响应式图片
* 我的资产页面:有我的收入,支出,体现,可用余额,最小体现金额不小于十.用table表格记录资产

### 所遇到的问题

* 点击索引标签根据标签内容不跳转页面刷新内容

```
<ul class="nav nav-tabs">
              <li role="presentation" class="active"><a href="#money-a1" aria-controls="settings" role="tab" data-     toggle="tab">收入</a></li>
  	      <li role="presentation"><a href="#money-a2" aria-controls="settings" role="tab" data-toggle="tab" >支出</a></li>
  	      <li role="presentation"><a href="#money-a3" aria-controls="settings" role="tab" data-toggle="tab">体现</a></li>
            </ul>
	    
	    
<div role="tabpanel" class="tab-pane fade active in" id="money-a1">
<div role="tabpanel" class="tab-pane fade" id="money-a2">
<div role="tabpanel" class="tab-pane fade" id="money-a3">

```

### 明日计划内容

* 哪缺写哪

## 2017-7-17

### 测试有问题的地方进行修改

### 今日任务完成

1. 对回复页进行修改.
   1. 修改之前:无论点击哪里都是跳转的同一个页面
   2. 修改之后:可以根据标题的内容跳转到相应的页面,呈现不同的效果
2. 修改了部分页面的css样式

### 所遇到的问题

回复页面回复时的内容模块出现问题,人物头像无法获取

```
router.get('/', function(req, res) {
  console.log(req.query);
  var state;
  if (req.session.uid != undefined) {
      state = true;
  } else {
      state = false;
  };
  qdb.qdb.find({"title": req.query.title}, function(err, data){
    console.log(data);
    res.render('answer', {state: state, data: data[0]});
  })
});

```

