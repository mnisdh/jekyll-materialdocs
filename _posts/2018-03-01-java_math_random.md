---
layout: post
title:  "Java Math Random"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java Math Random
---
**숫자계산**  

- 1 ~ max까지 더하는 메소드
```
	1 2 3 4 5 6 7 8
	8 7 6 5 4 3 2 1
	| | | | | | | |
	9 9 9 9 9 9 9 9

	(1 + 8) * 8 / 2 = 36
```
code :
{% highlight java linenos %}
/**
 * 1 ~ max 까지 더하는 함수
 * @param max
 * @return
 */
public long sum(long max){
	long sum = (max + 1) * max / 2;
	//for(int i = 1; i <= max; i++) sum += i;

	return sum;
}
{% endhighlight %}


- 1 ~ max까지 홀수만 더하는 메소드
```
	1 3 5     = 9     3 * 3 = 9
	1 3 5 7   = 16    4 * 4 = 16
	1 3 5 7 9 = 25    5 * 5 = 25

	홀수갯수의 제곱
```
code :
{% highlight java linenos %}
/**
 * 1 ~ max 까지 홀수만 더하는 함수(홀수갯수의 제곱)
 * @param max
 * @return
 */
public long sumOdd(long max){
	long count = 0;
	if(max % 2 == 1) max++;

	count = max / 2;

	return count * count;
}
{% endhighlight %}


- 1 ~ max까지 짝수만 더하는 메소드
```
	2 4     = 9     2 * 2 + 2 = 6
	2 4 6   = 16    3 * 3 + 3 = 12
	2 4 6 8 = 25    4 * 4 + 4 = 20

	짝수갯수의 제곱 + 짝수갯수
```
code :
{% highlight java linenos %}
/**
 * 1 ~ max 까지 짝수만 더하는 함수(짝수갯수의 제곱 + 짝수갯수)
 * @param max
 * @return
 */
public long sumEven(long max){
	long count = 0;
	if(max % 2 == 1) max--;

	count = max / 2;

	return count * count + count;
}
{% endhighlight %}


**Math 관련**  

abs(절대값) :
{% highlight java linenos %}
int a = Math.abs(-123);
{% endhighlight %}

round(반올림) :
{% highlight java linenos %}
long b = Math.round(123.5);
{% endhighlight %}

ceil(올림) :
{% highlight java linenos %}
double c = Math.ceil(123.4);
{% endhighlight %}

floor(내림) :
{% highlight java linenos %}
double d = Math.floor(123.5);
{% endhighlight %}

random(랜덤값) :
{% highlight java linenos %}
Math.random(); // 0보다 크가나 같고 1보다 작은 실수를 리턴
{% endhighlight %}

일반적인 Random값 사용 :
{% highlight java linenos %}
Random random = new Random();
// 1부터 100사이의 랜덤한 숫자 가져오기
random.nextInt(100); // 0 ~ 99사이의 정수가 리턴
int r = random.nextInt(100) + 1; // 1~ 100사이의 정수가 리턴
{% endhighlight %}