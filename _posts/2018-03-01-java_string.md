---
layout: post
title:  "Java String"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java String
---
### length - 문자열의 길이를 구한다  

```Java
String a = "String/Test";

// 길이
System.out.println(a.length());
```


### indexOf - 문자열의 위치를 리턴한다

```Java
// 위치검색
System.out.println(a.indexOf("T"));
System.out.println(a.indexOf("Test"));
```


### split - 문자열을 구분자 단위로 분해한다

```java
// 특정 구분자로 분해
String[] temp = a.split("/");
for(String item : temp) System.out.println(item);

// 빈문자열로 자르면 문자열을 글자 하나 단위로 분해
String[] temp2 = a.split("");
```


### substring - 지정한 인덱스대로 문자열을 분해한다

```java
// 문자열 자르기
// substring에서 인덱스는 문자열 앞으로 생각하고 사용
System.out.println(a.substring(0, 6));
```


### replace - 특정문자열을 지정한 문자열로 바꾼다

```java
// 문자열 바꾸기
System.out.println(a.replace("Te", "Px"));
```


### startsWith - 특정 문자열로 시작되는지 확인한다

```Java
// 특정 문자열로 시작되는지를 검사
System.out.println(a.startsWith("Str"));
```
