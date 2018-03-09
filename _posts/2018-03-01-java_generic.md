---
layout: post
title:  "Java Generic"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java Generic
comments: 1
---
**Generic**  
- 클래스의 타입을 parameter로 만든 것이다
- 다루는 클래스의 타입을 일반적으로 선언하면서도 Object가 아닌 실제 클래스 타입을 명시하므로써 형변환없이도 사용할수 있게 해준다
- Object로 여러 타입을 받아서 사용할 수있으나 형변환을 잘못하면 runtime시에 잘못을 확인되는데 Generic사용시는 사전에 타입을 확인하므로 유용하다


Class에서 사용시 :
{% highlight java linenos %}
public class Part<T> {
	private T part;

	public void set(T part) { this.part = part; }

	public T get() { return this.part; }
}

public class Test(){
	public static void Main(String[] args){
		Part<String> part = new Part<>();
		// String 이외의 다른타입은 넣을수 없음
		part.set("test");
		String text = part.get();
	}
}
{% endhighlight %}


생성자에서 사용시 :
{% highlight java linenos %}
public class Part<T, S>{
	private T item1;
	private S item2;

	public Part(T t, S s){
		this.item1 = t;
		this.item2 = s;
	}
}
{% endhighlight %}


Method에서 사용시 :
{% highlight java linenos %}
//Class에선 T를 사용하지만
//별개로 메소드에서 U로 다른 타입을 설정해서 사용가능함
public class Part<T>{
	public <U> void printPart(U info){
		System.out.println(info);
	}
}
{% endhighlight %}