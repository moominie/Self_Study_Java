# Chapter 05. 참조 타입1



## 05-1. 참조 타입과 참조 변수



##### <핵심 키워드>

`기본 타입`, `참조 타입`, `메모리 사용 영역`, `번지 비교`, `null`, `NullPointerException`



### 05-1-1. 기본 타입과 참조 타입

###### 데이터 타입(data type)

자바의 데이터 타입은 크게 기본 타입과 참조 타입으로 분류됨  

#####  

###### 기본 타입(Primitive type)

1. 정수 타입 : byte, char, short, int, long
2. 실수 타입 : float, double
3. 논리 타입 : boolean



###### 참조 타입(Reference type)

객체(object)의 번지를 참조하는 타입  

1. 배열 타입
2. 열거 타입
3. 클래스
4. 인터페이스



### 05-1-2. 메모리 사용 영역

###### 메모리 영역(Runtime Data Area)

JVM은 운영체제에서 할당받은 메모리 영역을 메소드 영역, 힙 영역, JVM 스택 영역의 3가지 세부 영역으로 구분해서 사용함



###### 메소드 영역(Method Area)

JVM이 시작될 때 생성되고 모든 스레드가 공유하는 영역  

메소드 영역에는 코드에서 사용되는 클래스(~.class)들을 클래스 로더로 읽어 클래스별로 정적 필드(static field)와 상수(constant), 메소드 코드, 생성자(constructor) 코드 등을 분류해서 저장함  



###### 힙 영역(Heap Area)

힙 영역은 객체와 배열이 생성되는 영역  

힙 영역에 생성된 객체와 배열은 JVM 스택 영역의 변수나 다른 객체의 필드에서 참조함  

만약 참조하는 변수나 필드가 없다면 JVM이 이것을 쓰레기로 취급하고 쓰레기 수집기(Garbage Collector)를 실행시켜 자동으로 제거함  



###### JVM 스택 영역(JVM Stack Area)

JVM 스택은 메소드를 호출할 때마다 프레임(Frame)을 추가(push)하고 메소드가 종료되면 해당 프레임을 제거(pop)하는 동작을 수행함  

프레임 내부에는 로컬 변수 스택이 있는데, 기본 타입 변수와 참조 타입 변수가 추가(push)되거나 제거(pop)됨  



### 05-1-3. 참조 변수의 ==, != 연산

참조 타입 변수들 간의 ==, != 연산은 동일한 객체를 참조하는지 다른 객체를 참조하는지 알아볼 때 사용됨  

동일한 객체를 참조하고 있을 경우 == 연산의 결과는 true이고 != 연산의 결과는 false임  



### 05-1-4. null과 NullPointerException

###### null

참조 타입 변수는 힙 영역의 객체를 참조하지 않는다는 뜻으로 null(널) 값을 가질 수 있음



###### 예외(Exception)

자바 프로그램 실행 도중에 발생하는 오류



###### NullPointerException

참조 타입 변수를 잘못 사용하면 발생하는 예외  

참조 변수가 null을 가지고 있을 경우에는 참조 객체가 없으므로 변수를 통해 객체를 사용할 수 없음   

만약 null 상태에서 있지도 않은 객체의 데이터(필드)나 메소드를 사용하는 코드를 실행하면 NullPointerException이 발생하게 됨  

*해결 방법은 참조 변수를 추적해서 객체를 참조하도록 수정하는 것*  

(예시)

```java
int[] intArray = null;
intArray[0] = 10; // NullPointerException

String str = null;
System.out.println("총 문자수 : " + str.length()); // NullPointerException
```



### 05-1-5. String 타입

자바는 문자열을 String 타입에 저장함  

정확히 표현하면 문자열은 String 객체로 생성되고 변수는 String 객체를 참조함  

문자열 리터럴은 `큰따옴표("")`로 감싸서 작성함



자바는 문자열 리터럴이 동일하다면 String 객체를 공유하도록 되어 있음

(예시)

```java
String name1 = "신용권";
String name2 = "신용권";
```

위의 name1과 name2는 동일한 String 객체를 참조하게 됨  



###### new 연산자

new 연산자는 힙 영역에 새로운 객체를 만들 때 사용하는 연산자로 객체 생성 연산자라고 함   

```java
String name1 = new String("신용권");
String name2 = new String("신용권");
```

위의 name1과 name2는 서로 다른 String 객체를 참조하고 있음



###### equals() 메소드 (중요!)

내부 문자열을 비교할 때 String 객체의 equals() 메소드를 사용함  

원본 문자열과 매개값으로 주어진 비교 문자열이 동일한지 비교한 후 true 또는 false를 리턴함  



(예시)

```java
package sec01.exam01;

public class StringEqualsExample {

	public static void main(String[] args) {
		String strVar1 = "무미니";
		String strVar2 = "무미니";
		
		if (strVar1 == strVar2) {
			System.out.println("strVar1과 strVar2는 참조가 같음");
		} else {
			System.out.println("strVar1과 strVar2는 참조가 다름");
		} // strVar1과 strVar2는 참조가 같음
		
		if (strVar1.equals(strVar2)) {
			System.out.println("strVar1과 strVar2는 문자열이 같음");
		} // strVar1과 strVar2는 문자열이 같음
		
		String strVar3 = new String("무미니");
		String strVar4 = new String("무미니");
		
		if (strVar3 == strVar4) {
			System.out.println("strVar3과 strVar4는 참조가 같음");
		} else {
			System.out.println("strVar3과 strVar4는 참조가 다름");
		} // strVar3과 strVar4는 참조가 다름
		
		if (strVar3.equals(strVar4)) {
			System.out.println("strVar3과 strVar4는 문자열이 같음");
		} // strVar3과 strVar4는 문자열이 같음

	}

}
```





