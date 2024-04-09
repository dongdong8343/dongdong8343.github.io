---
title: "오버로딩, 오버라이딩"
excerpt: "오버로딩, 오버라이딩 정리"

categories:
  - Cs
tags:
  - [오버로딩, 오버라이딩]
sidebar:
  nav: "counts"
---

### 오버로딩

메서드의 매개변수의 순서, 개수, 타입을 다르게 해서 같은 이름으로 여러 개의 메서드를 만드는 것을 말한다.

저렇게하면 유연성이 높아지고 코드를 깔끔하게 만들 수 있다.

```java
class Calculator{
	// 매개변수의 개수, 타입이 달라서 입력되는 인수에 따라 호출되는 메서드가 달라짐.
	void multiply(int a, int b){
		System.out.println("결과는 : "+ (a * b) + "입니다.");
	}
	void multiply(int a, int b, int c){
		System.out.println("결과는 : "+ (a * b * c) + "입니다.");
	}
	void multiply(double a, double b){
		System.out.println("결과는 : "+ (a * b) + "입니다.");
	}
}
public class MyClass {
	public static void main(String args[]) {
	int a = 1;
	int b = 2;
	int d = 4;
	Calculator c = new Calculator();
	c.multiply(a, b);
	c.multiply(a, b, d);
	double aa = 1.2;
	double bb = 1.4;
	c.multiply(aa, bb);
	}
}

// 매개변수의 순서가 달라도 들어오는 인수에 따라 호출되는 메서드가 달라짐.
class Person{
	void pay(String a, int b){
		System.out.println(a + "가 "+ b + "원만큼 계산합니다. ");
	}
	void pay(int a, String b){
		System.out.println(b + "가 "+ a + "원만큼 계산합니다. ");
	}
}
public class MyClass {
	public static void main(String args[]) {
		Person c = new Person();
		c.pay("영주", 1000000000);
		c.pay(1000000000, "영주");
	}
}
```

### 오버라이딩

상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의 하는 것을 말한다.

상속 관계에서 사용되고 static, final이 붙은 메서드는 오버라이딩 불가능하다.

```java
class Animal{
	void eat(){
		System.out.println("먹습니다.");
	}
}
class Person extends Animal{
	@Override
	void eat(){
		System.out.println("사람처럼 먹습니다. ");
	}
}
public class MyClass {
	public static void main(String args[]) {
	Person a = new Person();
	a.eat();
	}
}

// 인터페이스로 틀만 만들고 이를 기반으로 여러 개의 하위 클래스를 만들 수도 있음.
interface Animal{
	public void eat();
}
class Person implements Animal{
	@Override
	public void eat(){
		System.out.println("사람처럼 먹습니다. ");
	}
}
public class MyClass {
	public static void main(String args[]) {
	Person a = new Person();
	a.eat();
	}
}
```
