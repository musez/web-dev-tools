# EVENT事件

1. 阻止事件冒泡
    ```js
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

2. js实现jquery ready方法
    ```js
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