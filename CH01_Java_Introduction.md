# Chapter 01. 자바 시작하기



## 01-1. 프로그래밍 언어와 자바



##### <핵심 키워드>

`기계어`, `프로그래밍 언어`, `소스 파일`, `컴파일`, `JDK`, `환경 변수`



###### 기계어

컴퓨터(운영체제)가 이해하고 실행할 수 있는 0과 1로 이루어진 코드   



###### 프로그래밍 언어

사람의 언어와 기계어의 다리 역할을 함  

C, C++, C#, 자바, 파이썬 등  



###### 소스 파일

프로그래밍 언어로 작성한 파일  



###### 컴파일

소스 파일을 기계어로 번역하는 것  





### 01-1-1. 자바 소개

##### 자바의 특징

- 모든 운영체제에서 실행 가능

- **객체 지향 프로그래밍(Object-Oriented Programming, OOP)**

  : 객체(부품)를 만들고, 이 객체들을 서로 연결해서 더 큰 프로그램을 완성하는 기법

- 메모리 자동 정리
- 오픈 소스 라이브러리가 풍부



### 01-1-2. 자바 개발 도구 설치(Mac 기준)

###### JDK

자바 개발 도구(Java Development Kit)의 줄임말

자바로 프로그램을 개발할 수 있는 실행 환경(JVM)과 개발 도구(컴파일러) 등을 제공



#####  Java 8 설치

1. [https://Java.sun.com](https://Java.sun.com) 접속 (oracle 계정 로그인 필요)
2. Java SE 8u311 클릭
3. macOS 클릭
4. x64 DMG Installer 다운로드
5. jdk-8u311-macosx-x64.dmg 파일 실행해서 다운로드 완료



#### 환경 변수 설정

###### 환경 변수

운영체제가 실행하는 데 필요한 정보를 제공해주는 변수

JDK를 설치한 후 명령 라인(터미널)에서 컴파일러(javac)와 실행(java) 명령어를 사용하려면 JAVA_HOME 환경 변수를 등록하고 PATH 환경 변수를 수정하는 것이 좋음



##### JAVA_HOME 환경 변수 등록(Terminal)

1. JDK(jdk1.8.0_301.jdk)가 설치된 경로로 이동

`% cd /Library/Java/JavaVirtualMachines/jdk1.8.0_301.jdk/Contents/Home`

2. vi에디터로 환경 변수 설정

`% vi ~/.bash_profile`

- vi에디터 사용법
  - i : 입력모드
  - esc : 입력이 끝나면 esc 누르고 입력모드 종료
  - :wq : 저장 후 종료
- ~/.bash_profile에 환경 변수 설정 작성하기

```java
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_301.jdk/Contents/Home
export PATH=${PATH}:$JAVA_HOME/bin
```

3. vi에디터 변경 사항 저장

`$ source ~/.bash_profile`

4. PATH(환경 변수 경로) 출력해보기

`$ echo $PATH`







## 01-2. 이클립스 개발 환경 구축



##### <핵심 키워드>

`이클립스`, `워크스페이스`, `뷰`, `퍼스펙티브`



###### 이클립스(Eclipse)

오픈 소스 통합 개발 환경(Integrated Development Environment, IDE)

IDE란 프로젝트 생성, 자동 코드 완성, 디버깅 등과 같이 개발에 필요한 여러 가지 기능을 통합적으로 제공해주는 틀



### 01-2-1. 이클립스 설치

1. https://www.eclipse.org/downloads/ 접속
2. Get Eclipse IDE 2021-06 아래 Download x86_64 클릭 후 Download 클릭
3. eclipse-inst-jre-mac64.dmg 파일 실행해서 다운로드 진행

4. eclipse installer에서 Eclipse IDE for Enterprise Java Developers 선택



### 01-2-2. 워크스페이스(Workspace)

###### 워크스페이스

이클립스 실행과 관련된 메타 데이터(metadata)와 프로젝트 폴더가 저장되는 폴더



#### Eclipse IDE Launcher 대화상자에서 워크스페이스 폴더 지정하기

`/Users/<userName>/Projects/SelfStudyJava-workspace`



##### +) 이클립스 초기화 방법

워크스페이스 폴더 안에는 .metadata 폴더가 존재하는데, 여기에 이클립스가 실행할 때 적용되는 메타 데이터들을 저장함

이클립스를 초기화하려면 이클립스를 종료하고 Workspace로 지정한 폴더 안에 있는 .metadata 폴더를 강제로 삭제한 후 이클립스를 재시작하면 초기 상태의 .metadata 폴더가 다시 생성됨



###### 메타데이터

색상 테마, 폰트 종류, 폰트 크기 등

이클립스가 재시작할 경우 이전에 작업한 환경을 복원할 목적으로 사용



### 01-2-3. 퍼스펙티브(Perspective)와 뷰(View)

###### 뷰(View)

이클립스 내부에서 사용되는 작은 창  



###### 퍼스펙티브(Perspective)

프로젝트를 개발할 때 유용하게 사용할 수 있는 뷰들을 미리 묶어 이름을 붙여놓은 것  







## 01-3. 자바 프로그램 개발 과정



##### <핵심 키워드>

`바이트 코드 파일`, `JVM`, `클래스 선언`, `main() 메소드`, `주석`, `실행문`



### 01-3-1. 바이트 코드 파일과 자바 가상 기계

###### 바이트 코드 파일(.class)

자바 소스 파일(.java)을 javac 명령어를 통해 컴파일한 파일



###### JVM

자바 가상 기계(Java Virtual Machine, JVM)는 바이트 코드 파일을 각 운영체제에 맞는 완전한 기계어로 번역하고 실행하는 역할을 함

java 명령어에 의해 구동됨

자바는 JVM을 사용함으로써 바이트 코드 파일을 다양한 운영체제에서 수정하지 않고 바로 사용할 수 있음



### 01-3-2. 프로젝트 생성부터 실행까지

#### 1. 프로젝트 생성

1. Java Project 이름은 'ch01'로 생성하기



#### 2. 소스 파일 생성과 작성

Hello.java 소스 파일을 생성하고 , "Hello, Java"를 모니터에 출력하는 코드 작성하기

1. Package name은 'sec03.exam01'로 생성하기
2. Java Class name은 'Hello'로 생성하기

```java
package sec03.exam01;

public class Hello {
	// 프로그램 실행 진입점
	public static void main(String[] args) {
		// 콘솔에 출력하는 실행
		System.out.println("Hello, Java");
		} // end of main
} // end of class

```



#### 3. 바이트 코드 실행

소스 파일 마우스 오른쪽 버튼 클릭 - [Run As] - [Java Application] 선택

콘솔에 Hello, Java 가 출력됨



### 01-3-3. 명령 라인에서 컴파일하고 실행하기

생략  



### 01-3-4. 프로그램 소스 분석

```java
// 패키지 선언
package sec03.exam01;

// 클래스 선언부
public class Hello {
	// 메소드 선언부
	public static void main(String[] args) { // main 메소드는 프로그램 실행 진입점
		// 콘솔에 출력하는 실행
		System.out.println("Hello, Java");
		} // end of main
} // end of class

```



###### 클래스

필드 또는 메소드를 포함하는 블록  



###### 메소드

어떤 일을 처리하는 실행문들을 모아 놓은 불록  



###### 클래스 선언

자바 소스 파일은 클래스 선언부와 클래스 블록으로 구성되는데, 이렇게 작성하는 것을 클래스 선언이라고 함



###### main() 메소드

java 명령어로 바이트 코드 파일을 실행하면 제일 먼저 main() 메소드를 찾아 블록 내부를 실행함  

그래서 main() 메소드를 프로그램 실행 진입점이라고 부름  



### 01-3-5. 주석 사용하기

###### 주석

프로그램 실행과는 상관없이 코드에 설명을 붙인 것  

주석은 컴파일 과정에서 무시되고 실행문만 바이트 코드로 번역됨  



- 주석 기호
  - 라인 주석 `//`  : //부터 라인 끝까지 주석으로 처리
  - 범위 주석 `/* */` : `/*`와 `*/` 사이에 있는 내용을 모두 주석으로 처리
  - 도큐먼트 주석 `/** */` : `/**` 와 `*/` 사이에 있는 내용을 모두 주석으로 처리, 주로 javadoc 명령어로 API 도큐먼트를 생성하는 데 사용함 



### 01-3-6. 실행문과 세미콜론(;)

###### 실행문

변수 선언, 값 저장, 메소드 호출에 해당하는 코드  

실행문 끝에는 반드시 세미콜론(;)을 붙여야 함  



```java
package sec03.exam02;

public class RunStatementExample {

	public static void main(String[] args) {
		int x = 1; // 변수 x를 선언하고 1을 저장 
		int y = 2; // 변수 y를 선언하고 2를 저장 
		int result = x + y; // 변수 result를 선언하고 x와 y를 더한 값을 저장 
		System.out.println(result); // 모니터에 출력하는 메소드를 호
	}

}
```







