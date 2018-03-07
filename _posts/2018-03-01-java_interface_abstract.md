---
layout: post
title:  "Java Interface / Abstract"
date:   2017-03-01 09:00:00 +0800
categories: Java
tags: Java Interface Abstract
---
**다형성의 성립조건**  
- 클래스 계층구조(상속관계)
- 메소드 재정의, 동적 바인딩
- 상위캐스팅 후 재정의 된 메소드 호출

**Interface**  
추상메소드들로만 이루어져 있으며 메소드의 선언만 가능하다  
인터페이스의 메소드는 표준화된 공통기능을 가진다  
인터페이스를 사용하기 위해서는 implements 키워드를 사용한다  
하나의 클래스가 여러개의 인터페이스를 implements 할 수 있다  

code :
{% highlight java linenos %}
public class Main{
  public static void main(String[] args){
    C c = new C();
    c.print();
    c.save();

    //아래와같이 인터페이스로 캐스팅해서 사용할수도 있음
    iA a = new C();
    a.print();

    iB b = new C();
    b.save();
  }
}

// 인터페이스
interface iA{
  public void print();
}

// 인터페이스
interface iB{
  public void save();
}

class C implements iA, iB{
  // 상속받은 메소드 재정의
  @Override
  public void print(){
    System.out.println("print");
  }

  // 상속받은 메소드 재정의
  @Override
  public void save(){
    System.out.println("save");
  }
}
{% endhighlight %}


**Abstract class**(추상 클래스)  
추상클래스는 반드시 하나이상의 추상메소드를 가지며 객체를 생성할 수 없다  
추상 클래스나 추상메소드를 선언 하기위해서는 이름 앞에 abstract 키워드를 추가해야한다  
추상클래스를 상속받기위해서는 extends 키워드를 사용해야한다  
하나의 클래스는 하나의 클래스만 extends 할 수 있다  

code :
{% highlight java linenos %}
public class Main{
  public static void main(String[] args){
    B b = new B();
    C c = new C();
    b.change();
    c.change();

    //아래와같이 부모클래스로 캐스팅해서 사용할수도 있음
    A b2 = new B();
    A c2 = new C();
    b2.change();
    c2.change();
  }
}

//추상 클래스(super클래스)
abstract class A{
  int x, y;
  public void size(int x, int y){
    this.x = x;
    this.y = y;
  }

  //추상메소드
  public abstract void change();
}

//서브 클래스
class B extends A{
  int width, height;

  //메소드 재정의
  @Override
  public void change(){
    System.out.println("B changed.");
  }
}

//서브 클래스
class C extends A{
  int a;

  //메소드 재정의
  @Override
  public void change(){
    System.out.println("C changed.");
  }
}
{% endhighlight %}