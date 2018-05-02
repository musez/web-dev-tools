# EVENT事件

## 阻止事件冒泡
```javascript
// 阻止事件冒泡
function stopEventBubble (event) {
    var e = event || window.event;
    
    if (e && e.stopPropagation) {
        e.stopPropagation();
    } else {
        e.cancelBubble = true;
    }
}
```

## js实现jquery ready方法
```javascript
// js实现jquery ready方法
function ready (fn) {
    if (document.addEventListener) { // 标准浏览器
        document.addEventListener('DOMContentLoaded', function () {
            // 注销时间，避免反复触发
            document.removeEventListener('DOMContentLoaded', arguments.callee, false);
            fn(); // 执行函数
        }, false);
    } else if (document.attachEvent) { // IE浏览器
        document.attachEvent('onreadystatechange', function () {
            if (document.readyState == 'complete') {
                document.detachEvent('onreadystatechange', arguments.callee);
                fn(); // 函数执行
            }
        });
    }
}
```

## jQuery – 鼠标经过(hover)事件的延时处理
```javascript
(function($){
    $.fn.hoverDelay = function(options){
        var defaults = {
            hoverDuring: 200,
            outDuring: 200,
            hoverEvent: function(){
                $.noop();
            },
            outEvent: function(){
                $.noop();    
            }
        };
        var sets = $.extend(defaults,options || {});
        var hoverTimer, outTimer, that = this;
        return $(this).each(function(){
            $(this).hover(function(){
                clearTimeout(outTimer);
                hoverTimer = setTimeout(function(){sets.hoverEvent.apply(that)}, sets.hoverDuring);
            },function(){
                clearTimeout(hoverTimer);
                outTimer = setTimeout(function(){sets.outEvent.apply(that)}, sets.outDuring);
            });    
        });
    }      
})(jQuery);
```

**参数说明：**
hoverDelay方法共四个参数，表示意思如下：

`hoverDuring`鼠标经过的延时时间

`outDuring`鼠标移出的延时时间

`hoverEvent`鼠标经过执行的方法

`outEvent`鼠标移出执行的方法