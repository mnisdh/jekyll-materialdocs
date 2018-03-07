---
layout: post
title:  "Tizen WebApp Vibrate"
date:   2017-03-06 17:30:13 +0800
categories: Tizen
tags: Tizen WebApp Vibrate Background
---
**Tizen Web application 개발시 진동기능 호출**

필요한 권한
config.xml :
{% highlight xml linenos %}
  <tizen:privilege name="http://tizen.org/privilege/alarm"/>
{% endhighlight %}

navigator의 vibrate 함수를 호출하여 사용하며  
기본 사용법은 vibrate 함수의 인자로 진동값 배열을 넣어주면됨  
인덱스 순서에따라 -> 0:진동, 1:간격, 2:진동, 4:간격 …  

Code :
{% highlight javascript linenos %}
  navigator.vibrate([500]);
  navigator.vibrate([100,100,100]);
{% endhighlight %}


foreground 상황에서는 위와같이 호출하면 정상동작 하지만  
background로 WebSocket 통신중 진동 기능을 호출하면 동작을 안함  
편법으로 아래와 같이 지연을 뒤서 호출하는 코드를 확인하여 처리함  

Code :
{% highlight javascript linenos %}
setTimeout(function (){
		navigator.vibrate([200,100,200,100,200,100,500]);
	}, 500);
{% endhighlight %}