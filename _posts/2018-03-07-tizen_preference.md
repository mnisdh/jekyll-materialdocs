---
layout: post
title:  "Tizen WebApp Preference"
date:   2017-03-07 09:12:00 +0800
categories: Tizen
tags: Tizen WebApp Preference
comments: 1
---
**Tizen Web application 개발시 Preference 사용**

Config.xml 에 Preference를 미리 설정해두고 해당 Preference에 값을 가져오거나 설정하여 사용  
설정에 대한 값들을 관리하기 위해 사용함  

config.xml :
{% highlight xml linenos %}
  <preference name="test" value="1" readonly="false"/>
  <preference name="test2" value="2" readonly="false"/>
{% endhighlight %}


위에서 정의한 Preference의 사용법  

Code :
{% highlight javascript linenos %}
var value = widget.preferences.getItem("test"); 
widget.preferences.setItem("test",2);
{% endhighlight %}