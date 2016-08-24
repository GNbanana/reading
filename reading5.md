##:after伪类+content内容生成经典应用举例
<br/><br/>
###一、content内容生成

content内容生成就是通过content属性生成内容，可以使用:before以及:after伪元素生成内容。

例如：

    h2:before {
       content: "我是额外文字！";
    }


此段样式的作用是在每个h2标签的前面添加文字“我是额外文字”。
<br/><br/>
###二、:after伪类+content 清除浮动的影响

一般不含包裹属性的div内部有浮动元素的话，那么这个浮动元素会让此div的高度塌陷。可以使用:after+content方法清除浮动造成的塌陷。使用如下：

    .fix:after{display:block; content:"clear"; height:0; clear:both; overflow:hidden; visibility:hidden;}

这样就可以让IE8+和其他浏览器清除浮动破坏带来的塌陷问题了。至于暂不支持:after伪类的IE6/IE7，可以使用IE私有的zoom缩放属性让div远离浮动的破坏。如下：

    .fix{*zoom:1;}
    .fix:after{display:block; content:"clear"; height:0; clear:both; overflow:hidden; visibility:hidden;}


清除浮动影响方法很多，添加包裹属性的元素，例如：position:absolute; display:inline-block; float:left; overflow:hidden等，但是有局限性。

<br/><br/>
###三、:after伪类+content 让大小不固定图片垂直居中

:after伪类+content实现的图片垂直居中方法：

CSS：

    .pic_box{width:300px; height:300px; background-color:#beceeb; font-size:0; *font-size:200px; text-align:center;}
    .pic_box img{vertical-align:middle;}
    .pic_box:after{display:inline-block; width:0; height:100%; content:"center"; vertical-align:middle; overflow:hidden;}

HTML：

    <div class="pic_box">
        <img data-src="1.jpg" />
    </div>


与清除浮动影响类似，IE6/7不支持:after伪类，可以用另外的方法让图片垂直居中，例如font-size方法，设一个比较大点的字体大小，IE6/7就可以实现图片垂直对齐了，至于其他浏览器，就用:after伪类+content内容生成一个vertical-align:middle属性的元素就可以了。

<br/><br/><br/>
##clear属性

clear属性指定：一个元素是紧挨着前面的浮动元素，还是必须移动到它们的下面（浮动被清除）。
clear属性既可以用于浮动元素，也可以用于非浮动元素。

当应用于非浮动块时，它将元素的边框边界移动到所有相关浮动元素外边界的下方。这个行为作用时会导致外边距折叠不起作用。

当应用于浮动元素时，它将元素的外边界移动到所有相关的浮动元素外边界的下方。这会影响后面浮动元素的布局，后面的浮动元素的位置无法高于它之前的元素。

要被清除的相关浮动元素指 在相同块级格式化上下文中的前置浮动。

注释:如果想要一个元素将所有浮动元素包含在内，既可以将这个容器设置为浮动，又可以通过 ::after 伪元素设置clear属性作为替代。

    #container:after {
     content: "";
     display: block;
     clear: both;
    }

值  
none：元素不会向下移动清除之前的浮动。  
left：元素被向下移动用于清除之前的左浮动。  
right：元素被向下移动用于清除之前的右浮动。  
both：元素被向下移动用于清除之前的左右浮动。

<br/><br/><br/>
##自适应网站的标准尺寸

PC机时：
@media only screen and (min-width: 960px){*{color:red;}}

平板横放时：
@media only screen and (min-width: 768px) and (max-width: 959px){*{color:green;}}

手机横放以及平板竖放时：
@media only screen and (min-width: 480px) and (max-width: 767px){*{color:purple;}}

手机竖放时：
@media only screen and (max-width: 479px){*{color:orange;}}

<br/><br/><br/>
##css元素隐藏
    { display: none; /* 不占据空间，无法点击 */ }

    { visibility: hidden; /* 占据空间，无法点击 */ }

    { position: absolute; clip:rect(1px 1px 1px 1px); /* 不占据空间，无法点击 */ }

    { position: absolute; top: -999em; /* 不占据空间，无法点击 */ }

    { position: relative; top: -999em; /* 占据空间，无法点击 */ }

    { position: absolute; visibility: hidden; /* 不占据空间，无法点击 */ }

    { height: 0; overflow: hidden; /* 不占据空间，无法点击 */ }

    { opacity: 0; filter:Alpha(opacity=0); /* 占据空间，可以点击 */ }

    { position: absolute; opacity: 0; filter:Alpha(opacity=0); /* 不占据空间，可以点击 */ }

    { 
        zoom: 0.001;
        -moz-transform: scale(0);
        -webkit-transform: scale(0);
        -o-transform: scale(0);
        transform: scale(0);
        /* IE6/IE7/IE9不占据空间，IE8/FireFox/Chrome/Opera占据空间。都无法点击 */
    }

    {
        position: absolute;
        zoom: 0.001;
        -moz-transform: scale(0);
        -webkit-transform: scale(0);
        -o-transform: scale(0);
        transform: scale(0); 
        /* 不占据空间，无法点击 */
    }    


###display:none和visibility:hidden的区别
1.空间占据  
2.回流与渲染  
3.株连性   

1.display:none隐藏后的元素不占据任何空间，而visibility:hidden隐藏的元素空间依旧存在  
2.display:none隐藏产生reflow和repaint(回流与重绘)，而visibility:hidden没有这个影响前端性能的问题  
3.display:none：一旦父节点元素应用了display:none，父节点及其子孙节点元素全部不可见  
  visibility:hidden：父元素应用visibility:hidden，则其子孙后代也都会全部不可见,但如果子孙元素应用了visibility:visible，那么这个子孙元素又会显现出来
  

###height:0和overflow:hidden的组合
position: absolute元素溢出overflow: hidden元素的时候，如果其第一个含有position属性(static除外)的祖先元素（一直到body）是overflow: hidden元素祖先元素的时候，则不隐藏；否则，隐藏。
  
    body
        height: 0; overflow: hidden;
            position: absolute; /* 不会被隐藏 */

    position: relative;
        height: 0; overflow: hidden;
            position: absolute; /* 不会被隐藏 */

    height: 0; overflow: hidden;  position: relative;
        position: absolute; /* 会被隐藏 */

    height: 0; overflow: hidden;
        position: relative;
            position: absolute; /* 会被隐藏 */
