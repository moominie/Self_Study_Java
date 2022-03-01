# Chapter 06. 클래스4



## 06-6. 패키지와 접근 제한자



##### <핵심 키워드>

`패키지 선언`, `import문`, `접근 제한자`, `Getter/Setter`     



패키지의 기능

1. 파일 시스템의 폴더 기능

2. 클래스를 유일하게 만들어주는 식별자 역할

   클래스의 전체 이름 : `상위패키지.하위패키지.클래스` 



### 06-6-1. 패키지 선언

패키지 선언이란 클래스를 작성할 때 해당 클래스가 어떤 패키지에 속할 것인지를 선언하는 것  

- 클래스 작성 시 패키지 선언하는 방법

```java
package 상위패키지.하위패키지;

public class ClassName {...}
```

패키지는 클래스의 일부이므로 클래스만 따로 복사해서 다른 곳으로 이동하면 클래스를 사용할 수 없음  

만약 클래스를 이동해야 한다면 패키지 전체를 이동시켜야 함  



- 패키지 이름 작성 규칙

1. 숫자로 시작해서는 안 되고, _, $를 제외한 특수 문자를 사용해서는 안 된다.
2. java로 시작하는 패키지는 자바 표준 API에서만 사용하므로 사용해서는 안 된다.
3. 모두 소문자로 작성하는 것이 관례다.



#### 이클립스에서 패키지 생성과 클래스 생성

1. 프로젝트의 src 폴더를 선택한 후 마우스 오른쪽 버튼 클릭  

   File - New - Package 선택

2. Name 입력란에 `상위패키지.하위패키지` 형태로 입력 후 Finish 선택

3. 이클립스는 기본적으로 패키지를 Flat 방식으로 표시함  

   만약 상하위 패키지를 계층적으로 보고 싶다면 Package Explorer 뷰의 오른쪽 상단 점 3개 버튼을 클릭하고 Package Presentation - Hierarchical을 선택

4. 생성된 패키지를 선택한 후 마우스 오른쪽 버튼 클릭

   File - New - Class 선택

5. Name 입력란에 클래스 이름을 입력 후 Finish 선택



#### import문

사용하고자 하는 클래스 또는 인터페이스가 다른 패키지에 소속되어 있다면, import문으로 해당 패키지의 클래스 또는 인터페이스를 가져와 사용할 것임을 컴파일러에게 알려줘야 함  

- import문을 작성하는 방법

`import 상위패키지.하위패키지.클래스이름;`

`import 상위패키지.하위패키지.*;` 

import문은 패키지 선언과 클래스 선언 사이에 작성함  

만약 사용하고자 하는 클래스들이 동일 패키지 소속이라면 `*` 을 이용해서 해당 패키지에 소속된 클래스들을 사용할 것임을 알릴 수 있음  

*상위 패키지와 하위 패키지는 따로 import문을 작성해야 함*  

*서로 다른 패키지에 동일한 클래스 이름이 존재할 때, import문과 상관없이 패키지가 포함된 클래스의 전체 이름을 코드에 기술해야 함*



(예시) sec06.exam02.hyundai, sec06.exam02.hankook, sec06.exam02.kumho 3개의 패키지를 만들고 세 패키지를 모두 사용하는 Car.java 소스코드 만들기  

```java
package sec06.exam02.mycompany;

import sec06.exam02.hyundai.Engine;
import sec06.exam02.hankook.*;
import sec06.exam02.kumho.*;

public class Car {
	// 필드 
	Engine engine = new Engine();
	SnowTire tire1 = new SnowTire();
	BigWidthTire tire2 = new BigWidthTire();
	//Tire tire3 = new Tire();
	sec06.exam02.hankook.Tire tire3 = new sec06.exam02.hankook.Tire();
	sec06.exam02.kumho.Tire tire4 = new sec06.exam02.kumho.Tire();

}
```



###### (추가) 이클립스 import문 자동 추가 기능

현재 작성 중인 클래스에서 Source - Organize Imports 메뉴를 선택하거나 단축기 `Command + Shift + O (mac 기준)` 누르기



### 06-6-2. 접근 제한자

###### 접근 제한자(Access Modifier)

클래스 및 인터페이스 그리고 이들이 가지고 있는 멤버들에 대한 접근을 제어하기 위해 사용됨  



- 접근 제한자의 종류

1. public : 외부 클래스가 자유롭게 사용할 수 있도록 함
2. protected : 같은 패키지 또는 자식 클래스에서 사용할 수 있도록 함 
3. default : 같은 패키지에 소속된 클래스에서만 사용할 수 있도록 함 
4. private : 외부에서 사용할 수 없도록 함



### 06-6-3. 클래스의 접근 제한

클래스를 선언할 때 해당 클래스를 다른 패키지에서도 사용할 것인지, 아니면 같은 패키지 내에서만 사용할 것인지에 따라 public, default 접근 제한을 결정함

```java
// public 접근 제한
public class ClassName {...}

// default 접근 제한
class ClassName {...}
```



#### default 접근 제한

클래스를 선언할 때 public을 생략했다면 클래스는 default 접근 제한을 가짐  

같은 패키지 내에서는 아무런 제한 없이 사용할 수 있지만 다른 패키지에서는 사용할 수 없도록 제한됨  



#### public 접근 제한

클래스를 선언할 때 public 접근 제한자를 붙였다면 클래스는 public 접근 제한을 가짐  

같은 패키지뿐만 아니라 다른 패키지에서도 아무런 제한없이 사용할 수 있음  

클래스를 다른 개발자가 사용할 수 있도록 라이브러리 클래스로 개발한다면 반드시 public 접근 제한을 갖도록 해야 함  



(예시) 클래스의 접근 제한

```java
package sec06.exam03.package1;

// default 클래스 선언 
class A {

}
```

```java
package sec06.exam03.package1;

// public 클래스 선언 
public class B {
	A a; // 같은 패키지이므로 A 클래스에 접근 가능 

}
```

```java
package sec06.exam03.package2;

import sec06.exam03.package1.*;

// public 클래스 선언 
public class C {
	//A a; // 다른 패키지이므로 default 접근 제한을 갖는 A 클래스에 접근 안 됨 
	B b; // 다른 패키지이지만 public 접근 제한을 갖는 B 클래스에는 접근 가능 

}
```



### 06-6-4. 생성자의 접근 제한

객체를 생성하기 위해서 new 연산자로 생성자를 호출하는데, 생성자가 어떤 접근 제한을 갖느냐에 따라 호출 가능 여부가 결정됨  

```java
public class ClassName {
  // public 접근 제한
  public ClassName(...) {...}
  
  // protected 접근 제한
  protected ClassName(...) {...}
  
  // default 접근 제한
  ClassName(...) {...}
  
  // private 접근 제한
  private ClassName(...) {...}
}
```

클래스에 생성자를 선언하지 않으면 컴파일러에 의해 자동으로 기본 생성자가 추가되는데, 이때 기본 생성자의 접근 제한은 클래스의 접근 제한과 동일함  



##### public 접근 제한

모든 패키지에서 아무런 제한 없이 생성자를 호출할 수 있도록 함



##### protected 접근 제한

같은 패키지에 속하는 클래스 또는 다른 패키지에 속한 클래스가 해당 클래스의 자식(child) 클래스일 때 생성자를 호출할 수 있음 



##### default 접근 제한

생성자를 선언할 때 접근 제한자를 생략하면 default 접근 제한을 가짐  

같은 패키지에서는 아무런 제한 없이 생성자를 호출할 수 있음



##### private 접근 제한

오로지 클래스 내부에서만 생성자를 호출할 수 있고 객체를 만들 수 있음  



(예시) 생성자의 접근 제한

```java
package sec06.exam04.package1;

public class A {
	// 필드 
	A a1 = new A(true);
	A a2 = new A(1);
	A a3 = new A("문자열");
	
	// 생성자 
	public A(boolean b) {} // public 접근 제한 
	A(int b) {} // default 접근 제한 
	private A(String s) {} // private 접근 제한 
}
```

```java
package sec06.exam04.package1;

// A와 동일 패키지인 B 클래스
public class B {
	// 필드 
	A a1 = new A(true);
	A a2 = new A(1);
	//A a3 = new A("문자열"); // private 생성자 접근 불가 
}
```

```java
package sec06.exam04.package2;

import sec06.exam04.package1.*;

// A와 다른 패키지의 클래스 C 
public class C {
	// 필드
	A a1 = new A(true);
	//A a2 = new A(1); // default 생성자 접근 불가 
	//A a3 = new A("문자열"); // private 생성자 접근 불가 
}
```



###### (추가) 싱글톤(Singleton) 패턴 

전체 프로그램에서 단 하나의 객체만 만들도록 보장해야 하는 경우 여러 개의 객체를 만들지 못하도록 설계하는 것  

생성자를 private 접근 제한으로 선언하고, 자신의 유일한 객체를 리턴하는 getInstance() 정적 메소드를 선언하는 것  



### 06-6-5. 필드와 메소드의 접근 제한

필드와 메소드를 선언할 때 해당 필드와 메소드를 클래스 내부에서만 사용할 것인지, 패키지 내에서만 사용할 것인지, 아니면 다른 패키지에서도 사용할 수 있도록 할 것인지를 결정해야 함  

이것은 필드와 메소드가 어떤 접근 제한을 갖느냐에 따라 결정됨  



##### public 접근 제한

모든 패키지에서 아무런 제한 없이 필드와 메소드를 사용할 수 있음  



##### protected 접근 제한

같은 패키지에 속하는 클래스 또는 다른 패키지에 속한 클래스가 해당 클래스의 자식(child) 클래스일 때 필드와 메소드를 사용할 수 있음  



##### default 접근 제한

필드와 메소드를 선언할 때 접근 제한자를 생략하면 default 접근 제한을 가짐  

같은 패키지에서는 아무런 제한 없이 필드와 메소드를 사용할 수 있음  



##### private 접근 제한

오로지 클래스 내부에서만 필드와 메소드를 사용할 수 있음 



(예시) 필드와 메소드의 접근 제한

```java
package sec06.exam05.package1;

public class A {
	// 필드 
	public int field1; // public 접근 제한 
	int field2; // default 접근 제한 
	private int field3; // private 접근 제한 
	
	// 생성자
	public A() {
		field1 = 1;
		field2 = 1;
		field3 = 1;
		
		method1();
		method2();
		method3();
	}
	
	// 메소드
	public void method1() {} // public 접근 제한 
	void method2() {} // default 접근 제한 
	private void method3() {} // private 접근 제한 
}
```

```java
package sec06.exam05.package1;

// A 클래스와 동일 패키지 내의 B 클래스 
public class B {
	public B() {
		A a = new A();
	
		a.field1 = 1;
		a.field2 = 1;
		//a.field3 = 1; // private 필드 접근 불가 
	
		a.method1();
		a.method2();
		//a.method3(); // private 메소드 접근 불가 
	}
}
```

```java
package sec06.exam05.package2;

import sec06.exam05.package1.A;

// A 클래스와 다른 패키지 내의 클래스 C
public class C {
	public C() {
		A a = new A();
		a.field1 = 1;
		//a.field2 = 1; // default 필드 접근 불가 
		//a.field3 = 1; // private 필드 접근 불가 
		
		a.method1();
		//a.method2(); // default 메소드 접근 불가 
		//a.method3(); // private 메소드 접근 불가 
	}
}
```



### 06-6-6. Getter와 Setter 메소드

일반적으로 객체 지향 프로그래밍에서는 객체의 무결성(결점이 없는 성질)이 깨질 수도 있기 때문에 객체의 필드를 객체 외부에서 직접적으로 접근하는 것을 막음  

대신 필드는 외부에서 접근할 수 없도록 막고 메소드는 공개해서 외부에서 메소드를 통해 필드를 변경하는 방법을 선호함  

필드값을 직접 사용하면 부적절한 경우도 있기 때문에 외부에서 객체의 데이터를 읽을 때도 메소드를 사용하는 것이 좋음  

즉 클래스를 선언할 때 가능하다면 필드를 private으로 선언해서 외부로부터 보호하고, 필드에 대한 Setter와 Getter 메소드를 작성해서 필드값을 안전하게 변경/사용하는 것이 좋음  

 

###### Setter 메소드  

매개값을 검증해서 유효한 값만 객체의 필드로 저장할 수 있도록 한 메소드  



###### Getter 메소드

필드값을 가공한 후 외부로 전달하는 메소드  



- Setter와 Getter 메소드를 선언하는 방법

```java
private 타입 fieldName;

// Getter
public 리턴 타입 getFieldName() {
  return fieldName;
}

// Setter
public void setFieldName(타입 fieldName) {
  this.fieldName = fieldName;
}
```



필드 타입이 boolean일 경우에는 Getter는 get이 아닌 is로 시작하는 것이 관례  

```java
private boolean stop;

// Getter
public boolean isStop() {
  return stop;
}

// Setter
public void setStop(boolean stop) {
  this.stop = stop;
}
```



만약 외부에서 필드값을 읽을 수만 있고 변경하지 못하도록 하려면 (읽기 전용) Getter 메소드만 선언해도 좋고, 아니면 Setter 메소드가 private 접근 제한을 갖도록 선언해도 좋음  



###### (추가) 이클립스 Getter/Setter 메소드 자동 생성

이클립스는 클래스에 선언된 필드에 대해 자동으로 Getter와 Setter 메소드를 생성시키는 기능이 있음  

필드 선언 후 Source - Generate Getters and Setters 메뉴를 선택  



(예시1) Car.java

```java
package sec06.exam06;

public class Car {
	// 필드 
	private int speed;
	private boolean stop;
	
	// 생성자
	
	// 메소드 
	public int getSpeed() {
		return speed;
	}
	
	public void setSpeed(int speed) {
		if (speed<0) {
			this.speed = 0;
			return;
		} else {
			this.speed = speed;
		}
	}
	
	public boolean isStop() {
		return stop;
	}
	
	public void setStop(boolean stop) {
		this.stop = stop;
		this.speed = 0;
	}
}
```



(예시2) CarExample.java

```java
package sec06.exam06;

public class CarExample {

	public static void main(String[] args) {
		Car myCar = new Car();
		
		// 잘못된 속도 변경 
		myCar.setSpeed(-50);
		System.out.println("현재 속도 : " + myCar.getSpeed() + "km/h");
		
		// 올바른 속도 변경 
		myCar.setSpeed(60);
		System.out.println("현재 속도 : " + myCar.getSpeed() + "km/h");
		
		// 멈춤 
		if(!myCar.isStop()) {
			myCar.setStop(true);
		}
		System.out.println("현재 속도 : " + myCar.getSpeed() + "km/h");
	}

}
```





