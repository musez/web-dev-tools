# css封装

## 表单
1. input placeholder
    ```css
    ::-webkit-input-placeholder { /* WebKit browsers */
        color: #999;
    }
    :-moz-placeholder { /* Mozilla Firefox 4 to 18 */
        color: #999;
    }
    ::-moz-placeholder { /* Mozilla Firefox 19+ */
        color: #999;
    }
    :-ms-input-placeholder { /* Internet Explorer 10+ */
        color: #999;
    }
    ```

## 文本溢出显示省略号
1. 单行文本
    ```css
    p {
        overflow: hidden;
        text-overflow:ellipsis;
        white-space: nowrap;
    }
    
    /*注意事项：如果实现单行文本的溢出显示省略号同学们应该都知道用text-overflow:ellipsis属性来，当然还需要加宽度width属来兼容部分浏览。*/
    ```

2. 多行文本

    **第1种情况**
    
    适用范围：因使用了WebKit的CSS扩展属性，该方法适用于WebKit浏览器及移动端；
    ```css
    p {
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 3;
        overflow: hidden;
    }
    ```
     注意事项：
     
        1. -webkit-line-clamp用来限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他的WebKit属性。常见结合属性：
        2. display: -webkit-box; 必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。
        3. -webkit-box-orient 必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。

    **第2种情况**
    
    适用范围：该方法适用范围广，但文字未超出行的情况下也会出现省略号,可结合js优化该方法。

    ```css
    p {
        position: relative;
        line-height: 20px;
        max-height: 40px;
        overflow: hidden;
    }
    
    p::after {
        content: "...";
        position: absolute;
        bottom: 0; 
        right: 0;
        padding-left: 40px;
        background: -webkit-linear-gradient(left, transparent, #fff 55%);
        background: -o-linear-gradient(right, transparent, #fff 55%);
        background: -moz-linear-gradient(right, transparent, #fff 55%);
        background: linear-gradient(to right, transparent, #fff 55%);
    }
    ```
    注意事项：
    
        1. 将height设置为line-height的整数倍，防止超出的文字露出。
        2. 给p::after添加渐变背景可避免文字只显示一半。
        3. 由于ie6-7不显示content内容，所以要添加标签兼容ie6-7（如：<span>…<span/>）；兼容ie8需要将::after替换成:after。

## 兼容性
1. ie8兼容rgba(RR,GG,BB,AA)

    ie8以上：rgba(RR,GG,BB,AA);
    
    ie8：filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#AARRGGBB,endColorstr=#AARRGGBB);

## vue
1. 隐藏显示的\{\{\}\}
    ```css
    /*vue*/
    [v-cloak] {
        display: none !important;
    }
    ```