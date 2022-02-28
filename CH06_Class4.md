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



### 06-6-3. 클래스의 접근 제한

#### default 접근 제한

#### public 접근 제한



### 06-6-4. 생성자의 접근 제한



### 06-6-5. 필드와 메소드의 접근 제한



### 06-6-6. Getter와 Setter 메소드

