# Chapter 02. 변수와 타입2



## 02-3. 타입 변환



##### <핵심 키워드>

`자동 타입 변환`, `강제 타입 변환`, `문자열 결합 연산`, `Integer.parseInt()`, `Double.parseDouble()` 



### 02-3-1. 자동 타입 변환

###### 자동 타입 변환(promotion)

자동으로 타입이 변환되는 것  

값의 허용 범위가 작은 타입이 허용 범위가 큰 타입으로 저장될 때 발생 

- 기본 타입의 허용 범위 크기순 정리

byte < short < int < long < float < double

*단, byte 타입은 char 타입으로 자동 타입 변환될 수 없음 (char 타입의 허용 범위는 음수를 포함하지 않기 때문)* 



### 02-3-2. 강제 타입 변환

###### 강제 타입 변환(casting)

강제로 타입을 변환하는 것   

값의 허용 범위가 큰 타입을 허용 범위가 작은 타입으로 쪼개어서 저장하는 것   

캐스팅 연산자 `괄호()` 를 사용함

*실수 타입을 정수 타입으로 강제 타입 변환할 경우 소수점 이하 부분은 버려지고 정수 부분만 저장됨*

```java
int intValue = 65;
char charValue = (char) intValue;
System.out.println(charValue); // "A"가 출력

double doubleValue = 3.14;
int intValue2 = (int) doubleValue;
System.out.println(intValue2); // 3이 출력
```



### 02-3-3. 정수 연산에서의 자동 타입 변환

정수 타입 변수가 산술 연산식에서 피연산자로 사용되면 int 타입보다 작은 byte, short, char 타입의 변수는 int 타입으로 자동 타입 변환되어 연산을 수행함  

단, 정수 연산식에서 모든 변수가 int 타입으로 변환되는 것은 아니며 두 피연산자 중 허용 범위가 큰 타입으로 변환되어 연산을 수행함  



### 02-3-4. 실수 연산에서의 자동 타입 변환

실수 타입 변수가 산술 연산식에서 피연산자로 사용될 경우 피연산자 중 하나가 double 타입이면 다른 피연산자도 double 타입으로 자동 타입 변환되어 연산을 수행하며 연산 결과는 double 타입이 됨  



정수 연산의 결과는 정수가 됨

```java
int x = 1;
int y = 2;
double result = x / y;
System.out.println(result); // 0.0이 출력
```

연산 결과로 0.5를 출력하고 싶다면 정수 변수 x나 y 중 하나를 실수 타입으로 변환한 후 연산을 수행해야 함  

```java
int x2 = 1;
int y2 = 2;
double result2 = (double) x2 / y2;
System.out.println(result2); // 0.5가 출력

int x2 = 1;
int y2 = 2;
double result2 = x2 / (double) y2;
System.out.println(result2); // 0.5가 출력

int x2 = 1;
int y2 = 2;
double result2 = (double) x2 / (double) y2;
System.out.println(result2); // 0.5가 출력
```



### 02-3-5. + 연산에서의 문자열 자동 타입 변환

###### 문자열 결합 연산

문자열과 + 연산을 하면 다른 피연산자도 문자열로 변환되어 문자열 결합이 일어남  

연산식에서 + 연산자가 연이어 나오면 앞에서부터 순차적으로 + 연산을 수행함  

만약 먼저 수행된 연산이 결합 연산이라면 이후 + 연산은 모두 결합 연산이 됨  

*우선 연산하고 싶은 부분이 있다면 해당 부분을 괄호()로 감싸줌*



```java
String str = "3" + 7;
String str2 = 3 + "7";

System.out.println(str); // "37"이 출력
System.out.println(str2); // "37"이 출력
```



### 02-3-6. 문자열을 기본 타입으로 강제 타입 변환

- 문자열을 기본 타입으로 변환하기

Byte.parseByte()

Short.parseShort()

Integer.parseInt()

Long.parseLong()

Float.parseFloat()

Double.parseDouble()

Boolean.parseBoolean()



- 기본 타입을 문자열로 변환하기

String.valueOf()







## 02-4. 변수와 시스템 입출력



##### <핵심 키워드>

`System.out.println()`, `System.out.print()`, `System.out.printf()`, `System.in.read()`, `Scanner`



### 02-4-1. 모니터로 변수값 출력하기

###### System.out

시스템의 표준 출력 장치



- System.out의 메소드

| 메소드                              | 의미                                              |
| ----------------------------------- | ------------------------------------------------- |
| println(내용);                      | 괄호 안의 내용을 출력하고 행을 바꾸기             |
| print(내용);                        | 괄호 안의 내용을 출력만 하기                      |
| printf("형식문자열", 값1, 값2, ...) | 괄호 안의 첫 번째 문자열 형식대로 내용을 출력하기 |



- printf("형식문자열", 값1, 값2, ...)의 형식문자열 나열 순서  

  : **%** [argument_index$] [flags] [width] [.precision] **conversion**  

  - **%**
  - [argument_index$] : 값의 순번
  - [flags] : 빈자리 채우는 방법
    - 생략 시 왼쪽이 공백으로 채워짐
    - \- : 오른쪽이 공백으로 채워짐
    - 0 : 공백 대신 0으로 채워짐
  - [width] : 전체 자릿수
  - [.precision] : 소수 자릿수
  - **conversion : 변환 문자**
    - d(정수)
    - f(실수)
    - s(문자열)



```java
int value = 123;
System.out.printf("상품의 가격:%d원\n", value); // 상품의 가격:123원
System.out.printf("상품의 가격:%6d원\n", value); // 상품의 가격:   123원
System.out.printf("상품의 가격:%-6d원\n", value); // 상품의 가격:123   원
System.out.printf("상품의 가격:%06d원\n", value); // 상품의 가격:000123원

double area = 3.14159 * 10 * 10;
System.out.printf("반지름이 %d인 원의 넓이:%10.2f\n", 10, area); // 반지름이 10인 원의 넓이:    314.16

String name = "홍길동";
String job = "도적";
System.out.printf("%6d|%-10s|%10s\n", 1, name, job); //      1|홍길동       |        도적

```



### 2-4-2. 키보드에서 입력된 내용을 변수에 저장하기

###### System.in

시스템의 표준 입력 장치  



- System.in.read();  

키보드로 입력한 키코드를 읽는 메소드  

System.in.read()가 실행되면 이클립스의 Console 뷰는 `Enter` 키가 입력될 때까지 대기 상태가 되며, `Enter` 키가 입력되면 System.in.read()는 입력된 키들에 대한 키코드를 하나씩 읽음  



```java
package sec04.exam04;

public class QStopExample {

	public static void main(String[] args) throws Exception{
		int keyCode;
		
		while(true) {
			keyCode = System.in.read();
			System.out.println("keyCode : " + keyCode);
			if(keyCode == 113) {
				break; // keyCode가 113(q 입력)일 경우 while문을 중지함  
			} // end of if
		} // end of while

	} // end of main

} // end of class 
```



System.in.read()는 키코드를 하나씩 읽기 때문에 2개 이상의 키가 조합된 한글을 읽을 수 없고, 키보드로부터 입력된 내용을 통 문자열로 읽지 못함  

이러한 단점을 보완하기 위해 자바는 Scanner 클래스를 제공함  

scanner.nextLine() 메소드는 `Enter` 키가 입력되기 전까지 대기 상태가 되며, `Enter` 키가 입력되면 입력된 모든 내용을 문자열로 읽음  



키보드에 입력된 내용을 문자열로 읽고 출력하는 예제

```java
package sec04.exam05;

import java.util.Scanner;

public class ScannerExample {

	public static void main(String[] args) throws Exception{
		Scanner scanner = new Scanner(System.in);
		String inputData;
		
		while(true) {
			inputData = scanner.nextLine();
			System.out.println("입력된 문자열 : \"" + inputData + "\"");
			if (inputData.equals("q")) {
				break; 
			} // end of if 
		} // end of while 
		
		System.out.println("종료");

	} // end of main 

} // end of class 
```

*String(문자열)의 값이 동일한지 비교할 때 equals() 메소드를 사용함* 





