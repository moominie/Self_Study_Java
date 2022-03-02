# Chapter 07. 상속1



## 07-1. 상속



##### <핵심 키워드>

`상속`, `메소드 재정의`, `final 클래스`, `final 메소드`    



###### 상속(inheritance)

객체 지향 프로그래밍에서 부모 클래스의 멤버를 자식 클래스에게 물려주는 것  

부모 클래스를 상위 클래스, 자식 클래스를 하위 클래스 또는 파생 클래스라고 부름  



- 상속의 장점

1. 이미 잘 개발된 클래스를 재사용해서 새로운 클래스를 만들기 때문에 중복되는 코드를 줄여준다.
2. 부모 클래스의 수정으로 모든 자식 클래스들도 수정되는 효과를 가져오기 때문에 유지 보수 시간을 최소화할 수 있다.  



### 07-1-1. 클래스 상속

자식 클래스를 선언할 때 어떤 부모 클래스를 상속받을 것인지 결정하고, 선택된 부모 클래스는 `extends` 뒤에 기술함

```java
class 자식클래스 extends 부모클래스 {
  // 필드
  // 생성자
  // 메소드
}
```



- 상속의 특징

1. 여러 개의 부모 클래스를 상속할 수 없다.

2. 부모 클래스에서 private 접근 제한을 갖는 필드와 메소드는 상속 대상에서 제외된다. 

   부모 클래스와 자식 클래스가 서로 다른 패키지에 존재한다면 default 접근 제한을 갖는 필드와 메소드도 상속 대상에서 제외된다. (public 접근 제한을 갖는 멤버만 상속됨)  



(예시1) 부모 클래스

```java
package sec01.exam01;

public class Cellphone {
	// field 
	String model;
	String color;
	
	// constructor 
	
	// method
	void powerOn() {
		System.out.println("전원을 켭니다.");
	}
	void powerOff() {
		System.out.println("전원을 끕니다.");
	}
	void bell( ) {
		System.out.println("벨이 울립니다.");
	}
	void sendVoice(String message) {
		System.out.println("자기 : " + message);
	}
	void receiveVoice(String message) {
		System.out.println("상대방 : " + message);
	}
	void hangUp() {
		System.out.println("전화를 끊습니다.");
	}
}
```

(예시2) 자식 클래스

```java
package sec01.exam01;

public class DmbCellphone extends Cellphone {
	// field
	int channel;
	
	// constructor
	DmbCellphone(String model, String color, int channel) {
		this.model = model;
		this.color = color;
		this.channel = channel;
	}
	
	// method
	void turnOnDmb() {
		System.out.println("채널 " + channel + "번 DMB 방송 수신을 시작합니다.");
	}
	void changeChannelDmb(int channel) {
		this.channel = channel;
		System.out.println("채널 " + channel + "번으로 바꿉니다.");
	}
	void turnOffDmb() {
		System.out.println("DMB 방송 수신을 멈춥니다.");
	}
}
```

(예시3) 자식 클래스 사용

```java
package sec01.exam01;

public class DmbCellphoneExample {

	public static void main(String[] args) {
		// DmbCellphone 객체 생성 
		DmbCellphone dmbCellphone = new DmbCellphone("아이폰13프로", "실버", 3);
		
		// Cellphone 클래스로부터 상속받은 필드 
		System.out.println("모델 : " + dmbCellphone.model);
		System.out.println("색상 : " + dmbCellphone.color);
		
		// DmbCellphone 클래스의 필드
		System.out.println("채널 : " + dmbCellphone.channel);
		
		// Cellphone 클래스로부터 상속받은 메소드 호출
		dmbCellphone.powerOn();
		dmbCellphone.bell();
		dmbCellphone.sendVoice("여보세요.");
		dmbCellphone.receiveVoice("안녕하세요. 저는 Siri입니다.");
		dmbCellphone.sendVoice("아 예. 반갑습니다.");
		dmbCellphone.hangUp();
		
		// DmbCellphone 클래스의 메소드 호출
		dmbCellphone.turnOnDmb();
		dmbCellphone.changeChannelDmb(11);
		dmbCellphone.turnOffDmb();
	}

}
```



### 07-1-2. 부모 생성자 호출

자식 객체를 생성하면, 부모 객체가 먼저 생성되고 그 다음에 자식 객체가 생성됨

```java
DmbCellphone dmbCellphone = new DmbCellphone();
```

위의 코드를 실행하면 자식 객체인 DmbCellphone 객체만 생성하는 것이 아니라 부모인 Cellphone 객체가 먼저 생성되고 자식인 DmbCellphone 객체가 생성됨  

모든 객체는 클래스의 생성자를 호출해야만 생성되며, **부모 생성자는 자식 생성자의 맨 첫 줄에서 호출됨**  

```java
public DmbCellphone() {
  super();
}
```

super()는 부모 클래스의 기본 생성자를 호출하므로 다음 생성자를 호출함

```java
public Cellphone() {}
```



직접 자식 생성자를 선언하고 명시적으로 부모 생성자를 호출하는 것도 가능함

```java
자식클래스(매개변수 선언, ...) {
  super(매개값, ...);
}
```

super(매개값, ...)는 매개값의 타입과 일치하는 부모 생성자를 호출함  



(예시1) 부모 클래스

```java
package sec01.exam02;

public class People {
	public String name;
	public String ssn;
	
	public People(String name, String ssn) {
		this.name = name;
		this.ssn = ssn;
	}
}
```

부모 클래스인 People 클래스는 기본 생성자가 없고 name과 ssn을 매개값으로 받아 객체를 생성시키는 생성자만 있음  

(예시2) 자식 클래스

```java
package sec01.exam02;

public class Student extends People {
	public int studentNo;
	
	public Student(String name, String ssn, int studentNo) {
	super(name, ssn); // 부모 생성자 호출 
	this.studentNo = studentNo;
	}
}
```

부모 클래스(People)를 상속하는 자식 클래스(Student)는 생성자에서 name, ssn, studentNo를 매개값으로 받아서 `super(name, ssn)`으로 부모 클래스(People)의 생성자인 `People(String name, String ssn)`을 호출함  

(예시3) 자식 클래스의 사용

```java
package sec01.exam02;

public class StudentExample {

	public static void main(String[] args) {
		// Student 객체 생성 
		Student student = new Student("홍길동", "123456-1234567", 1);
		
		// 부모 클래스로부터 상속받은 필드 출력 
		System.out.println("name : " + student.name);
		System.out.println("ssn : " + student.ssn);
		
		// 자식 클래스의 필드 출력 
		System.out.println("studentNo : " + student.studentNo);
	}

}
```



### 07-1-3. 메소드 재정의 (★중요)

###### 메소드 재정의(Overriding)

자식 클래스에서 부모 클래스의 메소드를 다시 정의하는 것

부모 클래스의 메소드가 자식 클래스가 사용하기에 적합하지 않은 경우 상속된 일부 메소드는 자식 클래스에서 다시 수정해서 사용해야 함  



#### 메소드 재정의 방법

- 메소드 재정의할 때 지켜야 할 규칙

1. 부모의 메소드와 동일한 시그너처(리턴 타입, 메소드 이름, 매개 변수 목록)를 가져야 한다.
2. 접근 제한을 더 강하게 재정의할 수 없다.
3. 새로운 예외(Exception)를 throws할 수 없다.



메소드가 재정의되면 부모 객체의 메소드는 숨겨지기 때문에, 자식 객체에서 메소드를 호출하면 재정의된 자식 메소드가 호출됨  



`@override` 어노테이션은 생략해도 좋으나, 이것을 붙여주면 해당 메소드가 정확히 재정의된 것인지 컴파일러가 확인하기 때문에 개발자의 실수를 줄여줌  



(예시1) 부모 클래스

```java
package sec01.exam03;

public class Calculator {
	double areaCircle(double r) {
		System.out.println("Calculator 객체의 areaCircle() 실행");
		return 3.14159 * r * r;
	}
}
```

(예시2) 자식 클래스

```java
package sec01.exam03;

public class Computer extends Calculator {
  // 메소드 재정의
	@Override
	double areaCircle(double r) {
		System.out.println("Computer 객체의 areaCircle() 실행");
		return Math.PI * r * r;
	}
}
```

(예시3) 메소드 재정의 테스트

```java
package sec01.exam03;

public class ComputerExample {

	public static void main(String[] args) {
	int r = 10;
	
	Calculator calc = new Calculator();
	System.out.println("원면적 : " + calc.areaCircle(r));
	System.out.println();
	
	Computer com = new Computer();
	System.out.println("원면적 : " + com.areaCircle(r));
	}

}
```



###### (추가) 이클립스 재정의 메소드 자동 생성

이클립스는 부모 메소드 중 하나를 선택해서 재정의 메소드를 자동 생성해주는 기능이 있음

1. 자식 클래스에서 재정의 메소드를 작성할 위치로 입력 커서를 옮긴다.
2. Source - Override/Implement Methods 선택
3. 부모 클래스에서 재정의될 메소드를 선택하고 OK 버튼 클릭



#### 부모 메소드 호출

자식 클래스 내부에서 재정의된 부모 클래스의 메소드를 호출해야 하는 상황에서는 명시적으로 super 키워드를 붙여서 부모 메소드를 호출할 수 있음

`super.부모메소드();`



(예시1) 부모 클래스

```java
package sec01.exam04;

public class Airplane {
	public void land() {
		System.out.println("착륙합니다.");
	}
	public void fly() {
		System.out.println("일반비행합니다.");
	}
	public void takeOff() {
		System.out.println("이륙합니다.");
	}
}
```

(예시2) 자식 클래스

```java
package sec01.exam04;

public class SupersonicAirplane extends Airplane {
	public static final int NORMAL = 1;
	public static final int SUPERSONIC = 2;
	
	public int flyMode = 1;

	@Override
	public void fly() {
		if (flyMode == SUPERSONIC) {
			System.out.println("초음속비행합니다.");
		} else {
			super.fly();
		}
	}
}
```

(예시3) 자식 클래스의 사용

```java
package sec01.exam04;

public class SupersonicAirplaneExample {

	public static void main(String[] args) {
		SupersonicAirplane sa = new SupersonicAirplane();
		sa.takeOff();
		sa.fly();
		sa.flyMode = SupersonicAirplane.SUPERSONIC;
		sa.fly();
		sa.flyMode = SupersonicAirplane.NORMAL;
		sa.fly();
		sa.land();
	}

}
```



### 07-1-4. final 클래스와 final 메소드

final 키워드는 클래스, 필드, 메소드를 선언할 때 사용할 수 있는데, 해당 선언이 최종 상태이고 결코 수정될 수 없음을 뜻함  

- 필드를 선언할 때 final 지정 : 초기값 설정 후 더 이상 값을 변경할 수 없음
- 클래스와 메소드를 선언할 때 final 지정 : 상속과 관련이 있음



#### 상속할 수 없는 final 클래스

final 클래스는 최종적인 클래스이므로 상속할 수 없는 클래스가 됨  

즉, final 클래스는 부모 클래스가 될 수 없어 자식 클래스를 만들 수 없음  

`public final class ClassName {...}`



#### 재정의할 수 없는 final 메소드

final 메소드는 최종적인 메소드이므로 재정의할 수 없는 메소드가 됨  

즉, 부모 클래스를 상속해서 자식 클래스를 선언할 때 부모 클래스에 선언된 final 메소드는 자식 클래스에서 재정의할 수 없음  

`public final 리턴 타입 메소드(매개 변수, ...) {...}`



### (추가) protected 접근 제한자

###### protected

public과 default 접근 제한의 중간쯤에 해당  

같은 패키지에서는 default와 같이 접근 제한이 없지만 다른 패키지에서는 자식 클래스만 접근을 허용함  

필드, 생성자, 메소드 선언에 사용될 수 있음  



(예시1)

```java
package sec01.exam07.pack2;

import sec01.exam07.pack1.A;

// A 클래스를 상속한 D 클래스 
public class D extends A{
	public D() {
		super();
		this.field = "value";
		this.method();
	}
}
```

(예시2)

```java
package sec01.exam07.pack1;

// A 클래스와 동일 패키지 내의 클래스 B 
public class B {
	public void method() {
		A a = new A();
		a.field = "value";
		a.method();
		}
}
```

(예시3)

```java
package sec01.exam07.pack2;

// A 클래스와 다른 패키지에 있는 C 클래스 
public class C {
	public void method() {
		//A a = new A();
		//a.field = "value";
		//a.method();
	}
}
```

(예시4)

```java
package sec01.exam07.pack2;

import sec01.exam07.pack1.A;

// A 클래스를 상속한 D 클래스 
public class D extends A{
	public D() {
		super();
		this.field = "value";
		this.method();
	}
}
```





