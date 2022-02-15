# Chapter 06. 클래스2



## 06-2. 필드



##### <핵심 키워드>

`필드 선언`, `필드 사용`      



###### 필드(field)

객체의 고유 데이터, 객체가 가져야 할 부품, 객체의 현재 상태 데이터를 저장하는 곳  

(예시) 자동차 객체

- 고유 데이터 : 제작회사, 모델, 색깔, 최고 속도
- 상태 데이터 : 현재 속도, 엔진 회전 수
- 부품 : 차체, 엔진, 타이어

자동차 클래스를 생성할 때 이 정보들은 필드로 선언되어야 함  



### 06-2-1. 필드 선언

필드 선언은 클래스 중괄호{} 블록 어디서든 존재할 수 있음  

단, 생성자와 메소드 중괄호 {} 블록 내부에는 선언될 수 없으며, 이 곳에 선언된 것은 모두 로컬 변수가 됨  



- 필드 선언 형태

```java
타입 필드; // 필드의 초기값이 주어지지 않은 경우
타입 필드 = 초기값; // 필드의 초기값이 주어진 경우 
```



초기값이 지정되지 않은 필드는 객체 생성 시 자동으로 기본 초기값으로 설정됨  

- 필드 타입별 기본 초기값

| 분류      |                     | 타입    | 초기값           |
| --------- | ------------------- | ------- | ---------------- |
| 기본 타입 | 정수 타입           | byte    | 0                |
|           |                     | char    | \u0000 (빈 공백) |
|           |                     | short   | 0                |
|           |                     | int     | 0                |
|           |                     | long    | 0L               |
|           | 실수 타입           | float   | 0.0F             |
|           |                     | double  | 0.0              |
|           | 논리 타입           | boolean | false            |
| 참조 타입 | 배열                |         | null             |
|           | 클래스(String 포함) |         | null             |
|           | 인터페이스          |         | null             |



### 06-2-2. 필드 사용

필드를 사용한다는 것은 필드값을 읽고 변경하는 작업을 말함  

클래스 내부의 생성자나 메소드에서 사용할 경우 단순히 필드 이름으로 읽고 변경함  

클래스 외부에서 사용할 경우 우선적으로 클래스로부터 객체를 생성한 뒤 필드를 사용해야 함  

필드가 객체에 소속된 데이터이므로 객체가 존재하지 않으면 필드도 존재하지 않기 때문   



###### 도트(.) 연산자

객체 접근 연산자  

객체가 가지고 있는 필드나 메소드를 사용하고자 할 때 사용됨  



(예시1) Car 클래스 필드 선언

```java
package sec02.exam01;

public class Car {
	// 필드 선언 
	String company = "현대자동차";
	String model = "제네시스GV80";
	String color = "검정";
	int maxSpeed = 350;
	int speed;
}
```



(예시2) 외부 클래스에서 Car 필드값 읽기와 변경  

```java
package sec02.exam01;

public class CarExample {

	public static void main(String[] args) {
		// 객체 생성 
		Car myCar = new Car();
		
		// 필드값 읽기 
		System.out.println("제작 회사 : " + myCar.company);
		System.out.println("모델명 : " + myCar.model);
		System.out.println("색깔 : " + myCar.color);
		System.out.println("최고 속도 : " + myCar.maxSpeed);
		System.out.println("현재 속도 : " + myCar.speed);
		
		// 필드값 변경 
		myCar.speed = 60;
		System.out.println("수정된 속도 : " + myCar.speed);

	}

}
```



## 06-3. 생성자



##### <핵심 키워드>

`기본 생성자`, `생성자 선언`, `매개 변수`, `객체 초기화`, `this()`, `오버로딩`



###### 생성자(Constructor)

new 연산자로 클래스로부터 객체를 생성할 때 호출되어 객체의 초기화를 담당함  



###### 객체 초기화

필드를 초기화하거나 메소드를 호출해서 객체를 사용할 준비를 하는 것  



생성자를 실행하지 않고는 클래스로부터 객체를 만들 수 없음  

new 연산자에 의해 생성자가 성공적으로 실행되면 힙(heap) 영역에 객체가 생성되고 객체의 번지가 리턴됨  

리턴된 객체의 번지는 스택 영역에 생성된 클래스 변수에 저장됨  



### 06-3-1. 기본 생성자(Default Constructor)

모든 클래스는 생성자가 반드시 존재하며, 생성자를 하나 이상 가질 수 있음  

클래스 내부에 생성자 선언을 생략하면 컴파일러는 중괄호 {} 블록 내용이 비어 있는 기본 생성자를 바이트 코드에 자동 추가함  

`[public] 클래스() {}`

(예시1) 소스 파일(Car.java)

```java
public class Car {
  
}
```

(예시2) 바이트 코드 파일(Car.class)

```java
public class Car {
  public Car() {} // 기본 생성자가 자동 추가됨 
}
```



그렇기 때문에 클래스에 생성자를 추가하지 않아도 new 연산자 뒤에 기본 생성자를 호출해서 객체를 생성할 수 있었음

(예시) `Car myCar = new Car();`

Car() : 기본 생성자



그러나 클래스에 명시적으로 선언한 생성자가 1개라도 있으면 컴파일러는 기본 생성자를 추가하지 않음  

명시적으로 생성자를 선언하는 이유는 객체를 다양한 값으로 초기화하기 위함 

 

### 06-3-2. 생성자 선언

생성자를 명시적으로 선언하는 방법   

```java
클래스(매개변수 선언, ...) {
  // 객체의 초기화 코드
}
```

생성자 블록 내부에는 객체 초기화 코드가 작성되는데, 일반적으로 필드에 초기값을 저장하거나 메소드를 호출하여 객체 사용 전에 필요한 준비를 함  

매개변수 선언은 생략할 수도 있고 여러 개를 선언할 수도 있음  

매개변수는 new 연산자로 생성자를 호출할 때 외부의 값을 생성자 블록 내부로 전달하는 역할을 함  



클래스에 생성자가 명시적으로 선언되어 있을 경우 반드시 선언된 생성자를 호출해서 객체를 생성해야 함  



(예시1) 생성자 선언

```java
package sec03.exam01;

public class Car {
	// 생성자 
	public Car(String color, int cc) {
	}

}
```

(예시2) 생성자를 호출해서 객체 생성

```java
package sec03.exam01;

public class CarExample {

	public static void main(String[] args) {
		Car myCar = new Car("검정", 3000);
	}

}
```



### 06-3-3. 필드 초기화

클래스로부터 객체가 생성될 때 필드는 기본 초기값으로 자동 설정됨  



필드를 다른 값으로 초기화하는 방법

1. 필드를 선언할 때 초기값을 주는 방법  

   이 경우 동일 클래스로부터 생성되는 객체들은 모두 같은 값을 갖게 됨(객체 생성 후 초기값을 변경할 수 있음)  

2. 생성자에서 초기값을 주는 방법  

   객체 생성 시점에 외부에서 제공되는 다양한 값들로 초기화되어야 한다면 생성자에서 초기화해야 함 

   생성자의 매개값으로 이 값들을 받아 초기화함 



(예시1) 생성자에서 필드 초기화 

```java
package sec03.exam02;

public class Korean {
	// 필드 
	String nation = "대한민국";
	String name;
	String ssn;
	
	// 생성자
	public Korean(String n, String s) {
		name = n;
		ssn = s;
	}

}
```

(예시2) 객체 생성 후 필드값 출력

```java
package sec03.exam02;

public class KoreanExample {

	public static void main(String[] args) {
		Korean k1 = new Korean("김자바", "123456-7777777");
		System.out.println("k1.nation : " + k1.nation);
		System.out.println("k1.name : " + k1.name);
		System.out.println("k1.ssn : " + k1.ssn);
		
		Korean k2 = new Korean("박자바", "987654-7777777");
		System.out.println("k2.nation : " + k2.nation);
		System.out.println("k2.name : " + k2.name);
		System.out.println("k2.ssn : " + k2.ssn);

	}

}
```

일반적으로 필드와 동일한 이름을 갖는 매개 변수를 사용함  

필드와 매개 변수 이름이 동일할 때, 동일한 이름의 매개 변수가 사용 우선순위가 높기 때문에 생성자 내부에서 해당 필드에 접근할 수 없음  

해결 방법 : 필드 앞에 `this.` 붙이기  



###### this

객체 자신의 참조  

`this.필드` 는 this라는 참조 변수로 필드를 사용하는 것과 동일함  



(예시)

```java
package sec03.exam02;

public class Korean {
	// 필드 
	String nation = "대한민국";
	String name;
	String ssn;
	
	// 생성자
	public Korean(String name, String ssn) {
		this.name = name;
		this.ssn = sssn;
	}

}
```



### 06-3-4. 생성자 오버로딩

###### 생성자 오버로딩(overloading)

매개 변수를 달리하는 생성자를 여러 개 선언하는 것  

```java
public class 클래스 {
  클래스 ([타입 매개변수, ...]) {
    
  }
  
  클래스 ([타입 매개변수, ...]) {
    
  }
}
```

*생성자의 오버로딩 : 매개 변수의 타입, 개수, 순서를 다르게 선언한다.*

생성자가 오버로딩되어 있을 경우, new 연산자로 생성자를 호출할 때 제공되는 매개값의 타입과 수에 의해 호출될 생성자가 결정됨 



(예시1) 생성자의 오버로딩

```java
package sec03.exam03;

public class Car {
	// 필드 
	String company = "현대자동차";
	String model;
	String color;
	int maxSpeed;
	
	// 생성자1 - 기본 생성자 
	Car() {
		
	}
	
	// 생성자2
	Car(String model) {
		this.model = model;
	}
	
	// 생성자3
	Car(String model, String color) {
		this.model = model;
		this.color = color;
	}
	
	// 생성자4
	Car(String model, String color, int maxSpeed) {
		this.model = model;
		this.color = color;
		this.maxSpeed = maxSpeed;
	}

}
```

 (예시2) 객체 생성 시 생성자 선택

```java
package sec03.exam03;

public class CarExample {

	public static void main(String[] args) {
		Car car1 = new Car(); // 생성자1 선택 
		System.out.println("car1.company : " + car1.company);
		System.out.println();
		
		Car car2 = new Car("제네시스GV80"); // 생성자2 선택 
		System.out.println("car2.company : " + car2.company);
		System.out.println("car2.model : " + car2.model);
		System.out.println();
		
		Car car3 = new Car("제네시스GV80", "흰색"); // 생성자3 선택 
		System.out.println("car3.company : " + car3.company);
		System.out.println("car3.model : " + car3.model);
		System.out.println("car3.color : " + car3.color);
		System.out.println();
		
		Car car4 = new Car("제네시스GV80", "흰색", 200); // 생성자4 선택 
		System.out.println("car4.company : " + car4.company);
		System.out.println("car4.model : " + car4.model);
		System.out.println("car4.color : " + car4.color);
		System.out.println("car4.maxSpeed : " + car4.maxSpeed);
		System.out.println();
		
	}

}
```



### 06-3-5. 다른 생성자 호출: this()

필드 초기화 내용은 한 생성자에만 집중적으로 작성하고 나머지 생성자는 초기화 내용을 가지고 있는 생성자를 호출하면 생성자 간의 중복 코드 발생을 줄일 수 있음  

생성자에서 다른 생성자를 호출할 때에는 다음과 같이 this() 코드를 사용함  

```java
클래스([타입 매개변수, ...]) {
  this([타입 매개변수, ..., 값]); // 클래스의 다른 생성자 호출
}
```

 

###### this()

자신의 다른 생성자를 호출하는 코드  

반드시 생성자의 첫 줄에서만 허용됨  

(예시1) 다른 생성자를 호출해서 중복 코드 줄이기

```java
package sec03.exam04;

public class Car {
	// 필드
	String company = "현대자동차";
	String model;
	String color;
	int maxSpeed;
	
	// 생성자 
	Car() {
	}
	
	Car(String model) {
		this(model, "흰색", 200);
	}
	
	Car(String model, String color) {
		this(model, color, 200);
	}
	
	Car(String model, String color, int maxSpeed) {
		this.model = model;
		this.color = color;
		this.maxSpeed = maxSpeed;
	}

}
```

 (예시2) 객체 생성 시 생성자 선택

```java
package sec03.exam04;

public class CarExample {

	public static void main(String[] args) {
		Car car1 = new Car(); // 생성자1 선택 
		System.out.println("car1.company : " + car1.company);
		System.out.println();
		
		Car car2 = new Car("제네시스GV80"); // 생성자2 선택 
		System.out.println("car2.company : " + car2.company);
		System.out.println("car2.model : " + car2.model);
		System.out.println();
		
		Car car3 = new Car("제네시스GV80", "흰색"); // 생성자3 선택 
		System.out.println("car3.company : " + car3.company);
		System.out.println("car3.model : " + car3.model);
		System.out.println("car3.color : " + car3.color);
		System.out.println();
		
		Car car4 = new Car("제네시스GV80", "흰색", 200); // 생성자4 선택 
		System.out.println("car4.company : " + car4.company);
		System.out.println("car4.model : " + car4.model);
		System.out.println("car4.color : " + car4.color);
		System.out.println("car4.maxSpeed : " + car4.maxSpeed);
		System.out.println();
		
	}

}
```



## 06-4. 메소드



##### <핵심 키워드>

`선언부`, `void`, `매개 변수`, `리턴문`, `호출`, `오버로딩`



###### 메소드(method)

객체의 동작에 해당하는 중괄호{} 블록  



###### 메소드 시그니처(signature)

메소드 선언부  

리턴 타입, 메소드 이름, 매개 변수 선언으로 구성되며 메소드 선언부 다음에 메소드 실행 블록이 옴  



### 06-4-1. 메소드 선언

메소드 선언은 선언부(리턴 타입, 메소드 이름, 매개 변수 선언)와 실행 블록으로 구성됨  



#### 리턴 타입

리턴 타입은 리턴값(메소드를 실행한 후의 결과값)의 타입을 말함  



##### 메소드의 리턴값이 있는 경우

선언부에 리턴 타입을 명시해야 함  

메소드 호출 시 리턴값을 받기 위한 변수의 타입을 메소드의 리턴 타입과 동일하게 선언함  

단, 반드시 리턴값을 변수에 저장할 필요가 없을 때에는 변수를 선언하지 않고 메소드를 호출할 수도 있음  



##### 메소드의 리턴값이 없는 경우

리턴값이 없는 메소드는 리턴 타입에 void로 기술함  



(예시) 전자계산기 객체

- powerOn() 메소드

  전원을 켜고 끄는 기능 실행, 리턴값 없음

- divide() 메소드

  나누는 기능, 리턴값은 두 수를 나눈 결과

```java
void powerOn() { ... }
double divide(int x, int y) { ... }
```



#### 메소드 이름

메소드 이름은 자바 식별자 규칙에 맞게 작성함  

관례적으로 메소드 이름은 소문자로 작성함  



#### 매개 변수 선언

매개 변수는 메소드가 실행할 때 필요한 데이터를 외부로부터 받기 위해 사용함  

메소드 호출 시 넘겨준 매개값은 각각 해당 위치의 매개 변수에 저장되고, 이 매개 변수들을 이용해서 메소드 블록을 실행하게 됨  

이때, 매개값은 반드시 매개 변수의 타입에 부합되는 값이어야 함  



(예시)

```java
// 메소드 선언
double divide(int x, int y) { ... }

// 메소드 호출
double result = divide(10, 20);

// 매개 변수 타입으로 변환될 수 있는 매개값은 사용 가능
byte b1 = 10;
byte b2 = 20;
double result = divide(b1, b2);
```



(예시1) Calculator 클래스에서 메소드 선언

```java
package sec04.exam01;

public class Calculator {
	// 메소드 
	void powerOn() {
		System.out.println("전원을 켭니다.");
	}
	
	int plus(int x, int y) {
		int result = x + y;
		return result;
	}
	
	int minus(int x, int y) {
		int result = x - y;
		return result;
	}
	
	double divide(int x, int y) {
		double result = (double) x / y;
		return result;
	}
	
	double multiply(int x, int y) {
		double result = (double) x * y;
		return result;
	}
	
	void powerOff() {
		System.out.println("전원을 끕니다.");
	}
}
```



(예시2) 외부 클래스에서 메소드 호출

```java
package sec04.exam01;

public class CalculatorExample {

	public static void main(String[] args) {
		Calculator myCalc = new Calculator();
		
		myCalc.powerOn();
		
		int result1 = myCalc.plus(5, 6);
		System.out.println("5 + 6 = " + result1);
		
		int result2 = myCalc.minus(10, 3);
		System.out.println("10 - 3 = " + result2);
		
		byte x = 10;
		byte y = 4;
		double result3 = myCalc.divide(x, y);
		System.out.println("10 / 4 = " + result3);
		
		int a = 10;
		int b = 2;
		double result4 = myCalc.multiply(a, b);
		System.out.println("10 * 2 = " + result4);
		
		myCalc.powerOff();
	}

}
```



#### 매개 변수의 개수를 모를 경우

메소드를 선언할 때 매개 변수의 개수를 알 수 없는 경우의 해결 방법  

1. 매개 변수를 배열 타입으로 선언하기

```java
// 메소드 선언
int sum1(int[] values) { }

// 메소드 호출
int[] values = {1, 2, 3};
int result = sum1(values);

int result = sum1(new int[] {1, 2, 3});
```



2. 매개 변수를 ... 을 이용해서 선언하기

메소드 호출 시 배열을 생성하지 않고 값의 목록만 넘겨주는데, 이때 넘겨준 값의 수에 따라 자동으로 배열이 생성되고 매개값으로 사용됨  

...으로 선언된 매개 변수의 값은 메소드 호출 시 쉼표로 나열해주거나 배열을 직접 매개값으로 사용할 수 있음  

```java
// 메소드 선언
int sum2(int ... values) { }

// 메소드 호출
int result = sum2(1, 2, 3, 4, 5);

int[] values = {1, 2, 3, 4, 5};
int result = sum2(values);

int result = sum2(new int[] {1, 2, 3, 4, 5});
```



(예시1) 매개 변수의 개수를 모르는 경우 

```java
package sec04.exam02;

public class Computer {
	// 메소드 
	int sum1(int[] values) {
		int sum = 0;
		for(int i=0; i<values.length; i++) {
			sum += values[i];
		}
		return sum;
	}
	
	int sum2(int ... values) {
		int sum = 0;
		for(int i=0; i<values.length; i++) {
			sum += values[i];
		}
		return sum;
	}
}
```

```java
package sec04.exam02;

public class ComputerExample {

	public static void main(String[] args) {
		// 객체 생성 
		Computer myCom = new Computer();
		
		// 메소드 호출
		int[] values = {1, 2, 3};
		int result1 = myCom.sum1(values);
		System.out.println("result1 : " + result1);
		
		int result2 = myCom.sum1(new int[] {1, 2, 3, 4, 5});
		System.out.println("result2 : " + result2);
		
		int result3 = myCom.sum2(1, 2, 3);
		System.out.println("result3 : " + result3);
		
		int result4 = myCom.sum2(1, 2, 3, 4, 5);
		System.out.println("result4 : " + result4);
	}

}
```



### 06-4-2. 리턴(return)문

#### 리턴값이 있는 메소드

메소드 선언에 리턴 타입이 있는 메소드는 반드시 리턴문을 이용해서 리턴값을 지정해야 함  

`return 리턴값;`

리턴문의 리턴값은 리턴 타입이거나 리턴 타입으로 변환될 수 있어야 함  



(추가) 리턴문 이후의 실행문

리턴문 이후의 실행문이 오면 "Unreachable code"라는 컴파일 에러가 발생함  

```java
int plus(int x, int y) {
  int result = x + y;
  return result;
  System.out.println(result); // Unreachable code 에러 발생
}
```

하지만 다음의 경우에는 컴파일 에러가 발생하지 않음  

```java
boolean isLeftGas() {
  if (gas==0) {
    System.out.println("gas가 없습니다.");
    return false;
  }
  System.out.println("gas가 있습니다.");
  return true;
}
```



#### 리턴값이 없는 메소드 : void

리턴값이 없는 메소드는 리턴 타입으로  void를 사용함  

void로 선언된 메소드에서 return문을 사용하면 이것은 리턴값을 지정하는 것이 아니라 메소드 실행을 강제 종료시키는 역할을 함  

 `return;`



(예시) 리턴문 

```java
package sec04.exam03;

public class Car {
	// 필드 
	int gas;
	
	// 생성자
	
	// 메소드 
	void setGas(int gas) {
		this.gas = gas;
	} // 리턴값이 없는 메소드로 매개값을 받아서 gas 필드값을 변경 
	
	boolean isLeftGas() {
		if(gas == 0) {
			System.out.println("gas가 없습니다.");
			return false;
		}
		System.out.println("gas가 있습니다.");
		return true;
	} // 리턴값이 boolean인 메소드로 gas 필드값이 0이면 false를, 0이 아니면 true를 리턴 
	
	void run() {
		while(true) {
			if(gas>0) {
				System.out.println("달립니다. (gas 잔량 : " + gas + ")");
				gas--;
			} else {
				System.out.println("멈춥니다. (gas 잔량 : " + gas + ")");
				return; // run() 메소드 실행 종
			}
		}
	}
}
```

```java
package sec04.exam03;

public class CarExample {

	public static void main(String[] args) {
		Car myCar = new Car();
		
		myCar.setGas(5);
		
		boolean gasState = myCar.isLeftGas();
		if(gasState) {
			System.out.println("출발합니다.");
			myCar.run();
		}
		
		if(myCar.isLeftGas()) {
			System.out.println("gas를 주입할 필요가 없습니다.");
		} else {
			System.out.println("gas를 주입하세요.");
		}

	}

}
```



### 06-4-3. 메소드 호출

#### 객체 내부에서 호출

메소드가 매개 변수를 가지고 있을 때에는 매개 변수의 타입과 수에 맞게 매개값을 제공함  

`메소드(매개값, ...);`



리턴값이 있는 메소드를 호출하고 리턴값을 받고 싶다면 다음과 같이 변수를 선언하고 리턴값을 대입함  

`타입 변수  = 메소드(매개값, ...);`

이때 변수 타입은 메소드 리턴 타입과 동일하거나, 자동 타입 변환될 수 있어야 함  



(예시)

 ```java
 package sec04.exam04;
 
 public class Calculator {
 	int plus(int x, int y) {
 		int result = x + y;
 		return result;
 	}
 	
 	double avg(int x, int y) {
 		double sum = plus(x, y);
 		double result = sum / 2;
 		return result;
 	}
 	
 	void execute() {
 		double result = avg(10, 7);
 		System.out.println("실행 결과 : " + result);
 	}
 	
 	void println(String message) {
 		System.out.println(message);
 	}
 }
 ```

```java
package sec04.exam04;

public class CalculatorExample {

	public static void main(String[] args) {
		Calculator myCalc = new Calculator();
		myCalc.execute();
	}

} // 실행 결과 : 8.5
```



#### 객체 외부에서 호출

외부 클래스에서 메소드를 호출하려면 우선 클래스로부터 객체를 생성해야 함  

`클래스 참조변수  = new 클래스(매개값, ...);`



객체가 생성되고나면 참조 변수와 함께 도트(.) 연산자를 사용해서 메소드를 호출할 수 있음  

`참조변수.메소드(매개값, ...);` 

`타입 변수  = 참조변수.메소드(매개값, ...);`



(예시)

```java
package sec04.exam05;

public class Car {
	// 필드
	int speed;
	
	// 메소드
	int getSpeed() {
		return speed;
	}
	
	void keyTurnOn() {
		System.out.println("키를 돌립니다.");
	}
	
	void run() {
		for(int i=0; i<=50; i+=10) {
			speed = i;
			System.out.println("달립니다.(시속 : " + speed + "km/h)");
		}
	}

}
```

```java
package sec04.exam05;

public class CarExample {

	public static void main(String[] args) {
		Car myCar = new Car();
		myCar.keyTurnOn();
		myCar.run();
		int speed = myCar.getSpeed();
		System.out.println("현재 속도 : " + speed + "km/h");
	}

}
```



### 06-4-4. 메소드 오버로딩

클래스 내에 같은 이름의 메소드를 여러 개 선언하는 것을 메소드 오버로딩이라고 함 

메소드 오버로딩의 조건 : 매개 변수의 타입, 개수, 순서 중 하나가 달라야 함  

메소드 오버로딩이 필요한 이유 : 매개값을 다양하게 받아 처리할 수 있도록 하기 위해서  

오버로딩된 메소드를 호출할 경우 JVM은 매개값의 타입을 보고 메소드를 선택함  

매개 변수의 타입이 일치하지 않을 경우 JVM은 자동 타입 변환이 가능한지를 검사함  

메소드 오버로딩 시 주의할 점 : 매개 변수의 타입과 개수, 순서가 똑같을 경우 매개 변수의 이름이 다르다고 해서 이것을 메소드 오버로딩이라고 하지 않음, 리턴 타입만 다르고 매개 변수가 동일하다면 이것도 오버로딩이 아님  



(예시) 매개값의 개수에 따라 메소드를 다르게 호출하여 정사각형 혹은 직사각형의 넓이를 계산하여 리턴하는 메소드 오버로딩

```java
package sec04.exam06;

public class Calculator {
	// 정사각형의 넓이
	double areaRectangle(double width) {
		return width * width;
	}
	
	// 직사각형의 넓이
	double areaRectangle(double width, double height) {
		return width * height;
	}
}
```

```java
package sec04.exam06;

public class CalculatorExample {

	public static void main(String[] args) {
		Calculator myCalc = new Calculator();
		
		// 정사각형의 넓이 구하기
		double result1 = myCalc.areaRectangle(10);
		
		// 직사각형의 넓이 구하기
		double result2 = myCalc.areaRectangle(10, 20);
		
		// 결과 출력
		System.out.println("정사각형 넓이 : " + result1); // 정사각형 넓이 : 100.0
		System.out.println("직사각형 넓이 : " + result2);
	} // 직사각형 넓이 : 200.0

}
```





