# meta详解

meta标签可分为两大部分：http-equiv和name变量。

http-equiv

http-equiv相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助浏览器正确地显示网页内容。

|值|描述|例子|  
|-|-|-|  
|content-type|设定页面使用的字符集|`<meta http-equiv="content-Type" content="text/html; charset=utf-8">`<br>GB2312时，代表说明网站是采用的编码是简体中文；<br>ISO-8859-1时，代表说明网站是采用的编码是英文；<br>UTF-8时，代表世界通用的语言编码；<br>PS：html5页面的做法是直接使用<meta charset="utf-8"/>|  
|X-UA-Compatible|IE8的专用标记，用来指定IE8浏览器去模拟某个特定版本的IE浏览器的渲染方式，以此来解决部分兼容问题。|`<meta http-equiv="X-UA-Compatible" content="IE=7">`<br>以上代码告诉IE浏览器，无论是否用DTD声明文档标准，IE8/9都会以IE7引擎来渲染页面。<br>`<meta http-equiv="X-UA-Compatible" content="IE=8">`<br>以上代码告诉IE浏览器，IE8/9都会以IE8引擎来渲染页面。<br>`<meta http-equiv="X-UA-Compatible" content="IE=edge">`以上代码告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面。  
<br>`<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">`
<br>以上代码IE=edge告诉IE使用最新的引擎渲染网页，chrome=1则可以激活Chrome Frame.<br>PS：谷歌添加一个插件：Google Chrome Frame（谷歌内嵌浏览器框架GCF），这个插件可以让用户的IE浏览器外不变，但用户在浏览网页时，实际上使用的是Google Chrome浏览器内核，而且支持IE6、7、8等多个版本的IE浏览器。| 