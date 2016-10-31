##div垂直居中的N种方法

###一、单行垂直居中 
如果一个容器中只有一行文字，对它实现居中相对比较简单，只需要设置它的实际高度height和所在行的高度line-height相等即可。
如：
  
    div {   
        height:25px;   
        line-height:25px;    
    }   

###二、多行未知高度文字的垂直居中 
如果一段内容，它的高度是可变的,那么就可以设定Padding，使上下的padding值相同即可。同样的，这也是一种“看起来”的垂直居中方式，它只不过是使文字把<div>完全填充的一种访求而已。可以使用类似下面的代码：  

    div {   
        padding:25px;   
    } 
  
这种方法的优点就是它可以在任何浏览器上运行，并且代码很简单，只不过这种方法应用的前提就是容器的高度必须是可伸缩的。  

###三、多行文本固定高度的居中 
CSS中的vertical-align属性只会对拥有valign特性的(X)HTML标签起作用，但是在CSS中还有一个display属性能够模拟<table>，所以可以使用这个属性来让<div>模拟<table>就可以使vertical-align了。注意，display:table和display:table-cell的使用方法，前者必须设置在父元素上，后者必须设置在子元素上，因此要为需要定位的文本再增加一个<div>元素： 
 
    div#wrap {   
        height:400px;   
        display:table;   
    }   
    div#content {   
        vertical-align:middle;   
        display:table-cell;   
        border:1px solid #FF0099;   
        background-color:#FFCCFF;   
        width:760px;   
    }   

这个方法应该是很理想了，但是Internet Explorer 6 并不能正确地理解display:table和display:table-cell，因此这种方法在
Internet Explorer 6及以下的版本中是无效的。

### 四、在Internet Explorer中的解决方案 
在Internet Explorer 6及以下版本中，在高度的计算上存在着缺陷的。在Internet Explorer 6中对父元素进行定位后，如果再对子元素进行百分比计算时，计算的基础似乎是有继承性的（如果定位的数值是绝对数值没有这个问题，但是使用百分比计算的基础将不再是该元素的
高度，而从父元素继承来的定位高度）。例如，有下面这样一个(X)HTML代码段：  

    <div id="wrap">  
        <div id="subwrap">  
            <div id="content">  
            </div>  
        </div>
    </div>

如果对subwrap进行了绝对定位，那么content也会继承了这个这个属性，虽然它不会在页面中马上显示出来，但是如果再对content进行相对定位的时候，你使用的100%分比将不再是content原有的高度。例如，设定了subwrap的position为40%，如果想使content的上边缘和wrap重合的话就必须设置top:-80%;那么，如果设定subwrap的top:50%的话，必须使用100%才能使content回到原来的位置上去，但是如果把content也设置50%呢？那么它就正好垂直居中了。所以可以使用这中方法来实现Internet Explorer 6中的垂直居中：  

    div#wrap {   
        border:1px solid #FF0099;   
        background-color:#FFCCFF;   
        width:760px;   
        height:400px;   
        position:relative;   
    }   
    div#subwrap {   
        position:absolute;   
        border:1px solid #000;   
        top:50%;   
    }   
    div#content {   
        border:1px solid #000;   
        position:relative;   
        top:-50%;   
    }  
 
当然，这段代码只能在Internet Exlporer 6等计算存在问题的浏览器中才会有作用。（

###五、完美的解决方案 
综合上面两种方法就可以得到一个完美的解决方案，不过这要用到CSS hack的知识。对于如果使用CSS Hack来区分浏览器：  
    div#wrap {   
        display:table;   
        border:1px solid #FF0099;   
        background-color:#FFCCFF;   
        width:760px;   
        height:400px;   
        _position:relative;   
        overflow:hidden;   
    }   
    div#subwrap {   
        vertical-align:middle;   
        display:table-cell;   
        _position:absolute;   
        _top:50%;   
    }   
    div#content {   
        _position:relative;   
        _top:-50%;   
    }   
    

##css的div垂直居中的方法，百分比div垂直居中
###固定高宽div垂直居中
 
    div{
        position: absolute;
        left: 50%;
        top: 50%;
        width:200px;
        height:100px;
        margin-left:-100px;
        margin-top:-50px;
    }

###不固定高宽div垂直居中的方法

**方法一**：  
用一个“ghost”伪元素（看不见的伪元素）和 inline-block / vertical-align 可以搞定居中，非常巧妙。但是这个方法要求待居中的元素是 inline-block，不是一个真正通用的方案。

    .block {  
        text-align: center;  
    }

    .block:before {
        content: '';
        display: inline-block;
        height: 100%;
        vertical-align: middle;
        margin-right: -0.25em; 
    }

    .centered {
        display: inline-block;
        vertical-align: middle;
        width: 50%;
    }


**方法二**：
可以用table布局方法，但是这种方法也有局限性！
写法如下：

    <div class="something-semantic">
       <div class="something-else-semantic">
       </div>
    </div>

    .something-semantic {
        display: table;
        width: 100%;
    }
    .something-else-semantic {
        display: table-cell;
        text-align: center;
        vertical-align: middle;
    }



**方法三**，终极解决方法：
以上2中方法可能都有其局限性，我介绍的第三中方法是比较成熟的不是固定高宽div的垂直居中的方法！但是方法是css3的写法，想兼容IE8的童鞋们，建议用上面的方法！
方法和我们固定高宽的差不多，但是不用margin我们用的是 translate()
demo如下：

        position: fixed;
        top: 50%;
        left: 50%;
        background-color: #000;
        width:50%;
        height: 50%;
        -webkit-transform: translateX(-50%) translateY(-50%);
        -moz-transform: translateX(-50%) translateY(-50%);
        -ms-transform: translateX(-50%) translateY(-50%);
        transform: translateX(-50%) translateY(-50%);




**方法四**：css3不定宽高水平垂直居中

    justify-content:center;//子元素水平居中   
    align-items:center;//子元素垂直居中  
    display:-webkit-flex;

在父级元素上面加上上面3句话，就可以实现子元素水平垂直居中



<br/><br/>
##纯CSS3实现绘制各种图形

###制作圆形：
圆形在设置CSS时要设置宽度和高度相等，然后设置border-radius属性为宽度或高度的一半即可：

    #circle {
        width: 120px;
        height: 120px;
        background: #7fee1d;
        -moz-border-radius: 60px;
        -webkit-border-radius: 60px;
        border-radius: 60px;
    } 
<br/>

###制作椭圆形：

设置椭圆形的CSS时，高度要设置为宽度的一半，border-radius属性也要做相应的改变：

     #oval {
        width: 200px;
        height: 100px;
        background: #e9337c;
        -webkit-border-radius: 100px / 50px;
        -moz-border-radius: 100px / 50px;
        border-radius: 100px / 50px;
    } 
<br/>

###制作三角形：

要创建一个CSS三角形，需要使用border，通过设置不同边的透明效果，我们可以制作出三角形的现状。另外，在制作三角形时，宽度和高度要设置为0。 
                           
    #triangle {
        width: 0;
        height: 0;
        border-bottom: 140px solid #fcf921;
        border-left: 70px solid transparent;
        border-right: 70px solid transparent;
    } 
<br/>

###制作倒三角形：
与正三角形不同的是，倒三角形要设置的是border-top、border-left和border-right三条边的属性：
    
    #triangle {    
        width: 0;    
        height: 0;    
        border-top: 140px solid #20a3bf;    
        border-left: 70px solid transparent;    
        border-right: 70px solid transparent;
    }

注：在页面的边缘制作倒三角还可以通过制作一个正方形旋转45度后定位实现，例如页面上边缘：
   
    #triangle {    
        width: 200px;    
        height: 200px;    
        position:absolute;
        top:0;
        -webkit-transform:translateY(-50%) roate(45deg);
        -moz-transform:translateY(-50%) roate(45deg);
        -ms-transform:translateY(-50%) roate(45deg);
        -o-transform:translateY(-50%) roate(45deg);
        transform:translateY(-50%) roate(45deg);
    }
   
<br/>

###制作左三角形：
左三角形操作的是border-top、border-left和border-right三条边的属性，其中上边和下边要设置透明属性。
    
    #triangle_left {    
        width: 0;    
        height: 0;    
        border-top: 70px solid transparent;    
        border-right: 140px solid #6bbf20;    
        border-bottom: 70px solid transparent;
    }    
<br/>

###制作菱形
制作菱形的方法有很多种。这里使用的是transform属性和rotate相结合，使两个正反三角形上下显示。

    #diamond {
        width: 120px;
        height: 120px;
        background: #1eff00;
    /* Rotate */
        -webkit-transform: rotate(-45deg);
        -moz-transform: rotate(-45deg);
        -ms-transform: rotate(-45deg);
        -o-transform: rotate(-45deg);
        transform: rotate(-45deg);
    /* Rotate Origin */
        -webkit-transform-origin: 0 100%;
        -moz-transform-origin: 0 100%;
        -ms-transform-origin: 0 100%;
        -o-transform-origin: 0 100%;
        transform-origin: 0 100%;
        margin: 60px 0 10px 310px;
    }  
<br/>

###制作梯形：

梯形是三角形的一个变体，设置CSS梯形时，左右两条边设置为相等，并且给它设置一个宽度。

    #trapezium {
        height: 0;
        width: 120px;
        border-bottom: 120px solid #ec3504;
        border-left: 60px solid transparent;
        border-right: 60px solid transparent;
    } 
<br/>

###制作平行四边形：

平行四边形的制作方式是使用transform属性使长方形倾斜一个角度。

    #parallelogram {
        width: 160px;
        height: 100px;
        background: #8734f7;
        -webkit-transform: skew(30deg);
        -moz-transform: skew(30deg);
        -o-transform: skew(30deg);
        transform: skew(30deg);
    }  