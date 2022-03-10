# Chapter 07. 상속2



## 07-2. 타입 변환과 다형성



##### <핵심 키워드>

`다형성`, `클래스 타입 변환`, `자동 타입 변환`, `강제 타입 변환`, `instanceof`



###### 다형성

사용 방법은 동일하지만 다양한 객체를 이용해서 다양한 실행결과가 나오도록 하는 성질

예를 들어 자동차가 타이어를 사용하는 방법은 동일하지만 장착하는 타이어에 따라 주행 성능이 달라질 수 있음  

`메소드 재정의` + `타입 변환` -> `다형성`

다형성을 구현하려면 메소드 재정의와 타입 변환이 필요함  



### 07-2-1. 자동 타입 변환

###### 자동 타입 변환(promotion)

프로그램 실행 도중에 자동적으로 타입 변환이 일어나는 것  

클래스의 변환은 상속 관계에 있는 클래스 사이에서 발생하는데 자식은 부모 타입으로 자동 타입 변환이 가능함  

```java
부모타입 변수 = 자식타입; // 자동타입변환 
```

자식은 부모의 특징과 기능을 상속받기 때문에 부모와 동일하게 취급될 수 있다는 것  

(예시1) 부모 클래스

```
package sec02.exam00;

public class Animal {

}
```

(예시2) 자식 클래스

```java
package sec02.exam00;

public class Cat extends Animal {

}
```

(예시3) 자동 타입 변환

```java
package sec02.exam00;

public class CatExample {

	public static void main(String[] args) {
		Animal animal = new Animal();
		Cat cat = new Cat();
		
		// 자동 타입 변환
		animal = cat;
		
		// 참조 객체 확인 
		System.out.println(animal == cat);
	}

}
```

cat과 animal 변수는 타입만 다를 뿐, 동일한 Cat 객체를 참조함  



바로 위의 부모가 아니더라도 상속 계층에서 상위 타입이라면 자동 타입 변환이 일어날 수 있음

(예시)

```java
package sec02.exam01;

class A {}

class B extends A {}
class C extends A {}

class D extends B {}
class E extends C {}

public class PromotionExample {
	public static void main(String[] args) {
		B b = new B();
		C c = new C();
		D d = new D();
		E e = new E();
		
		A a1 = b;
		A a2 = c;
		A a3 = d;
		A a4 = e;
		
		B b1 = d;
		//B b2 = e; // 상속 관계에 있지 않기 때문에 컴파일 에러 발생 
		
		C c1 = e;
		//C c2 = d; // 상속 관계에 있지 않기 때문에 컴파일 에러 발생 
	}

}
```



부모 타입으로 자동 타입 변환된 이후로는 부모 클래스에 선언된 필드와 메소드만 접근이 가능함  

**(★중요) 예외 : 메소드가 자식 클래스에서 재정의되었다면 자식 클래스의 메소드가 대신 호출됨**

(예시1) 부모 클래스

```java
package sec02.exam02;

public class Parent {
	public void method1() {
		System.out.println("Parent-method1()");
	}
	
	public void method2() {
		System.out.println("Parent-method2()");
	}
}
```

(예시2) 자식 클래스

```java
package sec02.exam02;

public class Child extends Parent{
	// 메소드 재정의 
  @Override
	public void method2() {
		System.out.println("Child-method2()");
	}
	
	public void method3() {
		System.out.println("Child-method3()");
	}
}
```

(예시3) 자동 타입 변환 후 멤버 접근

```java
package sec02.exam02;

public class ChildExample {

	public static void main(String[] args) {
		Child child = new Child();
		
		// 자동 타입 변환 
		Parent parent = child;
		
		parent.method1(); // 실행 결과 : Parent-method1()
		parent.method2(); // 실행 결과 : Child-method2()
		//parent.method3();
	}

}
```



### 07-2-2. 필드의 다형성

###### 필드의 다형성

필드의 타입을 부모 타입으로 선언하면 다양한 자식 객체들이 저장될 수 있기 때문에 필드 사용 결과가 달라질 수 있음 



객체 지향 프로그래밍에서 프로그램은 수많은 객체들이 서로 연결되고 각자의 역할을 하게 되는데, 이 객체들은 다른 객체들로 교체될 수 있어야 함  

- 다형성을 구현할 수 있는 3가지 기술적 조건  
  1. 상속
  2. 메소드 재정의
  3. 타입 변환

부모 클래스를 상속하는 자식 클래스는 부모가 가지고 있는 필드와 메소드를 가지고 있으니 사용 방법은 동일함  

자식 클래스는 부모의 메소드를 재정의해서 메소드의 실행 내용을 변경함으로써 더 우수한 실행결과가 나오게 할 수도 있음  

자식 타입을 부모 타입으로 변환할 수 있음  



#### Tire 클래스

```java
package sec02.exam03;

public class Tire {
	// field
	public int maxRotation; // 최대 회전수(타이어 수명) 
	public int accumulatedRotation; // 누적 회전수 
	public String location; // 타이어의 위치 
	
	// constructor
	Tire(String location, int maxRotation) {
		this.location = location;
		this.maxRotation = maxRotation;
	}
	
	// method
	public boolean roll() {
		++accumulatedRotation; // 누적 회전수 1 증가 
		if (accumulatedRotation < maxRotation) {
			System.out.println(location + " Tire 수명 : " + (maxRotation - accumulatedRotation) + "회");
			return true;
		} else {
			System.out.println("***" + location + " Tire 펑크 ***");
			return false;
		}
	}
}
```



#### Car 클래스

```java
package sec02.exam03;

public class Car {
	// field
	Tire frontLeftTire = new Tire("앞왼쪽", 6);
	Tire frontRightTire = new Tire("앞오른쪽", 2);
	Tire backLeftTire = new Tire("뒤왼쪽", 3);
	Tire backRightTire = new Tire("뒤오른쪽", 4);
	
	//  constructor 
	
	// method
	// 모든 타이어를 1회 회전시키기 위해 각 Tire 객체의 roll() 메소드를 호출, false를 리턴하는 roll()이 있을 경우 stop() 메소드를 호출하고 해당 타이어 번호를 리턴 
	int run() {
		System.out.println("[자동차가 달립니다.]");
		if(frontLeftTire.roll()==false) {
			stop();
			return 1;
		}
		if(frontRightTire.roll()==false) {
			stop();
			return 2;
		}
		if(backLeftTire.roll()==false) {
			stop();
			return 3;
		}
		if(backRightTire.roll()==false) {
			stop();
			return 4;
		}
		return 0;
	}
	
	void stop() {
		System.out.println("[자동차가 멈춥니다.]");
	}
}
```



#### HankookTire, KumhoTire 클래스

```java
package sec02.exam03;

public class HankookTire extends Tire {
	// field 
	
	// constructor 
	public HankookTire(String location, int maxRotation) {
		super(location, maxRotation);
	}
	
	// method 
	@Override
	public boolean roll() {
		++accumulatedRotation;
		if(accumulatedRotation<maxRotation) {
			System.out.println(location + " HankookTire 수명 : " + (maxRotation-accumulatedRotation) + "회");
			return true;
		} else {
			System.out.println("*** " + location + " HankookTire 펑크 ***");
			return false;
		}
	}

}
```

```java
package sec02.exam03;

public class KumhoTire extends Tire {
	// field
	
	// constructor
	public KumhoTire(String location, int maxRotation) {
		super(location, maxRotation);
	}

	// method
	@Override
	public boolean roll() {
		++accumulatedRotation;
		if(accumulatedRotation<maxRotation) {
			System.out.println(location + " KumhoTire 수명 : " + (maxRotation-accumulatedRotation) + "회");
			return true;
		} else {
			System.out.println("*** " + location + " KumhoTire 펑크 ***");
			return false;
		}
	}
	
}
```



#### CarExample 클래스

```java
package sec02.exam03;

public class CarExample {

	public static void main(String[] args) {
		Car car = new Car();
		
		for(int i=0; i<10; i++) {
			int problemLocation = car.run();
			
			switch(problemLocation) {
				case 1:
					System.out.println("앞왼쪽 HankookTire로 교체");
					car.frontLeftTire = new HankookTire("앞왼쪽", 15);
					break;
				case 2:
					System.out.println("앞오른쪽 HankookTire로 교체");
					car.frontRightTire = new HankookTire("앞오른쪽", 15);
					break;
				case 3:
					System.out.println("뒤왼쪽 KumhoTire로 교체");
					car.backLeftTire = new KumhoTire("뒤왼쪽", 12);
					break;
				case 4:
					System.out.println("뒤오른쪽 KumhoTire로 교체");
					car.backRightTire = new KumhoTire("뒤오른쪽", 12);
					break;
			}
			System.out.println("--------------------");
		}
	}

}
```



실행 결과  

```java
[자동차가 달립니다.]
앞왼쪽 Tire 수명 : 5회
앞오른쪽 Tire 수명 : 1회
뒤왼쪽 Tire 수명 : 2회
뒤오른쪽 Tire 수명 : 3회
--------------------
[자동차가 달립니다.]
앞왼쪽 Tire 수명 : 4회
***앞오른쪽 Tire 펑크 ***
[자동차가 멈춥니다.]
앞오른쪽 HankookTire로 교체
--------------------
[자동차가 달립니다.]
앞왼쪽 Tire 수명 : 3회
앞오른쪽 HankookTire 수명 : 14회
뒤왼쪽 Tire 수명 : 1회
뒤오른쪽 Tire 수명 : 2회
--------------------
[자동차가 달립니다.]
앞왼쪽 Tire 수명 : 2회
앞오른쪽 HankookTire 수명 : 13회
***뒤왼쪽 Tire 펑크 ***
[자동차가 멈춥니다.]
뒤왼쪽 KumhoTire로 교체
--------------------
[자동차가 달립니다.]
앞왼쪽 Tire 수명 : 1회
앞오른쪽 HankookTire 수명 : 12회
뒤왼쪽 KumhoTire 수명 : 11회
뒤오른쪽 Tire 수명 : 1회
--------------------
[자동차가 달립니다.]
***앞왼쪽 Tire 펑크 ***
[자동차가 멈춥니다.]
앞왼쪽 HankookTire로 교체
--------------------
[자동차가 달립니다.]
앞왼쪽 HankookTire 수명 : 14회
앞오른쪽 HankookTire 수명 : 11회
뒤왼쪽 KumhoTire 수명 : 10회
***뒤오른쪽 Tire 펑크 ***
[자동차가 멈춥니다.]
뒤오른쪽 KumhoTire로 교체
--------------------
[자동차가 달립니다.]
앞왼쪽 HankookTire 수명 : 13회
앞오른쪽 HankookTire 수명 : 10회
뒤왼쪽 KumhoTire 수명 : 9회
뒤오른쪽 KumhoTire 수명 : 11회
--------------------
[자동차가 달립니다.]
앞왼쪽 HankookTire 수명 : 12회
앞오른쪽 HankookTire 수명 : 9회
뒤왼쪽 KumhoTire 수명 : 8회
뒤오른쪽 KumhoTire 수명 : 10회
--------------------
[자동차가 달립니다.]
앞왼쪽 HankookTire 수명 : 11회
앞오른쪽 HankookTire 수명 : 8회
뒤왼쪽 KumhoTire 수명 : 7회
뒤오른쪽 KumhoTire 수명 : 9회
--------------------
```



### 07-2-3. 매개 변수의 다형성

###### 매개 변수의 다형성

매개 변수의 타입이 클래스일 경우, 해당 클래스의 객체뿐만 아니라 자식 객체까지도 매개값으로 사용할 수 있음

이 때, 매개값으로 어떤 자식 객체가 제공되느냐에 따라 메소드의 실행 결과가 다양해질 수 있음  

자식 객체가 부모의 메소드를 재정의했다면 메소드 내부에서 재정의된 메소드를 호출함으로써 메소드의 실행결과는 다양해짐  



(예시1) 부모 클래스

```java
package sec02.exam04;

public class Vehicle {
	public void run() {
		System.out.println("차량이 달립니다.");
	}
}
```

(예시2) Vehicle을 이용하는 클래스

```java
package sec02.exam04;

public class Driver {
	public void drive(Vehicle vehicle) {
		vehicle.run();
	}
}
```

(예시3) 자식클래스1 

```java
package sec02.exam04;

public class Bus extends Vehicle {
	@Override
	public void run() {
		System.out.println("Bus가 달립니다.");
	}
}
```

(예시4) 자식클래스2

```java
package sec02.exam04;

public class Taxi extends Vehicle {
	@Override
	public void run() {
		System.out.println("Taxi가 달립니다.");
	}
}
```

(예시5) 실행 클래스

```java
package sec02.exam04;

public class DriverExample {

	public static void main(String[] args) {
		Driver driver = new Driver();
		Vehicle vehicle = new Vehicle();
		Bus bus = new Bus();
		Taxi taxi = new Taxi();
		
		driver.drive(vehicle);
		driver.drive(bus);
		driver.drive(taxi);
	}

}
```



### 07-2-4. 강제 타입 변환

###### 강제 타입 변환(casting)

부모 타입을 자식 타입으로 변환하는 것 

조건 : 자식 타입이 부모 타입으로 자동 타입 변환한 후 다시 자식 타입으로 변환할 때 강제 타입 변환을 사용할 수 있음  

```java
자식타입 변수 = (자식타입) 부모타입; // 강제 타입 변환 
```

자식 타입이 부모 타입으로 자동 타입 변환하면 부모에 선언된 필드와 메소드만 사용 가능함  

만약 자식에 선언된 필드와 메소드를 꼭 사용해야 한다면 강제 타입 변환을 해서 다시 자식 타입으로 변환한 다음 자식의 필드와 메소드를 사용하면 됨  



(예시1) 부모 클래스 

```java
package sec02.exam05;

public class Parent {
	public String field1;
	
	public void method1() {
		System.out.println("Parent-method1()");
	}
	
	public void method2() {
		System.out.println("Parent-method2()");
	}
}
```

(예시2) 자식 클래스

```java
package sec02.exam05;

public class Child extends Parent {
	public String field2;
	
	public void method3() {
		System.out.println("Child-method3()");
	}
}
```

(예시3) 강제 타입 변환

```java
package sec02.exam05;

public class ChildExample {

	public static void main(String[] args) {
		// 자동 타입 변환 
		Parent parent = new Child();
		
		parent.field1 = "xxx";
		//parent.field2 = "yyy";
		parent.method1();
		parent.method2();
		//parent.method3();
		
		// 강제 타입 변환 
		Child child = (Child) parent;
		
		child.field2 = "yyy";
		child.method3();
		}

}
```



### 07-2-5. 객체 타입 확인

###### instance 연산자

어떤 객체가 어떤 클래스의 인스턴스인지 확인하기 위해 사용하는 연산자  

instanceof 연산자의 좌항에는 객체가 오고 우항에는 타입이 오는데, 좌항의 객체가 우항의 인스턴스이면 true를 리턴하고, 그렇지 않으면 false를 리턴함  

```java
boolean result = 좌항(객체) instanceof 우항(타입);
```



instanceof 연산자는 주로 매개값의 타입을 조사할 때 사용함  

메소드 내에서 강제 타입 변환이 필요할 경우 반드시 매개값이 어떤 객체인지 instanceof 연산자로 확인하고 안전하게 강제 타입 변환을 해야 함  

만약 타입을 확인하지 않고 강제 타입 변환을 시도하면 `ClassCastException` 이 발생할 수 있음  



(예시1) 부모 클래스

```java
package sec02.exam06;

public class Parent {

}
```

(예시2) 자식 클래스

```java
package sec02.exam06;

public class Child extends Parent {

}
```

(예시3) 객체 타입 확인

```java
package sec02.exam06;

public class InstanceofExample {

	public static void method1(Parent parent) {
		if(parent instanceof Child) {
			Child child = (Child) parent;
			System.out.println("method1 - Child로 변환 성공");
		} else {
			System.out.println("method1 - Child로 변환되지 않음");
		}
	}
	
	public static void method2(Parent parent) {
		Child child = (Child) parent;
		System.out.println("method2 - Child로 변환 성공");
	}
	
	public static void main(String[] args) {
		Parent parentA = new Child();
		method1(parentA);
		method2(parentA);
		
		Parent parentB = new Parent();
		method1(parentB);
		method2(parentB);
	}

}
```



실행결과

```java
method1 - Child로 변환 성공
Exception in thread "main" method2 - Child로 변환 성공
method1 - Child로 변환되지 않음
java.lang.ClassCastException: sec02.exam06.Parent cannot be cast to sec02.exam06.Child
	at sec02.exam06.InstanceofExample.method2(InstanceofExample.java:15)
	at sec02.exam06.InstanceofExample.main(InstanceofExample.java:26)
```





