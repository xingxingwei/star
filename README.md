事件捕获的三种方法：
- 使用内联模式
- 使用传统模式
- 使用更现代的addEventListener/attachEvent方法

```
<html lang="en">
 <head>
  <title>事件处理</title>
  <script>
	function helloMsg(){
		var helloString="1hello";
		alert(helloString);
	}
	//////////////////
		//传统模式
	function helloTwice(){
		var helloString="2hi ";
		alert(helloString);
	}
	window.onload=helloMsg;

	//////////////////
	  //DOM Level2时间模式
	function helloThree(){
		var helloString="3world ";
		alert(helloString);
	}
	window.addEventListener("load",helloThree,false);


  </script>
 </head>
 <body  onload="helloTwice();"><!--内联模式-->
  
 </body>
</html>

```
可复用的跨浏览器兼容的事件处理函数

```
function catchEvent(eventObj,event,eventHandler){
    if(eventObj.addEventListener){
        eventObj.addEventListener(event,eventHandler,false);
    }else if(eventObj.attachEvent){
        event="on"+event;
        eventObj.attachEvent(event,eventHandler);
    }else{
        event="on"+event;
        eventObj.event=eventHandler;
    }
}
```
取消一个事件

```
function cancelEvent(event){
    if(event.preventDefault){//针对其他浏览器
        event.preventDefault();
        event.stopPropagation();
    }else{//针对IE
        event.returnValue=false;
        event.cancelBubble=true;
    }
}
```
