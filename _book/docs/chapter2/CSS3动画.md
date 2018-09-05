# CSS3 常用动画

``` html
    <script id="jsListTemplate" type="text/html">
        {{each list}}
        <li>
            {{$value.name}}
        </li>
        {{/each}}
    </script>
```

## CSS3 常用四个动画（旋转、放大、旋转放大、移动）
1. 效果一：360°旋转 修改rotate(旋转度数)
    ```css
    * {
        transition:All 0.4s ease-in-out;
        -webkit-transition:All 0.4s ease-in-out;
        -moz-transition:All 0.4s ease-in-out;
        -o-transition:All 0.4s ease-in-out;
    }
    *:hover {
        transform:rotate(360deg);
        -webkit-transform:rotate(360deg);
        -moz-transform:rotate(360deg);
        -o-transform:rotate(360deg);
        -ms-transform:rotate(360deg);
    }
    ```

2. 效果二：放大 修改scale(放大的值)
    ```css
    * {
        transition:All 0.4s ease-in-out;
        -webkit-transition:All 0.4s ease-in-out;
        -moz-transition:All 0.4s ease-in-out;
        -o-transition:All 0.4s ease-in-out;
    }
    *:hover {
        transform:scale(1.2);
        -webkit-transform:scale(1.2);
        -moz-transform:scale(1.2);
        -o-transform:scale(1.2);
        -ms-transform:scale(1.2);
    }
    ```

3. 效果三：旋转放大 修改rotate(旋转度数) scale(放大值)
    ```css
    * {
        transition:All 0.4s ease-in-out;
        -webkit-transition:All 0.4s ease-in-out;
        -moz-transition:All 0.4s ease-in-out;
        -o-transition:All 0.4s ease-in-out;
    }
    *:hover {
        transform:rotate(360deg) scale(1.2);
        -webkit-transform:rotate(360deg) scale(1.2);
        -moz-transform:rotate(360deg) scale(1.2);
        -o-transform:rotate(360deg) scale(1.2);
        -ms-transform:rotate(360deg) scale(1.2);
    }
    ```
    
4. 效果四：上下左右移动 修改translate(x轴,y轴)
    ```css
    * {
        transition:All 0.4s ease-in-out;
        -webkit-transition:All 0.4s ease-in-out;
        -moz-transition:All 0.4s ease-in-out;
        -o-transition:All 0.4s ease-in-out;
    }
    *:hover {
        transform:translate(0,-10px);
        -webkit-transform:translate(0,-10px);
        -moz-transform:translate(0,-10px);
        -o-transform:translate(0,-10px);
        -ms-transform:translate(0,-10px);
    }
    ```
    
    **SCSS改造**
    
    ```scss
    // 执行动画以及执行时间设定
    @mixin dz($time:0.25s){
        -webkit-transition: all $time ease-in-out;
        -moz-transition: all $time ease-in-out;
        -o-transition: all $time ease-in-out;
        -ms-transition: all $time ease-in-out;
        transition: all $time ease-in-out;
    }
 
    // 宣传动画调用
    @mixin xz($deg:360){
        transform:rotate($deg+deg);
        -webkit-transform:rotate($deg+deg);
        -moz-transform:rotate($deg+deg);
        -o-transform:rotate($deg+deg);
        -ms-transform:rotate($deg+deg);
    }
 
    // 放大动画
    @minxin fd($s1:1.2){
        transform:scale($s1);
        -webkit-transform:scale($s1);
        -moz-transform:scale($s1);
        -o-transform:scale($s1);
        -ms-transform:scale($s1);
    }
 
    // 旋转放大动画
    @mixin xzfd($deg:360,$s1:1.2){
        transform:rotate($deg+deg) scale($s1);
        -webkit-transform:rotate($deg+deg) scale($s1);
        -moz-transform:rotate($deg+deg) scale($s1);
        -o-transform:rotate($deg+deg) scale($s1);
        -ms-transform:rotate($deg+deg) scale($s1);
    }
 
    // 移动动画
    @mixin yd($s1:0,$s2:0){
        transform:translate($s1,$s2);
        -webkit-transform:translate($s1,$s2);
        -moz-transform:translate($s1,$s2);
        -o-transform:translate($s1,$s2);
        -ms-transform:translate($s1,$s2);
    } 
    ```
    
    **使用方法**
    ```scss
    #somebox{
        @include dz();
        &:hover {
            @include yd(-10px,-10px);
        }
    }
    ```
    
