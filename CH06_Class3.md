# Chapter 06. 클래스3



## 06-5. 인스턴스 멤버와 정적 멤버



##### <핵심 키워드>

`인스턴스 멤버`, `this`, `정적 멤버`, `static`, `싱글톤`, `final 필드`, `상수`     



### 06-5-1. 인스턴스 멤버와 this

###### 인스턴스 멤버(instance member)

객체마다 가지고 있는 멤버  

객체(인스턴스)를 생성한 후 사용할 수 있는 필드와 메소드를 말하며, 이들을 각각 인스턴스 필드, 인스턴스 메소드라고 부름

- 인스턴스 필드 : 힙 영역의 객체마다 가지고 있는 멤버, 객체마다 다른 데이터를 저장
- 인스턴스 메소드 : 객체가 있어야 호출 가능한 메소드, 클래스 코드(메소드 영역)에 위치하지만 이해가기 쉽도록 객체마다 가지고 있는 메소드라고 생각해도 됨  



#### 인스턴스 멤버 선언

(예시) Car 클래스에 인스턴스 필드 gas와 인스턴스 메소드 setSpeed()를 선언

```java
public class Car {
  // 인스턴스 필드
  int gas;
  
  // 인스턴스 메소드
  void setSpeed(int speed) {
    ...
  }
}
```

gas 필드와 setSpeed() 메소드는 인스턴스 멤버이기 때문에 외부 클래스에서 사용하기 위해서는 우선 Car 객체(인스턴스)를 생성하고 참조 변수 myCar 또는 yourCar로 접근해야 함

```java
Car myCar = new Car();
myCar.gas = 10;
myCar.setSpeed(60);

Car yourCar = new Car();
yourCar.gas = 20;
yourCar.setSpeed(80);
```

위 코드 실행 후 메모리 상태를 보면 인스턴스 필드 gas는 객체마다 따로 존재하고, 인스턴스 메소드 setSpeed()는 메소드 영역에 저장되고 공유됨  



#### this

객체 내부에서 인스턴스 멤버에 접근하기 위해 this를 사용함  

객체는 자신을 가리킬 때  `this` 라고 함  

this는 주로 생성자와 메소드의 매개 변수 이름이 필드와 동일한 경우, 인스턴스 멤버인 필드임을 명시하고자 할 때 사용됨  



(예시1) Car.java

```java
package sec05.exam01;

public class Car {
	// 인스턴스 필드
	String model;
	int speed;
	
	// 생성자 
	Car(String model) {
		this.model = model;
	}
	
	// 인스턴스 메소드
	void setSpeed(int speed) {
		this.speed = speed;
	}
	
	void run() {
		for(int i=0; i<=50; i+=10) {
			this.setSpeed(i);
			System.out.println(this.model + "가 달립니다. (시속 : " + this.speed + "km/h)");
		}
	}
}
```

(예시2) CarExample.java

```java
package sec05.exam01;

public class CarExample {

	public static void main(String[] args) {
		Car myCar = new Car("포르쉐");
		Car yourCar = new Car("벤츠");
		
		myCar.run();
		yourCar.run();
	}

}
```



### 06-5-2. 정적 멤버와 static

###### 정적 멤버(static member)

객체와 상관없는 멤버

클래스 코드(메소드 영역)에 위치  

클래스에 고정된 멤버로서 객체를 생성하지 않고 사용할 수 있는 필드와 메소드를 말하며, 이들을 각각 정적 필드, 정적 메소드라고 함  

- 정적 필드 및 상수 : 객체없이 클래스만으로도 사용 가능한 필드
- 정적 메소드 : 객체가 없이 클래스만으로도 호출 가능한 메소드  

*정적(static)의 의미 : '고정된'*



#### 정적 멤버 선언

정적 멤버를 선언하려면 `static` 키워드를 추가적으로 붙임

```java
public class 클래스 {
  // 정적 필드
  static 타입 필드 [= 초기값];
  
  // 정적 메소드
  static 리턴 타입 메소드(매개변수 선언, ...) {
    ...
  }
}
```

정적 멤버는 클래스에 고정된 멤버이므로 클래스 로더가 클래스(바이트 코드)를 로드해서 메소드 메모리 영역에 적재할 때 클래스별로 관리됨  

따라서 클래스의 로딩이 끝나면 바로 사용할 수 있음  



- 필드 선언 시 인스턴스 필드와 정적 필드 선택의 판단 기준
  - 객체마다 가지고 있어야 할 데이터라면 인스턴스 필드로 선언 
  - 객체마다 가지고 있을 필요가 없는 공용 데이터라면 정적 필드로 선언 

(예시)

```java
public class Calculator {
  // 인스턴스 필드
  String color; // 계산기별로 색깔이 다를 수 있음
  // 정적 필드
  static double pi = 3.14159; // 계산기에서 사용하는 파이값은 동일함 
}
```



- 메소드 선언 시 인스턴스 메소드와 정적 메소드 선택의 판단 기준
  - 인스턴스 필드나 인스턴스 메소드 또는 this를 포함하고 있다면 인스턴스 메소드로 선언
  - 인스턴스 필드를 포함하고 있지 않다면 정적 메소드로 선언

(예시)

```java
public class Calculator {
  // 인스턴스 필드
  Sting color;
  // 인스턴스 메소드
  void setColor(String color) {
    this.color = color;
  }
  // 정적 메소드
  static int plus(int x, int y) {
    return x+y;
  }
  static int minus(int x, int y) {
    return x-y;
  }
}
```



#### 정적 멤버 사용

정적 멤버는 클래스 이름과 함께 도트 연산자(`.`)로 접근

```java
클래스.필드;
클래스.메소드(매개값, ...);
```



(예시1) Calculator.java

```java
package sec05.exam02;

public class Calculator {
	static double pi = 3.14159;
	
	static int plus(int x, int y) {
		return x+y;
	}
	
	static int minus(int x, int y) {
		return x-y;
	}
}
```



(예시2) CalculatorExample.java

```java
package sec05.exam02;

public class CalculatorExample {

	public static void main(String[] args) {
		double result1 = 10 * 10 * Calculator.pi;
		int result2 = Calculator.plus(10, 5);
		int result3 = Calculator.minus(10, 5);
		
		System.out.println("result1 : " + result1);
		System.out.println("result2 : " + result2);
		System.out.println("result3 : " + result3);
	}

}
```



#### 정적 메소드 선언 시 주의할 점

객체가 없어도 실행된다는 특징 때문에 정적 메소드를 선언할 때에는 내부에 인스턴스 필드나 인스턴스 메소드를 사용할 수 없음  

정적 메소드에서 인스턴스 멤버를 사용하고 싶다면 객체를 먼저 생성하고 참조 변수로 접근해야 함 

main 메소드도 정적 메소드이므로 객체 생성 없이 인스턴스 필드와 인스턴스 메소드를 main() 메소드에서 바로 사용할 수 없음   

또한 객체 자신의 참조인 this 키워드도 사용이 불가능함  



(예시)

```java
package sec05.exam03;

public class Car {
	// 인스턴스 필드 
	int speed;
	
	// 인스턴스 메소드 
	void run() {
		System.out.println(speed + "으로 달립니다.");
	}
	
	public static void main(String[] args) {
		// 객체 생성 
		Car myCar = new Car();
		// myCar 참조 변수로 인스턴스 멤버에 접근 
		myCar.speed = 60;
		myCar.run();
	}
 }
```



### 06-5-3. 싱글톤

###### 싱글톤(Singleton)

전체 프로그램에서 단 하나의 객체만 만들도록 보장해야 하는 경우에 단 하나만 생성된다고 해서 이 객체를 싱글톤이라고 부름  



싱글톤을 만들려면 클래스 외부에서 new 연산자로 생성자를 호출할 수 없도록 생성자 앞에 `private` 접근 제한자를 붙여줌   

그리고 자신의 타입인 정적 필드를 하나 선언하고 자신의 객체를 생성해 초기화함(클래스 내부에서는 new 연산자로 생성자 호출이 가능함)  

정적 필드도 private 접근 제한자를 붙여 외부에서 필드값을 변경하지 못하도록 막음  

대신 외부에서 호출할 수 있는 정적 메소드인 getInstance()를 선언하고 정적 필드에서 참조하고 있는 자신의 객체를 리턴해줌  

```java
// 싱글톤 만들기
public class 클래스 {
  // 정적 필드
  private static 클래스 singleton = new 클래스();
  
  // 생성자
  private 클래스() {}
  
  // 정적 메소드
  static 클래스 getInstance() {
    return singleton;
  }
}
```



외부에서 객체를 얻는 유일한 방법은 getInstance() 메소드를 호출하는 것  

```java
클래스 변수1 = 클래스.getInstance();
클래스 변수2 = 클래스.getInstance();
```

위 코드에서 getInstance() 메소드는 단 하나의 객체만 리턴하므로 변수1과 변수2는 동일한 객체를 참조함  



(예시1) Singleton.java

```java
package sec05.exam04;

public class Singleton {
	private static Singleton singleton = new Singleton();
	
	private Singleton() {}
	
	static Singleton getInstance() {
		return singleton;
	}
}
```



(예시2) SingletonExample.java

```java
package sec05.exam04;

public class SingletonExample {

	public static void main(String[] args) {
		/* 컴파일 에러 
		Singleton s1 = new Singleton();
		Singleton s2 = new Singleton();
		*/
		
		Singleton obj1 = Singleton.getInstance();
		Singleton obj2 = Singleton.getInstance();
		
		if(obj1==obj2) {
			System.out.println("같은 Singleton 객체입니다.");
		} else {
			System.out.println("다른 Singleton 객체입니다.");
		}
	}

}
```



### 06-5-4. final 필드와 상수

#### final 필드

###### final 필드

초기값이 저장되면 이것이 최종적인 값이 되어서 프로그램 실행 도중에 수정할 수 없는 필드  



##### final 필드의 선언

`final 타입 필드 [= 초기값];`



##### final 필드에 초기값을 주는 방법 (2가지)

1. 필드 선언 시에 주는 방법

​		단순값일 경우 필드 선언 시에 주는 것이 제일 간단함  

2. 생성자에서 주는 방법

​		복잡한 초기화 코드가 필요하거나 객체 생성 시에 외부 데이터로 초기화해야 한다면 생성자에서 초기값을 지정해야 함  



(예시1) Person.java

```java
package sec05.exam05;

public class Person {
	// final 필드 
	final String nation = "Korea";
	final String ssn;
	// 인스턴스 필드
	String name;
	
	// 생성자
	public Person(String ssn, String name) {
		this.ssn = ssn;
		this.name = name;
	}
}
```

(예시2) PersonExample.java

```java
package sec05.exam05;

public class PersonExample {

	public static void main(String[] args) {
		Person p1 = new Person("123456-1234567", "홍길동");
		
		System.out.println(p1.nation);
		System.out.println(p1.ssn);
		System.out.println(p1.name);
		
		//p1.nation = "USA";
		//p1.ssn = "654321-7654321";
		p1.name = "홍길서";
	}

}
```



#### 상수

###### 상수(static final)

일반적으로 불변의 값을 상수라고 함  

(예) 원주율 파이, 지구의 무게 및 둘레 등  



###### 상수(constant)

자바에서 이런 불변의 값을 저장하는 필드를 상수라고 함  

상수는 static이면서 final이어야 함  

static final 필드는 객체마다 존재하지 않고 클래스에만 존재하며, 한 번 초기값이 저장되면 변경할 수 없음  

`static final 타입 상수 = 초기값;`

상수 이름은 관례적으로 모두 대문자로 작성하며, 만약 서로 다른 단어가 혼합된 경우 언더바(`_`)로 단어들을 연결해줌  



- 인스턴스 final과 정적(static) final 필드의 차이  

  - 인스턴스 final 필드 : 객체에 한번 초기화된 데이터를 변형 불가로 만들 경우 

    (예) final String ssn; (생성자에서 초기화)

  - 정적 final 필드 : 불변의 값인 상수를 만들 경우 

    (예) static final double PI = 3.14159;



(예시1) 상수 선언

```java
package sec05.exam06;

public class Earth {
	static final double EARTH_RADIUS = 6400;
	static final double EARTH_AREA = 4 * Math.PI * EARTH_RADIUS * EARTH_RADIUS;
}
```



(예시2) 상수 사용

```java
package sec05.exam06;

public class EarthExample {

	public static void main(String[] args) {
		System.out.println("지구의 반지름 : " + Earth.EARTH_RADIUS + "km");
		System.out.println("지구의 표면적 : " + Earth.EARTH_AREA + "km^2");
	}

}
```





