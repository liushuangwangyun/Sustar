吴东朔总结:

day1:
  * 熟悉git, 进行协同开发
   * 首先`fork`下项目到自己的github
   * `git clone https://github.com/hsiaoshen/Sustar.git` 原项目地址到本地
   * 此时 `origin` 指向原项目地址
   * `git remote add branch https://github.com/gurenyigu/Sustar.git` 将自己`fork`的地址添加到项目中,名为`branch`
   * 创建分支并切换 `git checkout -b develop`
   * 查看两次hash值及所在分支 `git branch -av`
    * 这时我们对这个自己的新分支进行开发操作
   * 之后每次开发前执行 : `git checkout master`  `git pull origin` `git merge develop` 分支切换 更新 分支合并
    * `git commit -a -m '修改了....'` `git push branch develop`
    * 到github Pull requests
    
  * 项目主页面编写, 遇到问题, 注意以后要用 sass 来编写 css 样式
   * 替换别人框架的样式要使用自己的 类 , 使用 scss 取得高优先级
   * express 引用模板时, 相同的样式 和 其他库 只引用一次即可
   
  * 项目讨论, 小功能实现
  
  ```js
        // 代码中, 每个变迁在hover 时提供事件, 使用 ES6 新块级作用域的 let
          for (let i = 0, j = $('.tag').length; i < j; i++) {
            $('.tag').eq(i).hover(function() {
            // 使用 stop 在每次新事件触发时, 结束上次动画, 达到取消动画此起彼伏的晃眼
              $('.chuank').eq(i).stop().fadeIn(2000);
            }, function() {
            // 若离开, 立刻结束 2秒的 hover 动画
              $('.chuank').eq(i).stop().fadeOut(300);
            });
            
            // 在每次 hover 到标签时, 结束上次动画, 并添加显示
            $('.chuank').eq(i).hover(function() {
              $('.chuank').eq(i).stop().fadeIn();
            }, function() {
            // 离开同理
              $('.chuank').eq(i).stop().fadeOut();
            });
          }
  ```
   

day2:
 * 问题: jquery 添加的元素 无法获取, 实现的标签添加删除 行内携带 data 数据
   ```js
   // 定义两个变量, 一个控制次数, 另一个记录索引
              var b = 0;
              var index = 0;
              $('.tag-a').click(function() {
                  if (b < 5) {
                    b++;
                    var a = $(this).text();
                    // 索引值为选中元素父元素的索引, 索引范围为父元素内
                    index = $(this).parent('.mb5').index();
                    // 这里是添加到页面中的标签
                    $('#tags').append("<span class='tag-span center'>" + a + "<i class='remove'> × </i></span>");
                    // 将其父元素 类mb5 进行隐藏
                    $(this).parent('.mb5').fadeOut();
                    // 这里为最近一次 也就是最后一个标签添加数据 注意: 这里的数据在页面中不显示, 但是可以获取到
                    $('.tag-span').last().data('value', index);
                  });

                // 对添加的元素操作
                // 添加到页面的元素 使用 $(document).on(event, dom, function) 来添加事件
                $(document).on('click', '.remove', function() {
                  // 控制个数, 每次 减一
                  b--;
                  // 将上面保存到每次添加到页面的元素中 data 的索引值 取出来
                  index = $(this).parent('.tag-span').data('value');
                  // 对这个元素操作
                  $(this).parent('.tag-span').remove();
                  // 将取出来的那个索引位值元素显示
                  $('.mb5').eq(index).fadeIn();
                });

                // 问题: 在此项目中 index 并没有解决多栏中元素的索引...
   ```
