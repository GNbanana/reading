

#<center>bootstrap笔记</center>


----------
##基本的HTML模版  

    <!DOCTYPE html>
    <html>
      <head>
        <title>Bootstrap 101 Template</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- Bootstrap -->
        <link href="css/bootstrap.min.css" rel="stylesheet" media="screen">
      </head>
      <body>
        <h1>Hello, world!</h1>
        <script src="http://code.jquery.com/jquery.js"></script>在本页面引用此函数库以便本页面调用里面的函数
        <script src="js/bootstrap.min.js"></script>加载当前页面目录中名为js的子目录下面的js包
      </body>
    </html>

在一个典型的html文件中加入了相应的CSS和JS文件，使其成为一个Bootstrap模板，加入这两个文件之后就可以用Bootstrap开发任何网站和应用程序了。           
<br/>

##排版和链接

Bootstrap 为屏幕、排版和链接设置了基本的全局样式。尤其是:  

- 移除了body的 margin  
- 设置了 body 的背景颜色 background-color: white;  
- 使用 @baseFontFamily、@baseFontSize 和@baseLineHeight 属性作为我们排版的基础  
- 通过 @linkColor 设置全局链接颜色，并且，当链接处于 :hover 状态时才会带有下划线  
<br/>

##栅格系统示例

Bootstrap默认的栅格系统为12列 ，形成一个940px宽的容器，默认没有启用 响应式布局特性 。如果加入响应式布局CSS文件，栅格系统会自动根据可视窗口的宽度从724px到1170px进行动态调整。在可视窗口低于767px宽的情况下，列将不再固定并且会在垂直方向堆叠。
<br/>
##带有基本栅格的HTML代码

对于简单的两列式布局，创建一个 .row 容器，并在容器中加入合适数量的 .span* 列即可。由于默认是12列的栅格，所有 .span* 列所跨越的栅格数之和最多是12(或者等于其父容器的栅格数)。
    
    <div class="row">
      <div class="span4">...</div>
      <div class="span8">...</div>
    </div>
<br/>

##偏移列

把列向右移动可使用 .offset* 类。每个类都给列的左边距增加了指定单位的列。例如，.offset4 将 .span4 右移了4个列的宽度。

    <div class="row">
      <div class="span4">...</div>
      <div class="span3 offset2">...</div>
    </div>


##嵌套列

在默认的栅格系统里, 在已有的.span*内添加一个新的 .row 并加入 .span* 列，就可实现嵌套。被嵌套列中的每列列数总和要等于父级列。

    <div class="row">
      <div class="span9">
        Level 1 column
        <div class="row">
          <div class="span6">Level 2</div>
          <div class="span3">Level 2</div>
        </div>
      </div>
    </div>



##在HTML中引入CSS的方法主要有四种

###1.行内式
在标记的style属性中设定CSS样式。
###2.嵌入式
将CSS样式集中写在<head></head>标签对的<style></style>标签对中。
缺点是对于一个包含很多网页的网站，在每个网页中使用嵌入式，进行修改样式时非常麻烦。单一网页可以考虑使用嵌入式。

###3.导入式
将一个独立的.css文件引入HTML文件中，导入式使用CSS规则引入外部CSS文件，&lt;style&gt;标记也是写在&lt;head&gt;标记中，使用的语法如下：

    <style type="text/css">
      @import"mystyle.css"; 此处要注意.css文件的路径
    </style>

导入式会在整个网页装载完后再装载CSS文件，因此这就导致了一个问题，如果网页比较大则会儿出现先显示无样式的页面，闪烁一下之后，再出现网页的样式。这是导入式固有的一个缺陷。

###4.链接式
也是将一个.css文件引入到HTML文件中，但它与导入式不同的是链接式使用HTML规则引入外部CSS文件,它在网页的&lt;head&gt; &lt;/head&gt;标签对中使用<link>标记来引入外部样式表文件，使用语法如下：

    <link href="mystyle.css" rel="stylesheet" type="text/css"/>

使用链接式时与导入式不同的是它会以网页文件主体装载前装载CSS文件，因此显示出来的网页从一开始就是带样式的效果的，它不会象导入式那样先显示无样式的网页，然后再显示有样式的网页，这是链接式的优点。

总结：一般来说，做网站时把样式多写在多个样式表文件中，因此先用链接式引入一个总的CSS文件，然后在这个CSS文件中在使用导入式来引入其他的CSS文件。但如果通过JavaScrip来动态引入CSS文件则只能使用链接式。


##一些语法

- @media all and (max-width: 500px) {} 意思就是在所有媒介下，浏览器宽度小于等于500px的时候使用{}里的样式  



- absolute指绝对位置，就是说设定后该控件是固定在页面的某处，不会因其他控件的大小变化而影响到其分布位置的改变。position指一般位置，就是说设定后该控件在无其他控件的影响下，其位置位于你设定的地方。如果其他控件的大小占用了你设定的位置，那么原先就会让出位置啦。relative指相对位置，就是相对来说的，比如控件与控件之间的相对位置，控件与面页的相对位置，打个比方，控件A和控件B是相对位置，那么当控件A的位置发生改变时，控件B 也跟着改变。  



- min-height就是你的层的最小高度，如果该层中的元素内容高度小于这个高度，就将层显示为min-height的值，超过的话，就撑破层，使层的高度与元素内容高度一样。  
max-height就是和这个相反了，不超出的话，层高度就和层中内容元素高度一样，否则就截断内容，显示max-height的高度。  
line-height是行高，就是针对文本的，即一行文字的行高，是以该标签中文字大小font-size做比较的，例如line-height=200%；就是让行高是文字大小的两倍  



- **text-shadow属性**    
text-shadow:1px 1px 1px rgba(0,0,0,.3);  
none：无阴影    
<length>①：第1个长度值用来设置对象的阴影水平偏移值。可以为负值  
<length>②：第2个长度值用来设置对象的阴影垂直偏移值。可以为负值  
<length>③：如果提供了第3个长度值则用来设置对象的阴影模糊值。不允许负值  
<color>：设置对象的阴影的颜色。  



- **cursor** 属性  
该属性定义了鼠标指针放在一个元素边界范围内时所用的光标形状  
