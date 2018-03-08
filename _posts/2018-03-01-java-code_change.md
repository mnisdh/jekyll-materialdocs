---
layout: post
title:  "Java Code 잔돈계산"
date:   2017-03-01 09:00:00 +0800
categories: Java-Code
tags: Java Code 잔돈계산 Interface
---
**잔돈계산**  

ChangeMain class(main) :
{% highlight java linenos %}
// 지불금액과 구입금액을 입력받아 잔돈 계산
public static void main(String[] args){
	Scanner scanner = new Scanner(System.in);

	System.out.print("지불금액 : ");
	int num1 = scanner.nextInt();
	System.out.print("구입금액 : ");
	int num2 = scanner.nextInt();

	//반복문 사용한 코드
	Change change = new Change();
	change.calc(num1, num2);

	//반복문 사용안한 코드
	//ChangeMain cMain = new ChangeMain();
	//cMain.calc(num1, num2);
}
{% endhighlight %}


Design.IChange interface(계산 메소드를 설계한 인터페이스) :
{% highlight java linenos %}
package Design;
/**
* 인터페이스를 설계하는 방법
* 접근제한자 + interface + 이름
*
* 설계된데로 구현하도록 강제화하는 방법
*
* 인터페이스에 맞는 메소드별로 모아서 생성할것
*
* @author daeho
*
*/
public interface IChange {
	public void calc(int pay, int buy);
}
{% endhighlight %}


Design.IChangePrint interface(출력 메소드를 설계한 인터페이스) :
{% highlight java linenos %}
package Design;

public interface IChangePrint {
		public void print(String flag, int count);
}
{% endhighlight %}


Change class(IChange, IChangePrint를 구현한 잔돈계산 class) :
{% highlight java linenos %}
/**
 * 인터페이스를 구현하기
 * class + 클래스명 + implements + 인터페이스명
 * @author daeho
 *
 */
public class Change implements Design.IChange, Design.IChangePrint {
	int[] changeArray = {5000, 1000, 500, 100, 50, 10};

	/**
	 * 거스름돈 계산
	 * ---------반복---------------------
	 * 잔돈계산
	 * 잔돈을 현재 거스름돈으로 나눈후 나머지 저장
	 * ---------------------------------
	 * @param pay
	 * @param buy
	 */
	@Override
	public void calc(int pay, int buy){
		int result = pay - buy;

		//System.out.printf("총거스름돈 : %,d원%n", result);
		print("총거스름돈", result);

		for(int change : changeArray){
			//System.out.printf("%d원 : %d개%n", change, result / change);
			print(change + "", result / change);
			result %= change;
		}
	}

	@Override
	public void print(String flag, int count){
		System.out.printf("%d원 : %d개%n", flag, count);
	}
}
{% endhighlight %}