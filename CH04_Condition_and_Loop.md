# Chapter 04. 조건문과 반복문

자바 프로그램은 main() 메소드의 시작 중괄호 {에서 끝 중괄호}까지 위에서부터 아래로 실행하는 흐름을 가지고 있는데, 이러한 실행 흐름을 개발자가 원하는 방향으로 바꿀 수 있도록 해주는 것이 바로 `제어문`, 혹은 `흐름 제어문`이다.  

제어문의 종류에는 조건문과 반복문이 있다.  



## 04-1. 조건문: if문, switch문



##### <핵심 키워드>

`if문`, `if-else문`, `if-else if-else문` , `switch문` 



###### 조건문

조건식에 따라 다른 실행문을 실행하기 위해 사용되며, 조건문의 종류로는 if문과 switch문이 있음  



### 04-1-1. if문

if문은 조건식의 결과에 따라 블록 실행 여부가 결정됨  

조건식이 true이면 블록을 실행하고, false이면 블록을 실행하지 않음  

```java
if ( 조건식 ) {
  실행문A
}
실행문B
```

1. 조건식이 true이면 실행문A -> 실행문B 실행
2. 조건식이 false이면 실행문B 실행



### 04-1-2. if-else문

if문의 조건식이 true이면 if문의 블록이 실행되고, 조건식이 false이면 else 블록이 실행됨  

```java
if ( 조건식 ) {
  실행문A
} else {
  실행문B
}
실행문C
```

1. 조건식이 true이면 실행문A -> 실행문C 실행

2. 조건식이 false이면 실행문B -> 실행문C 실행



### 04-1-3. if-else if-else문

조건문이 여러 개인 if문  

처음 if문의 조건식이 true일 경우 다른 조건식의 결과에 따라 실행 블록을 선택할 수 있음  

else if문의 수는 제한이 없으며, 여러 개의 조건식 중 true가 되는 블록만 실행하고 전체 if문을 벗어나게 됨

```java
if ( 조건식1 ) {
  실행문A
} else if ( 조건식2 ) {
  실행문B
} else {
  실행문C
}
실행문D
```

1. 조건식1이 true이면 실행문A -> 실행문D 실행
2. 조건식1이 false이면 조건식2로 이동
3. 조건식2가 true이면 실행문B -> 실행문D 실행
4. 조건식2가 false이면 실행문C -> 실행문D 실행



(예시) 주사위를 굴려서 나올 수 있는 1, 2, 3, 4, 5, 6 중에서 하나의 수를 무작위로 뽑아서 출력하는 프로그램

```java
package sec01.exam04;

public class IfDiceExample {

	public static void main(String[] args) {
		// 주사위 번호 하나 뽑기 
		int num = (int) (Math.random() * 6) + 1;
		
		if (num==1) {
			System.out.println("1번이 나왔습니다.");
		} else if (num==2) {
			System.out.println("2번이 나왔습니다.");
		} else if (num==3) {
			System.out.println("3번이 나왔습니다.");
		} else if (num==4) {
			System.out.println("4번이 나왔습니다.");
		} else if (num==5) {
			System.out.println("5번이 나왔습니다.");
		} else {
			System.out.println("6번이 나왔습니다.");
		}

	}

}
```



(추가) 로또 번호 하나 뽑기

```java
int num = (int) (Math.random() * 45) + 1;
```



### 04-1-4. switch문

switch문은 변수가 어떤 값을 갖느냐에 따라 실행문이 선택됨  

```java
switch ( 변수 ) {
  case 값1:
    실행문A
    break;
 
  case 값2:
    실행문B
    break;
    
  default:
    실행문C
}
```

1. 변수가 값1과 동일할 경우 실행문A를 실행함, case 끝에 break가 붙어 있기 때문에 다음 case를 실행하지 않고 switch문을 빠져나감
2. 변수가 값2와 동일할 경우 실행문B를 실행함, case 끝에 break가 붙어 있기 때문에 다음 case를 실행하지 않고 switch문을 빠져나감
3. 변수가 값1과 값2와 모두 동일하지 않을 경우 default로 가서 실행문C를 실행함

*만약 case 끝에 break문이 없다면 다음 case가 연달아 실행되는데, 이때는 case 값과는 상관없이 실행됨*



(예시) char 타입 변수를 이용해서 알파벳 대소문자에 관계없이 동일하게 처리하도록 만든 switch문

```java
package sec01.exam07;

public class SwitchCharExample {

	public static void main(String[] args) {
		char grade = 'B';
		
		switch (grade) {
			case 'A' :
			case 'a' :
				System.out.println("우수 회원입니다.");
				break;
				
			case 'B' :
			case 'b' :
				System.out.println("일반 회원입니다.");
				break;
			
			default:
				System.out.println("손님입니다.");
		}

	}

} // 출력 결과 : 일반 회원입니다.
```







## 04-2. 반복문 : for문, while문, do-while문



##### <핵심 키워드>

`for문`, `while문`, `do-while문`, `break문`, `continue문`



###### 반복문

어떤 작업(코드)이 반복적으로 실행되도록 할 때 사용되며, 반복문의 종류로는 for문, while문, do-while문이 있음  



### 04-2-1. for문

for문은 주어진 횟수만큼 실행문을 반복 실행할 때 적합한 반복 제어문  

```java
for (①초기화식; ②조건식; ④증감식) {
  ③실행문;
}
```

1. for문이 처음 실행될 때 초기화식이 제일 먼저 실행
2. 조건식을 평가해서 true이면 for문 블록 내부의 실행문을 실행하고, false이면 for문 블록을 실행하지 않고 종료함
3. 블록 내부의 실행문들이 모두 실행되면 증감식을 실행하고 다시 조건식을 평가함
4. 조건식의 평가 결과가 true이면 실행문 -> 증감식 -> 조건식으로 다시 진행하고, false이면 for문이 종료됨



초기화식은 조건식과 실행문, 증감식에서 사용할 변수를 초기화하는 역할을 함  

초기화식과 증감식이 둘 이상 있을 경우에는 쉼표(,)로 구분해서 작성함  

초기화식에 선언된 변수는 for문 블록 내부에서 사용되는 로컬 변수이므로 for문을 벗어나서는 사용할 수 없음  

*for문 작성시 초기화식에서 루프 카운터 변수를 선언할 때 부동 소수점을 쓰는 float 타입을 사용하면 안 된다.*  



###### 중첩 for문

for문이 또 다른 for문을 내포한 것  

바깥쪽 for문이 한 번 실행할 때마다 중첩된 for문은 지정된 횟수만큼 반복해서 돌다가 다시 바깥쪽 for문으로 돌아감  

(예시) 구구단 출력하기

```java
package sec02.exam05;

public class ForMultiplicationTableExample {

	public static void main(String[] args) {
		for (int i=2; i<=9; i++) {
			System.out.println("*** " + i + "단 ***");
			for(int j=1; j<=9; j++) {
				System.out.println(i + " x " + j + " = " + (i*j));
			}
			System.out.println();
		}

	}

}
```



### 04-2-2. while문

while문은 조건식이 true일 경우에 계속해서 반복하며, 조건식이 false가 되면 반복 행위를 멈추고 while문을 종료함  

```java
while( 조건식 ) {
  실행문;
}
```

1. while문이 처음 실행될 때 조건식을 평가함
2. 평가 결과가 true이면 실행문을 실행함
3. 실행문이 모두 실행되면 조건식으로 되돌아가서 다시 조건식을 평가함
4. 만약 조건식이 true라면 실행문 -> 조건식으로 다시 진행함
5. 만약 조건식이 false라면 while문을 종료함  



(예시) 1부터 100까지 합을 출력하기

```java
package sec02.exam07;

public class WhileSumFrom1To100Example {

	public static void main(String[] args) {
		int i=1;
		int sum=0;
		while(i<=100) {
			sum += i;
			i++;
		}
		System.out.println(sum);

	}

}
```

while문 내부에서 계속 누적되는 값을 갖는 루프 카운터 변수는 while문이 시작하기 전에 미리 선언해놓아야 함  



### 04-2-3. do-while문

do-while문은 블록 내부의 실행문을 우선 한 번은 실행하고, 실행 결과에 따라서 반복 실행을 계속할지 결정함

```java
do {
  실행문;
} while ( 조건식 );
```

1. do-while문이 처음 실행될 때 실행문을 우선 실행함
2. 실행문이 모두 실행되면 조건식을 평가함
3. 조건식의 결과가 true이면 실행문 -> 조건식과 같이 반복 실행을 함
4. 조건식의 결과가 false이면 do-while문을 종료함



### 04-2-4. break문

break문은 반복문인 for문, while문, do-while문, 그리고 조건문인 switch문을 실행 중지할 때 사용함  

주로 if문과 함께 사용되어 if문의 조건식에 따라 반복문/조건문을 종료할 때 사용함  

(예시) while문을 이용해서 주사위 번호 중 하나를 반복적으로 무작위로 뽑되, 6이 나오면 while문을 종료하기  

```java
package sec02.exam08;

public class BreakExample {

	public static void main(String[] args) {
		
		while(true) {
			int num = (int) (Math.random() * 6) + 1;
			System.out.println(num);
			
			if (num == 6) {
				break;
			}
		}

	}

}
```



중첩 반복문의 경우 break문은 가장 가까운 반복문만 종료하고 바깥쪽 반복문은 종료하지 않음  

바깥쪽 반복문까지 종료시키려면 바깥쪽 반복문에 이름(라벨)을 붙이고 'break 이름;'을 사용함  

```java
Label: for (...) {
  for (...) {
    break Label;
  }
}
```



(예시) 바깥쪽 for문은 'A~Z'까지 반복하고 중첩된 for문은 'a~z'까지 반복하는데, 중첩된 for문에서 lower 변수가 'g' 값을 갖게 되면 바깥쪽 for문까지 빠져나오도록 하기

```java
package sec02.exam09;

public class BreakOutterExample {

	public static void main(String[] args) {
		Outter: for(char upper 'A'; upper <= 'Z'; upper++) {
			for(char lower 'a'; lower <= 'z'; lower++) {
				System.out.println(upper + " - " + lower);
				
				if (lower == 'g') {
					break Outter;
				}
			}
		}

	}

}
```



### 04-2-5. continue문

 continue문은 반복문인 for문, while문, do-while문에서만 사용되는데, 블록 내부에서 continue문이 실행되면 for문의 증감식 또는 while문, do-while문의 조건식으로 이동함  

continue문은 반복문을 종료하지 않고 계속 반복을 수행한다는 점이 break문과 다름  

주로 if문과 함께 사용되는데, 특정 조건을 만족하는 경우에 continue문을 실행해서 그 이후의 문장을 실행하지 않고 다음 반복으로 넘어감  

(예시) 1부터 10 사이의 수 중에서 짝수만 출력하기

```java
package sec02.exam10;

public class ContinueExample {

	public static void main(String[] args) {
		for(int i=1; i<=10; i++) {
			if (i % 2 == 1) {
				continue;
			}
			System.out.println(i);
		}
	}

}
```

