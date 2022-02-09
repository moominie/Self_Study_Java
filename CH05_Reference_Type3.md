# Chapter 05. 참조 타입3



## 05-3. 열거 타입



##### <핵심 키워드>

`열거 타입`, `열거 타입 선언`, `열거 상수`, `열거 타입 변수`   



###### 열거 타입(enumeration type)

한정된 값인 열거 상수(enumeration constant) 중에서 하나의 상수를 저장하는 타입  



### 05-3-1. 열거 타입 선언

1. 먼저 열거 타입의 이름을 정하고 해당 이름으로 소스 파일(.java)을 생성함

​	열거 타입 이름은 관례적으로 첫 글자를 대문자로 하고 나머지는 소문자로 구성함  

​	만약 여러 단어로 구성된 이름이라면 각 단어의 첫 글자는 대문자로 하는 것이 관례

2. 소스 파일의 내용

   1. 열거 타입 선언

   `public enum 열거타입이름 {...}`

   2. 열거 상수 선언

   관례적으로 열거 상수는 모두 대문자로 작성함  

   만약 열거 상수가 여러 단어로 구성될 경우에는 단어 사이를 밑줄(_)로 연결함  



- 이클립스에서 열거 타입 생성하기

1. File - New - Enum
2. Package에는 열거 타입이 속할 패키지 이름을 입력하고, Name에는 열거 타입 이름을 입력한 후 Finish 클릭
3. 소스 코드에 열거 상수 작성하기

```java
package sec03.exam01;

public enum Week {
	MONDAY,
	TUESDAY,
	WEDNESDAY,
	THURSDAY,
	FRIDAY,
	SATURDAY,
	SUNDAY
}
```



### 05-3-2. 열거 타입 변수

열거 타입 변수를 선언하기

`열거타입 변수;`

(예시)

```java
Week today;
```



열거 타입 변수를 선언한 후에는 열거 상수를 저장할 수 있음  

열거 상수는 단독으로 사용할 수 없고 반드시 '열거타입.열거상수' 형태로 사용함  

`열거타입 변수 = 열거타입.열거상수;`

(예시)

```java
Week today = Week.SUNDAY;
```



*열거 타입도 참조 타입이기 때문에 열거 타입 변수에 null을 저장할 수 있음*  

(예시)

```java
Week birthday = null;
```



열거 상수는 열거 객체로 생성됨  

열거 타입 변수 Week의 경우 MONDAY부터 SUNDAY까지의 열거 상수는 총 7개의 Week 객체로 생성됨  

메소드 영역에 생성된 열거 상수가 해당 Week 객체를 각각 참조하게 됨



```java
Week today = Week.SUNDAY;
```

위 코드의 경우 열거 타입 변수 today는 스택 영역에 생성됨  

today에 저장되는 값은 Week.SUNDAY 열거 상수가 참조하는 객체의 번지임  

따라서 열거 상수 Week.SUNDAY와 today 변수는 서로 같은 Week 객체를 참조하게 됨  

```java
today == Week.SUNDAY; // true
```



###### Calendar 클래스

자바는 컴퓨터의 날짜, 요일, 시간을 얻기 위해 Calendar 클래스를 제공함  



Calendar 변수를 선언하고 getInstance() 메소드로 Calendar 객체를 얻기

```java
Calendar now = Calendar.getInstance();
```



Calendar 객체를 얻었으므로 get() 메소드를 이용해서 연, 월, 일, 요일, 시간, 분, 초를 다음과 같이 얻을 수 있음  

```java
int year = now.get(Calendar.YEAR); // 연
int month = now.get(Calendar.MONTH) + 1; // 월
int day = now.get(Calendar.DAY_OF_MONTH); // 일
int week = now.get(Calendar.DAY_OF_WEEK); // 요일(1~7)
int hour = now.get(Calendar.HOUR); // 시간
int minute = now.get(Calendar.MINUTE); // 분
int second = now.get(Calendar.SECOND); // 초
```



(예시) Calendar를 이용해서 오늘의 요일을 얻고 나서, Week 열거 타입 변수 today에 해당 열거 상수를 대입하기

```java
package sec03.exam02;

import java.util.Calendar;

import sec03.exam01.Week;

public class EnumWeekExample {

	public static void main(String[] args) {
		Week today = null; // 열거 타입 변수 선언
		
		Calendar cal = Calendar.getInstance();
		int week = cal.get(Calendar.DAY_OF_WEEK); // 일(1) ~ 토(7)까지의 숫자를 리턴 
		
		switch (week) {
		case 1:
			today = Week.SUNDAY; // 열거 상수 대입 
			break;
		case 2:
			today = Week.MONDAY;
			break;
		case 3:
			today = Week.TUESDAY;
			break;
		case 4:
			today = Week.WEDNESDAY;
			break;
		case 5:
			today = Week.THURSDAY;
			break;
		case 6:
			today = Week.SATURDAY;
			break;
		}
		
		System.out.println("오늘 요일 : " + today);
		
		if (today==Week.SUNDAY) {
			System.out.println("일요일에는 축구를 합니다.");
		} else {
			System.out.println("열심히 자바 공부를 합니다.");
		}
	}

}
```





