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
    ```
    
    **注意事项：**如果实现单行文本的溢出显示省略号同学们应该都知道用text-overflow:ellipsis属性来，当然还需要加宽度width属来兼容部分浏览。

2. 多行文本

    **第1种情况**
    
    **适用范围：**因使用了WebKit的CSS扩展属性，该方法适用于WebKit浏览器及移动端；
    ```css
    p {
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 3;
        overflow: hidden;
    }
    ```
    ** 注意事项：**
        1. -webkit-line-clamp用来限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他的WebKit属性。常见结合属性：
        2. display: -webkit-box; 必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。
        3. -webkit-box-orient 必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。

    **第2种情况**
    
    **适用范围：**该方法适用范围广，但文字未超出行的情况下也会出现省略号,可结合js优化该方法。

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
    **注意事项：**
        1. 将height设置为line-height的整数倍，防止超出的文字露出。
        2. 给p::after添加渐变背景可避免文字只显示一半。
        3. 由于ie6-7不显示content内容，所以要添加标签兼容ie6-7（如：<span>…<span/>）；兼容ie8需要将::after替换成:after。

## 兼容性
1. ie8兼容rgba(RR,GG,BB,AA)

    ie8以上：rgba(RR,GG,BB,AA);
    
    ie8：filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#AARRGGBB,endColorstr=#AARRGGBB);
    
    “#AARRGGBB”是颜色的意思，是由两部分组成的。
    第一部是透明度值：#AA 。是rgba透明度0.1的IEfilter值。从0.1到0.9每个数字对应一个IEfilter值。对应关系如下：
  
    |rgba透明值| IEfilter值|
    |-|-|
    |0.1|19|
    |0.2|33|
    |0.3|4c|
    |0.4|66|
    |0.5|7f|
    |0.6|99|
    |0.7|b2|
    |0.8|c8|
    |0.9|e5|

## vue
1. 隐藏显示的\{\{\}\}
    ```css
    /*vue*/
    [v-cloak] {
        display: none !important;
    }
    ```
    
## 时间轴
1. 时间轴

**演示地址**：[https://musez.github.io/web-dev-tools/pages/timeline.htm](https://musez.github.io/web-dev-tools/pages/timeline.html)

html
 ```html
<ul class="timeline">
    <li class="timeline_cell active">
        <b></b>
        <p class="timeline_cell-time">2018-01-01 00:00:00</p>
        <p class="timeline_cell-desc"><a href="javascript:;">武汉佳软信息技术有限公司（以下简称”佳软信息”）</a>成立于2007年，是一家电子政务整体解决方案提供商，位于武汉东湖新技术开发区——“中国光谷”中心的光谷软件园。经过多年的发展，公司的业务范围扩展至政府门户网站建设、行政审批信息化、政府信息资源整合、政府行业管理系统的研发服务，涉及统一门户、统一用户、网站内容管理平台、全文检索、信息资源库、信息资源目录及信息交流平台等，不断为政务服务和民生服务提供优质产品。目前拥有湖北省交通运输厅、省财政厅、省国土资源厅、省公安厅、省质监局、省监察厅等40余家省直部门用户。</p>
    </li>
    <li class="timeline_cell">
        <b></b>
        <p class="timeline_cell-time">2018-01-01 00:00:00</p>
        <p class="timeline_cell-desc">武汉佳软信息技术有限公司（以下简称”佳软信息”）</p>
    </li>
    <li class="timeline_cell">
        <b></b>
        <p class="timeline_cell-time">2018-01-01 00:00:00</p>
        <p class="timeline_cell-desc">武汉佳软信息技术有限公司（以下简称”佳软信息”）</p>
    </li>
</ul>
```
scss
```scss
.timeline {
  list-style-type: none;
  padding: 0px;
  border-left: 2px solid #ccc;
  margin: 10px 10px 10px 20px;

  @at-root .timeline_cell {
    position: relative;
    margin-top: 15px;
    padding-left: 20px;

    b:before {
      content: '';
      position: absolute;
      left: -10px;
      width: 18px;
      height: 18px;
      border-radius: 9px;
      background: #ccc;
    }

    &.active b:before {
      background: #359;
    }

    .timeline_cell-time,
    .timeline_cell-desc {
      display: block;
      color: #000;

      a {
        color: #359;
        text-decoration: none;
      }
    }

    &.active .timeline_cell-time {
      color: #359;
      font-weight: bolder;
    }
  }
}
```
css
```css
.timeline {
    list-style-type: none;
    padding: 0px;
    border-left: 2px solid #ccc;
    margin: 10px 10px 10px 20px;
}

.timeline_cell {
    position: relative;
    margin-top: 15px;
    padding-left: 20px;
}

.timeline_cell b:before {
    content: '';
    position: absolute;
    left: -10px;
    width: 18px;
    height: 18px;
    border-radius: 9px;
    background: #ccc;
}

.timeline_cell.active b:before {
    background: #359;
}

.timeline_cell .timeline_cell-time,
.timeline_cell .timeline_cell-desc {
    display: block;
    color: #000;
}

.timeline_cell .timeline_cell-time a,
.timeline_cell .timeline_cell-desc a {
    color: #359;
    text-decoration: none;
}

.timeline_cell.active .timeline_cell-time {
    color: #359;
    font-weight: bolder;
}
```
