## 					lazyload使用
一、lazyload.js用于长页面图片的延迟加载，视口外的图片会在窗口滚动到它的位置时再进行加载，这是与预加载相反的。
优点：
​       1、它可以提高页面记载速度;
​       2、在某些情况下可以帮助减少服务器负载。
二、lazyload依赖于jquery，所以先引入jquery和lazyload

    <script src="jquery.js"><script>
    <script src="jquery.lazyload.js"><script>
1、将图片路径写入data-original属性
2、给lazyload的图片增加一个名为lazy的class
3、选择所有要lazyload的图片(img.lazy),执行lazyload();
    <img class="lazy" data-original="img/example.jpg" style="margin-top:1000px" height="200">
    <script>
        $(function(){
            $("img.lazy").lazyload();
        })
    </script>
    注意：必须设置图片的高度或宽度，否则插件可能无法正常工作
三、提前加载 ——Threshold
 lazyload默认是当滚动该图片位置时,加载该图片。但是可以通过设置Threshold参数来实现滚到距离其指定距离时，就加载。
    $(function(){
      $("img.lazy").lazyload({
        threshold:20
      });
    })
    这个例子是设置了滚动距离图片20px时，图片就开始加载
四、事件触发(可以是jquery事件，也可以是自定义事件)——event
   当触发定义时，图片才开始加载
     $(function(){
       $("img.lazy").lazyload({
         event:"click"
       });
     })
     这个例子是当图片点击后，才开始加载
  可以通过这个来实现图片的延迟加载
   $(function() {
    $("img.lazy").lazyload({
        event : "sporty"
    });
});

$(window).bind("load", function() {
    var timeout = setTimeout(function() {
        $("img.lazy").trigger("sporty")
      }, 5000);
    });
    这个例子在代码加载完毕后五秒开始加载图片
五、插件默认的是show(),也可以自定义
    $("img.lazy").lazyload({
        effect : "fadeIn"
    });
六、滚动容器内的图片——container
插件也可以使用在滚动容器内的图片上。下面的div拥有scrollerbar，当内容进行滚动，滚动到图片位置时，图片开始加载
    <div style="height:600px;overflow:scroll" id="container">
      <img class="lazy" data-original="img/example.jpg" alt="" style="margin-top:1000px" height="200">
    </div>
    <script>
      $(function(){
         $("img.lazy").lazyload({
            container: $("#container")
         });
      })
    </script>

七、不按顺序排列的图片
​    插件会执行一个寻找未加载的循环，该循环会检查图片是否可见，默认情况下，当第一个视图外的图片被找到，循环就会停止。
   但是存在一种情况：页面布局图片的顺序和html图片代码顺序不一致；它会导致本该加载的没有加载。这种情况下可以将failure设为10，它使插件找到10个视图外的图片才停止搜索；当然也可以把这个参数设高一点。
     $("img.lazy").lazyload({
      failure_limit : 10
     });

八、处理隐藏图片——skip_invisible
  为了提升性能，插件默认忽略隐藏的图片;如果想要加载隐藏图片，设置skip_invisible为false
     $("img.lazy").lazyload({
        skip_invisible : true
     });
     注意：webkit浏览器将自动把没有宽度和高度的图像视为不见