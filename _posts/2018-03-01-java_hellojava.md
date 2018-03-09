---
layout: post
title:  "Java Hello"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java Hello
comments: 1
---
**변수 다루는 법**  

int :
{% highlight java linenos %}
//정수 연산은 int로 대체된다
byte a = 10;
byte b = 11;
//byte c = a + b; (x)
//int c = a + b; (o)
byte c = (byte) (a + b);
{% endhighlight %}


long :
{% highlight java linenos %}
//long 선언시 값마지막에 L붙여줌
long longA = 213984342L;
{% endhighlight %}


double, float :
{% highlight java linenos %}
//실수는 모두 double 로 대체된다
double dVal = 2.55556;
//float일 경우 값마지막에 f붙여줌
float fVal = 2.55556f;
{% endhighlight %}


실수 연산 :
{% highlight java linenos %}
//실수는 직접연산하지 않는다
float d = 3.14f;
float e = 4.1928f;
//float f = d + e;  (x)
float f = Float.sum(d, e);

double g = 5.223;
double h = 1.98343;
double i = Double.sum(g, h);
{% endhighlight %}


우선순위 :
{% highlight java linenos %}
//연산자 우선순위는 괄호로 하고 부족한부분은 검색
int j = (30 + 1) * 2 / (50 - 3);
{% endhighlight %}


int to String 메소드 :
{% highlight java linenos %}
/**
* 숫자를 문자로 변환
* @param number
* @return
*/
public String changeNumberToString(int number){
	return number + "";
}
{% endhighlight %}


String to int 메소드 :
{% highlight java linenos %}
/**
* 숫자인 문자열을 숫자로 변환
* @param word
* @return
*/
public int changeStringToInteger(String word){
	return Integer.parseInt(word);
}
{% endhighlight %}


String to long 메소드 :
{% highlight java linenos %}
/**
* long숫자인 문자열을 long으로 변환
* @param word
* @return
*/
public long changeStringToLong(String word){
	return Long.parseLong(word);
}
{% endhighlight %}


메소드 구조 :
{% highlight java linenos %}
접근제한자 리턴타입 함수명(파라미터타입 파라미터) {  
public  
private  
protected  
(default)  
}  
파라미터 사용 : java -c HelloMain.class a b c 1 22
{% endhighlight %}


연산 테스트 :
{% highlight java linenos %}
/**
* 연산테스트 메소드
*/
private static void calcTest(){
	int a = 2 + 3;
	int b = 2 - 3;
	int c = 2 * 3;
	int d = 2 / 3;//소수점이하 반올림(자동형변환)
	int e = 5 % 3;//5를 3으로 나눈 나머지
	int f = 10 % 3;//10을 3으로 나눈 나머지
	double dou = 5.0 % 4.2;
	System.out.println("2 + 3 = " + a);
	System.out.println("2 - 3 = " + b);
	System.out.println("2 * 3 = " + c);
	System.out.println("2 / 3 = " + d);
	System.out.println("5 % 3 = " + e);
	System.out.println("10 % 3 = " + f);
	System.out.println("5.0 % 4.2 = " + dou);
}
{% endhighlight %}


**조건문**  

if문 :
{% highlight java linenos %}
/**
 * 조건문 if
 */
public void checkIf(){
	int a = 10;
	int b = 5;

	if(a > b){
		//a가 b보다 크면 실행되는 영역
		System.out.println("a가 b보다 큽니다.");
	}else if(a == b){
		//a와 b가 같으면 실행되는 영역
	}else{
		//그외 조건일때 실행되는 영역
	}

}
{% endhighlight %}


switch문 :
{% highlight java linenos %}
/**
 * 조건문 switch
 * 한개의 변수를 대상으로 값이 같은지 체크할때 사용
 */
public void checkSwitch(){
	int a = 10;

	switch(a){
	case 5:
		System.out.println("a의 값이 5입니다.");
			break; //break가 없을시 아래코드까지 실행되므로 예외사항아닐시엔 항상 넣을것
	case 10:
		System.out.println("a의 값이 10입니다.");
		break;
	}
}
{% endhighlight %}


**반복문**  

for문 :
{% highlight java linenos %}
/**
 * 반복문 for
 * 배열의 인덱스는 0부터시작함
 */
public void checkFor(){
	int[] array = {1, 2, 3, 4, 5, 6, 7};
	//array[0] == 1
	//array[1] == 2

	//일반적인 for문
	//for(시작값; 조건; 증감값)
	for(int i = 0; i < array.length; i++){
		System.out.println(array[i]);
	}
	/* result
	 * 1
	 * 2
	 * 3
	 * 4
	 * 5
	 * 6
	 * 7
	 */

	//for(꺼낼타입 변수명 : 꺼낼배열)  향상된 for
	for(int item : array){
		System.out.println(item);
	}
	/* result
	 * 1
	 * 2
	 * 3
	 * 4
	 * 5
	 * 6
	 * 7
	 */
}
{% endhighlight %}


while문 :
{% highlight java linenos %}
/**
 * 반복문 while
 * 반복이 가능한 if문
 */
public void checkWhile(){
	int[] array = {1, 2, 3, 4, 5, 6, 7};

	int count = 0; // 시작값

	// while(조건식)  false가 될때까지 실행
	while(count < array.length){ // 종료값
		System.out.println(array[count]);
		count++; // 증감값
	}
}
{% endhighlight %}


do while문 :
{% highlight java linenos %}
/**
 * 반복문 do while
 * While은 조건식 체크후 동작하지만 Do While은 do블럭 실행후 조건식을 체크하므로
 * do블럭은 반드시 1번은 실행되는 방식
 */
public void checkDoWhile(){
	int[] array = {1, 2, 3, 4, 5, 6, 7};

	int count = 0;

	do{
		System.out.println(array[count]);
		count++; // 증감값
	}
	while(count < array.length);
}
{% endhighlight %}


**주석 종류** :
{% highlight java linenos %}
1.
  // 주석으로 처리할 내용

2.   
  /* 주석으로
      처리할
      내용   */

3.
  /**
  * 자바독에서 사용가능한 주석
  */
{% endhighlight %}