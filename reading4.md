#自适应网页设计（Responsive Web Design）

###一、允许网页宽度自动调整

首先，通过在在网页代码的头部&lt;head&gt; 标签里添加，加入一行viewport元标签。

    <meta name="viewport" content="width=device-width, initial-scale=1" />

(这段代码支持Chrome、Firefox、IE9以上的浏览器，但不支持IE8以及低于IE8的浏览器。)

viewport是网页默认的宽度和高度，上面这行代码的意思是，网页宽度默认等于屏幕宽度（width=device-width），原始缩放比例（initial-scale=1）为1.0，即网页初始大小占屏幕面积的100%。

所有主流浏览器都支持这个设置，包括IE9。对于那些老式浏览器（主要是IE6、7、8），需要使用css3-mediaqueries.js。
  
    <!--[if lt IE 9]>       
      <script src="http://css3-mediaqueries-js.googlecode.com/svn/trunk/css3-mediaqueries.js"></script>
    <![endif]-->

###二、不使用绝对宽度

由于网页会根据屏幕宽度调整布局，所以不能使用绝对宽度的布局，也不能使用具有绝对宽度的元素。这一条非常重要。

具体说，CSS代码不能指定像素宽度：

    width:xxx px;

只能指定百分比宽度：

    width: xx%;

或者

    width:auto;

(网页总体框架可以使用绝对宽度，但往下的内容框架、侧栏等最好使用相对宽度，这样针对不同分辨率进行修改就方便。当然也可以不用相对宽度，那就需要在 @media screen and (max-device-width: 480px) 里面增加各个div的针对小屏幕的宽度，实际上更麻烦。)

###三、相对大小的字体

字体也不能使用绝对大小（px），而只能使用相对大小（em）。

    body {
        font: normal 100% Helvetica, Arial, sans-serif;
    }

上面的代码指定，字体大小是页面默认大小的100%，即16像素。

    h1 {
       font-size: 1.5em; 
    }

然后，h1的大小是默认大小的1.5倍，即24像素（24/16=1.5）。

    small {
        font-size: 0.875em;
    }

small元素的大小是默认大小的0.875倍，即14像素（14/16=0.875）。

###四、流动布局（fluid grid）

"流动布局"的含义是，各个区块的位置都是浮动的，不是固定不变的。

    .main {
       float: right;
       width: 70%; 
    }

    .leftBar {
       float: left;
       width: 25%;
     }

float的好处是，如果宽度太小，放不下两个元素，后面的元素会自动滚动到前面元素的下方，不会在水平方向overflow（溢出），避免了水平滚动条的出现。

另外，绝对定位（position: absolute）的使用，也要非常小心。

###五、选择加载CSS

"自适应网页设计"的核心，就是CSS3引入的Media Query模块。

它的意思就是，自动探测屏幕宽度，然后加载相应的CSS文件。

    <link rel="stylesheet" type="text/css"
       media="screen and (max-device-width: 400px)"
       href="tinyScreen.css" />

上面的代码意思是，如果屏幕宽度小于400像素（max-device-width: 400px），就加载tinyScreen.css文件。

    <link rel="stylesheet" type="text/css"
       media="screen and (min-width: 400px) and (max-device-width: 600px)"
       href="smallScreen.css" />

如果屏幕宽度在400像素到600像素之间，则加载smallScreen.css文件。

除了用html标签加载CSS文件，还可以在现有CSS文件中加载。

    @import url("tinyScreen.css") screen and (max-device-width: 400px);

###六、CSS的@media规则

同一个CSS文件中，也可以根据不同的屏幕分辨率，选择应用不同的CSS规则。

    @media screen and (max-device-width: 400px) {

       .column {
          float: none;
          width:auto;
       }

       #sidebar {
          display:none;
       }
    
    }

上面的代码意思是，如果屏幕宽度小于400像素，则column块取消浮动（float:none）、宽度自动调节（width:auto），sidebar块不显示（display:none）。

###七、图片的自适应（fluid image）

除了布局和文本，"自适应网页设计"还必须实现图片的自动缩放。

这只要一行CSS代码：

    img { max-width: 100%;}

这行代码对于大多数嵌入网页的视频也有效，所以可以写成：

    img, object { max-width: 100%;}

老版本的IE不支持max-width，所以只好写成：

    img { width: 100%; }

此外，windows平台缩放图片时，可能出现图像失真现象。这时，可以尝试使用IE的专有命令：

    img { -ms-interpolation-mode: bicubic; }

或者，Ethan Marcotte的imgSizer.js。

    addLoadEvent(function() {

        var imgs = document.getElementById("content").getElementsByTagName("img");

        imgSizer.collate(imgs);

    });

css加载的background-image自适应大小，CSS3中是可以实现的，添加如下语句：background-size:100% 100%;

注：如有条件的话，最好还是根据不同大小的屏幕，加载不同分辨率的图片

<br/><br/><br/>

**尺寸相关**

--------------------------------------------------------------------------------

- 百分比，百分比是相对父对象的，这里特性非常好用，很多时候会用在自适应布局上面。浏览器尺寸的改变，就是根节点html的长宽改变，可以用%来将浏览器尺寸和元素尺寸联系起来，做到自适应。

- auto，auto是很多尺寸值的默认值，也就是由浏览器自动计算。首先是块级元素水平方向的auto，块级元素的margin、border、padding以及content宽度之和等于父元素width。使用auto属性在父元素宽度变化的时候，该元素的宽度也会随之变化。 但是当该元素被设为浮动时，该元素的width就变成了内容的宽度了，由内容撑开，也就是所谓的有了包裹性。overflow | position:absolute | float:left/right都可以产生包裹性，替换元素也同样具有包裹性。在具有包裹性的元素上想利用width : auto；来让元素宽度自适应浏览器宽是不行的。

- 包裹性  高度方向：外边距重叠，外边距auto为0。

- margin：auto对不能计算垂直方向的值:  垂直方向是被设计成可以无限扩展的，内容越多浏览器便产生滚动条来扩展，所以垂直方向都找不到一个计算基准，以此返回一个false，便成了0。

用处：通过width、height控制大小，各个方向的margin值控制与边界或者其他元素的距离来定位。

**浮动**

--------------------------------------------------------------------------------

浮动布局的核心就是让元素脱离普通流，然后使用width/height，margin/padding将元素定位。高度不同所以可以叠在其他元素上面产生重叠或者使用负边距跑到父元素外。

下面用个圣杯布局的例子说明一下，理解了这个之后其他布局更加简单：

<html>
    <head>
        <meta charset="utf-8" />
        <title>宽度自适应布局</title>
        <style>
            .wrap {
                background-color: #D66464;
            }
            .clearfix:after {
                content: "";
                clear: both;
                display: block;
            }
            .left {
                float: left;
                width: 100px;
                background: #00f;
                height: 180px;
            }
            .right {
                float: right;
                width: 150px;
                background: #0f0;
                height: 200px;
            }
            .center {
                background: #FFFFFF;
                margin-left: 110px;
                margin-right: 160px;
                height: 150px;
            }
        </style>
    </head>
    <body>
        <div class="wrap clearfix">
            <div class="left">left，宽度固定，高度可固定也可以由内容撑开。</div>
            <div class="right">right，宽度固定，高度可固定也可以由内容撑开。</div>
            <div class="center">center，可以自适应浏览器宽度，高度可固定也可以由内容撑开。</div>
        </div>
    </body>
</html>   
     
<br/><br/>

    <head>
        <meta charset="utf-8" />
        <title>宽度自适应布局</title>
        <style>
            .wrap {
                background-color: #D66464;
            }
            .clearfix:after {
                content: "";
                clear: both;
                display: block;
            }
            .left {
                float: left;
                width: 100px;
                background: #00f;
                height: 180px;
            }
            .right {
                float: right;
                width: 150px;
                background: #0f0;
                height: 200px;
            }
            .center {
                background: #FFFFFF;
                margin-left: 110px;
                margin-right: 160px;
                height: 150px;
            }
        </style>
    </head>
    <body>
        <div class="wrap clearfix">
            <div class="left">left，宽度固定，高度可固定也可以由内容撑开。</div>
            <div class="right">right，宽度固定，高度可固定也可以由内容撑开。</div>
            <div class="center">center，可以自适应浏览器宽度，高度可固定也可以由内容撑开。</div>
        </div>
    </body>
 

原理：左右侧边栏定宽并浮动，中部内容区放最后不浮动、默认width：auto并设置相应外边距，让左右侧边栏浮动到上面。注意：子元素设置为浮动之后，父对象的高度就坍塌了，需要设置父对象后的元素清除浮动，这样父对象的高度才能被浮动子元素撑起来了。


总结：使用浮动来进行布局，一个比较大的问题是清除浮动。这个可以使用一个after伪类来清除。更大的问题是浮动性像水一样向上流动，难以把握。在元素较多而且元素高度尺寸不一的情况下，单纯使用浮动只能实现上端对齐，这对于适应多种设备的布局就显得力不从心了。目前的做法是牺牲一部分内容，将元素做成等高排列，从美观上看也当然也是极好的，比参差不齐的排列要美观。


**普通流布局**

--------------------------------------------------------------------------------

普通流布局：display : inline-block

使用inline-block元素会有4px左右的空隙，这个是因为我们写代码时候的换行符所致。

解决办法：在inline-block的父元素中设置样式font-size：0；letter-spacing: -4px; 然后设置inline-block的所有兄弟元素 font-size：值；letter-spacing: 值px;  恢复正常的显示。

另外还有一点需要注意的是inline-block默认是基线对齐的，而inline-block的基线又跟文本基线一致，所以在内容不同的时候并不能水平对齐。只需要用vertical-align显式声明一下top/bottom/middle对齐即可。

- 基线的内容分有文字和无文字两种情况：

1）无文字：容器的margin-bottom下边缘。与容器内部的元素没有关系。

2）有文字：最后一行文字的下边缘，跟文字块（p,h等）的margin、padding没关系！注意是最后一行，无论文字在什么子对象容器内在什么位置都没关系，浏览器会找到最后一行文字对齐底部。

总结：相比浮动inline-block更加容易理解，也更符合我们的认知，结合盒子模型的几个控制属性就可以进行布局了。对于元素高度不同的情况，目前浮动布局的做法都是将元素做成等高元素进行展现，这从美学上看也符合整齐的要求，不过牺牲了一部分内容。但inline-block有vertical-align属性，可以很好地解决元素高度不同而带来的布局问题。

**绝对定位**

--------------------------------------------------------------------------------

absolute定位的基准是最近的非static定位父对象，而fixed是相对html根节点的定位。两种定位都会脱离普通流，跟之前说的浮动一样。

使用绝对定位（特指absolute）做自适应布局跟前面两种方式没太大差别，宽度自适应还是在auto和100%上做文章，而位置则由top/bottom/left/right等控制。还是以圣杯布局来举例：


    <head>
        <meta charset="utf-8" />
        <title>宽度自适应布局</title>
        <style>
            .wrap {
                position: relative;
                background-color: #FBD570;
                margin-left: 100px;
                margin-right: 150px;
                height: 250px;
            }
            .left {
                position: absolute;
                top: 0;
                left: -100px;
                width: 100px;
                background: #00f;
                height: 180px;
            }
            .right {
                position: absolute;
                top: 0;
                right: 0;
                   width: 150px;
                background: #0f0;
                height: 200px;
                margin-right: -150px;
            }
            .center {
                position: absolute;
                top: 0;
                left: 0;
                background: #B373DA;
                height: 150px;
                min-width: 150px;
                width: 100%;
            }
        </style>
    </head>
    <body>
        <div class="wrap">
            <div class="center">
                center，可以自适应浏览器宽度，高度固定。
            </div>
            <div class="left">left，宽度高度固定</div>
            <div class="right">right，宽度高度固定</div>
        </div>
    </body>

 
父元素为relative，子元素为absolute，这样的话，又会出现跟浮动一样的问题：父对象高度坍塌，子元素不能撑起父对象。原因也跟浮动一样，解决办法可以给父对象指定一个确定height值

总结：单纯使用绝对定位进行自适应布局的情况很少，一般绝对定位都用在尺寸固定的元素定位上。而且fixed定位的渲染效率很低，因为它会频繁触发浏览器的重排。


