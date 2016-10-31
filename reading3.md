##网页的全屏背景

1. 利用background-size 属性  

        html { 
          background: url(images/bg.jpg) no-repeat center center fixed; 
          -webkit-background-size: cover;
          -moz-background-size: cover;
          -o-background-size: cover;
          background-size: cover;
        }   

2. 使用内联元素&lt;img&gt;,设置了一个最小高度,并设置100%宽度

        img.bg {
          /* Set rules to fill background */
          min-height: 100%;
          min-width: 1024px;
	
          /* Set up proportionate scaling */
          width: 100%;
          height: auto;
	
          /* Set up positioning */
          position: fixed;
          top: 0;
          left: 0;
        }

          @media screen and (max-width: 1024px) { 
          /* Specific to this particular image */
          img.bg {
            left: 50%;
            margin-left: -512px;   /* 50% */
          }
        }

3. 把一个内联元素&lt;img&gt;定位到左上角，并给它设置最小宽度和100%高度 

        <img src="images/bg.jpg" id="bg" alt="">

        #bg {
          position: fixed; 
          top: 0; 
          left: 0; 
	
          /* Preserve aspet ratio */
          min-width: 100%;
          min-height: 100%;
        }

4. jQuery方法

    （1）

        <img src="images/bg.jpg" id="bg" alt=""> 

        #bg { position: fixed; top: 0; left: 0; }
        .bgwidth { width: 100%; }
        .bgheight { height: 100%; }

        $(window).load(function() {    

	           var theWindow        = $(window),
	               $bg              = $("#bg"),
	               aspectRatio      = $bg.width() / $bg.height();
	    			    		
	           function resizeBg() {
		
		            if ( (theWindow.width() / theWindow.height()) < aspectRatio ) {
		                $bg
		    	            .removeClass()
		    	            .addClass('bgheight');
		            } else {
		                $bg
		    	            .removeClass()
		    	            .addClass('bgwidth');
		            }
					
	           }
	                   			
	           theWindow.resize(resizeBg).trigger("resize");

         });

    （2）

        <img id="bg" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7" alt="" style="position: fixed; left: 0; top: 0" />

        (function() {

        var win = $(window);

        win.resize(function() {
    
            var win_w = win.width(),
                win_h = win.height(),
                $bg    = $("#bg");

            // Load narrowest background image based on 
            // viewport width, but never load anything narrower 
            // that what's already loaded if anything.
            var available = [
              1024, 1280, 1366,
              1400, 1680, 1920,
              2560, 3840, 4860
            ];

            var current = $bg.attr('src').match(/([0-9]+)/) ? RegExp.$1 : null;
    
            if (!current || ((current < win_w) && (current < available[available.length - 1]))) {
      
              var chosen = available[available.length - 1];
      
              for (var i=0; i<available.length; i++) {
                if (available[i] >= win_w) {
                  chosen = available[i];
                  break;
                }
              }
      
              // Set the new image
              $bg.attr('src', '/img/bg/' + chosen + '.jpg');
      
              // for testing...
              // console.log('Chosen background: ' + chosen);
      
            }

            // Determine whether width or height should be 100%
            if ((win_w / win_h) < ($bg.width() / $bg.height())) {
              $bg.css({height: '100%', width: 'auto'});
            } else {
              $bg.css({width: '100%', height: 'auto'});
            }
    
          }).resize();
  
        })(jQuery);


##流式栅格系统

###基本的流式栅格HTML代码片段

将 .row 替换为 .row-fluid 就能让任何一行“流动”起来。应用于每一列的类不用改变，这样能方便的在流式与固定栅格之间切换。
    
    <div class="row-fluid">
      <div class="span4">...</div>
      <div class="span8">...</div>
    </div>

###流式栅格的偏移

定义方式和固定网格系统相同：给任何想偏移的列添加 .offset* 即可。

    <div class="row-fluid">
      <div class="span4">...</div>
      <div class="span4 offset2">...</div>
    </div>

###流式嵌套布局

和固定栅格的嵌套有一点不同：被嵌套的列数之和要等于12。这是因为流式栅格使用百分比来设置每列的宽度。

    <div class="row-fluid">
      <div class="span12">
        Fluid 12
        <div class="row-fluid">
          <div class="span6">
            Fluid 6
            <div class="row-fluid">
              <div class="span6">Fluid 6</div>
              <div class="span6">Fluid 6</div>
            </div>
          </div>
          <div class="span6">Fluid 6</div>
        </div>
      </div>
    </div>


##布局

###固定布局

提供了一个通用的固定宽度(也可以变为响应式)的布局方式，仅仅用 &lt;div class="container"&gt; 即可。

    <body>
      <div class="container">
        ...
      </div>
    </body>

###流式布局
利用&lt;div class="container-fluid"&gt; 代码可以创建一个流式、两列的页面 — 非常适合于应用和文档类页面。

    <div class="container-fluid">
      <div class="row-fluid">
        <div class="span2">
          <!--Sidebar content-->
        </div>
        <div class="span10">
         <!--Body content-->
        </div>
      </div>
    </div>

<br/><br/>
**最近遇到的一个图片滚动的代码**

    <body>
    <center>
    <div class="blk_18"> 
      <div class="pcont" id="ISL_Cont_1">
        <div class="ScrCont">
          <div id="List1_1">
            <a class="pl" ><img src="1.jpg" width="100" height="100" /></a>
            <a class="pl" ><img src="2.jpg" width="100" height="100" /></a>
            <a class="pl" ><img src="3.jpg" width="100" height="100" /></a>
            <a class="pl" ><img src="4.jpg" width="100" height="100" /></a>
            <a class="pl" ><img src="5.jpg" width="100" height="100" /></a>
            <a class="pl" ><img src="6.jpg" width="100" height="100" /></a>
          </div>
          <div id="List2_1"></div>
        </div>
      </div>
    </div>
    <div class="botton">
      <a class="LeftBotton" onmousedown="ISL_GoUp_1()" onmouseup="ISL_StopUp_1()" onmouseout="ISL_StopUp_1()" href="javascript:void(0);" target="_self"></a>
      <a class="RightBotton" onmousedown="ISL_GoDown_1()" onmouseup="ISL_StopDown_1()" onmouseout="ISL_StopDown_1()" href="javascript:void(0);" target="_self"></a> 
    </div>

    <script type="text/javascript">picrun_ini()</script>
    </center>
    </body>

css代码

    .blk_18 { overflow:hidden; zoom:1; font-size:9pt; width:100%; margin-top:8px; text-align:center; }
    .blk_18 .pcont { width:100%; float:left; overflow:hidden; padding-left:5px; }
    .blk_18 .ScrCont { width:32766px; zoom:1; margin-left:-5px; }
    .blk_18 #List1_1, .blk_18 #List2_1 { float:left; }
    .botton { padding-top:20px; display:table-cell; vertical-align:middle; }
    .LeftBotton { width:50px; height:50px; float:left; background:url(left.jpg) no-repeat; margin-right:10px; }
    .RightBotton { width:50px; height:50px; float:left; background:url(right.jpg) no-repeat; margin-left:10px; }
    .blk_18 .pl img { display:block; cursor:pointer; border:none; margin:6px auto 1px auto; }
    .blk_18 .pl { width:220px; height:310px; float:left; text-align:center;}

js代码

    var Speed_1 = 10; //速度(毫秒)
    var Space_1 = 20; //每次移动(px)
    var PageWidth_1 = 107 * 6; //翻页宽度
    var interval_1 = 5000; //翻页间隔时间
    var fill_1 = 0; //整体移位 
    var MoveLock_1 = false;
    var MoveTimeObj_1;
    var MoveWay_1="right";
    var Comp_1 = 0;
    var AutoPlayObj_1=null;
    function GetObj(objName){if(document.getElementById){return eval('document.getElementById("'+objName+'")')}else{return eval('document.all.'+objName)}}
    function AutoPlay_1(){clearInterval(AutoPlayObj_1);AutoPlayObj_1=setInterval('ISL_GoDown_1();ISL_StopDown_1();',interval_1)}
    function ISL_GoUp_1(){if(MoveLock_1)return;clearInterval(AutoPlayObj_1);MoveLock_1=true;MoveWay_1="left";MoveTimeObj_1=setInterval('ISL_ScrUp_1();',Speed_1);}
    function ISL_StopUp_1(){if(MoveWay_1 == "right"){return};clearInterval(MoveTimeObj_1);if((GetObj('ISL_Cont_1').scrollLeft-fill_1)%PageWidth_1!=0){Comp_1=fill_1-(GetObj('ISL_Cont_1').scrollLeft%PageWidth_1);CompScr_1()}else{MoveLock_1=false}
    AutoPlay_1()}
    function ISL_ScrUp_1(){if(GetObj('ISL_Cont_1').scrollLeft<=0){GetObj('ISL_Cont_1').scrollLeft=GetObj('ISL_Cont_1').scrollLeft+GetObj('List1_1').offsetWidth}
    GetObj('ISL_Cont_1').scrollLeft-=Space_1}
    function ISL_GoDown_1(){clearInterval(MoveTimeObj_1);if(MoveLock_1)return;clearInterval(AutoPlayObj_1);MoveLock_1=true;MoveWay_1="right";ISL_ScrDown_1();MoveTimeObj_1=setInterval('ISL_ScrDown_1()',Speed_1)}
    function ISL_StopDown_1(){if(MoveWay_1 == "left"){return};clearInterval(MoveTimeObj_1);if(GetObj('ISL_Cont_1').scrollLeft%PageWidth_1-(fill_1>=0?fill_1:fill_1+1)!=0){Comp_1=PageWidth_1-GetObj('ISL_Cont_1').scrollLeft%PageWidth_1+fill_1;CompScr_1()}else{MoveLock_1=false}
    AutoPlay_1()}
    function ISL_ScrDown_1(){if(GetObj('ISL_Cont_1').scrollLeft>=GetObj('List1_1').scrollWidth){GetObj('ISL_Cont_1').scrollLeft=GetObj('ISL_Cont_1').scrollLeft-GetObj('List1_1').scrollWidth}
    GetObj('ISL_Cont_1').scrollLeft+=Space_1}
    function CompScr_1(){if(Comp_1==0){MoveLock_1=false;return}
    var num,TempSpeed=Speed_1,TempSpace=Space_1;if(Math.abs(Comp_1)<PageWidth_1/2){TempSpace=Math.round(Math.abs(Comp_1/Space_1));if(TempSpace<1){TempSpace=1}}
    if(Comp_1<0){if(Comp_1<-TempSpace){Comp_1+=TempSpace;num=TempSpace}else{num=-Comp_1;Comp_1=0}
    GetObj('ISL_Cont_1').scrollLeft-=num;setTimeout('CompScr_1()',TempSpeed)}else{if(Comp_1>TempSpace){Comp_1-=TempSpace;num=TempSpace}else{num=Comp_1;Comp_1=0}
    GetObj('ISL_Cont_1').scrollLeft+=num;setTimeout('CompScr_1()',TempSpeed)}}
    function picrun_ini(){
    GetObj("List2_1").innerHTML=GetObj("List1_1").innerHTML;
    GetObj('ISL_Cont_1').scrollLeft=fill_1>=0?fill_1:GetObj('List1_1').scrollWidth-Math.abs(fill_1);
    GetObj("ISL_Cont_1").onmouseover=function(){clearInterval(AutoPlayObj_1)}
    GetObj("ISL_Cont_1").onmouseout=function(){AutoPlay_1()}
    AutoPlay_1();
    }


