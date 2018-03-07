---
layout: post
title:  "Tizen WebApp WebSocket"
date:   2017-03-06 17:35:13 +0800
categories: Tizen
tags: Tizen WebApp WebSocket Background
---
**Tizen Web application 개발시 WebSocket 사용**

필요한 권한
config.xml :
{% highlight xml linenos %}
  <tizen:privilege name="http://tizen.org/privilege/internet"/>
{% endhighlight %}

Tizen Web application 은 javascript, html5를 지원하며  
현재 프로젝트에서 서버와 UDP통신을 하도록 설계되어 있었으나  
javascript, html5, tizen 기본 제공모듈 에는 UDP, TCP 통신은 포함되어있지 않아서  
결국 html5가 지원하는 WebSocket방식으로 변경하게 되었음  
[참고한 Tizen Developer사이트 공식문서](https://developer.tizen.org/ko/community/tip-tech/html5-features-on-tizen?langswitch=ko)

현재 프로젝트는 WebSocket에 항상 연결되어있어야 하므로  
onclose()호출시 다시 커넥션 맺도록 되어있음  
message를 받게되면 알람함수를 호출함  

Code :
{% highlight javascript linenos %}
var serverAddr = "ws://" + widget.preferences.getItem("ip") + ":" + widget.preferences.getItem("port");
var ws;
var isFinish = false;

function webSocketStart(){
    try {
    	ws = new WebSocket(serverAddr);
    	ws.onmessage = function(event) {
	    	onAlarm(event.data);
	    };
	    ws.onclose = function(){
	    	if(!isFinish){
	    		setTimeout(function(){ webSocketStart(); }, 1000);
	    	}
	    };
    } catch ( e ) {
    	if(!isFinish){
    		setTimeout(function(){ webSocketStart(); }, 1000);
    	}
    }
}
{% endhighlight %}