---
layout: post
title:  "Java String"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java String
---
**String 함수**  

length(문자열의 길이) :
{% highlight java linenos %}
String a = "String/Test";

// 길이
System.out.println(a.length());
{% endhighlight %}


indexOf(문자열의 위치) :
{% highlight java linenos %}
// 위치검색
System.out.println(a.indexOf("T"));
System.out.println(a.indexOf("Test"));
{% endhighlight %}


split(문자열을 구분자 단위로 분해) :
{% highlight java linenos %}
// 특정 구분자로 분해
String[] temp = a.split("/");
for(String item : temp) System.out.println(item);

// 빈문자열로 자르면 문자열을 글자 하나 단위로 분해
String[] temp2 = a.split("");
{% endhighlight %}


substring(지정한 인덱스대로 문자열을 분해) :
{% highlight java linenos %}
// 문자열 자르기
// substring에서 인덱스는 문자열 앞으로 생각하고 사용
System.out.println(a.substring(0, 6));
{% endhighlight %}


replace(특정문자열을 지정한 문자열로 바꿈) :
{% highlight java linenos %}
// 문자열 바꾸기
System.out.println(a.replace("Te", "Px"));
{% endhighlight %}


startsWith(특정 문자열로 시작되는지 확인) :
{% highlight java linenos %}
// 특정 문자열로 시작되는지를 검사
System.out.println(a.startsWith("Str"));
{% endhighlight %}