# Chapter 05. 참조 타입2



## 05-2. 배열



##### <핵심 키워드>

`배열`, `인덱스`, `배열 길이`, `배열 선언`, `배열 생성`, `다차원 배열`, `향상된 for문`



### 05-2-1. 배열이란?

###### 배열

같은 타입의 데이터를 연속된 공간에 나열하고, 각 데이터에 인덱스(index)를 부여해놓은 자료구조  



`배열[인덱스]`

배열의 각 인덱스는 각 항목의 데이터를 읽거나 저장하는 데 사용됨  

배열 이름 옆의 대괄호[] 안에 인덱스를 기입하며, 인덱스는 0부터 시작함  



- 배열의 특징

  1. 배열은 같은 타입의 데이터만 저장할 수 있다. 

     또한 선언과 동시에 저장할 수 있는 타입이 결정되며, 만약 다른 타입의 값을 저장하려고 하면 타입 불일치(Type mismatch) 컴파일 에러가 발생한다.  

  2. 한 번 생성된 배열은 길이를 늘리거나 줄일 수 없다.  

     이미 생성된 배열의 길이보다 더 많거나 적은 개수의 값을 저장하려면 다른 길이의 새로운 배열을 생성하고, 기존 배열 항목을 새 배열로 복사해야 한다.  



### 05-2-2. 배열 선언

- 배열을 선언하는 두 가지 방식

1. 타입[] 변수;
2. 타입 변수[];

대괄호[]는 배열 변수를 선언하는 기호로 사용됨  

타입은 배열에 저장될 데이터의 타입을 의미함  

(예시)

```java
int[] intArray;
double[] doubleArray;
String[] strArray;

int intArray[];
double doubleArray[];
String strArray[];
```



### 05-2-3. 배열 생성

- 배열 객체를 생성하는 두 가지 방식
  1. 값 목록으로 배열 생성
  2. new 연산자로 배열 생성  



#### 값 목록으로 배열 생성

값의 목록이 있을 때 사용  

`타입[] 변수 = {값0, 값1, 값2, 값3, ...};`

중괄호{}는 주어진 값들을 항목으로 가지는 배열 객체를 힙에 생성하고, 배열 객체의 번지를 리턴함  

배열 변수는 리턴된 번지를 저장함으로써 참조가 이루어짐  

(예시)

```java
package sec02.exam01;

public class ArrayCreateByValueListExample1 {

	public static void main(String[] args) {
		int[] scores = { 83, 90, 87 };
		
		System.out.println("scores[0] : " + scores[0]); // scores[0] : 83
		System.out.println("scores[1] : " + scores[1]); // scores[1] : 90
		System.out.println("scores[2] : " + scores[2]); // scores[2] : 87
		
		int sum = 0;
		for (int i=0; i<scores.length; i++) {
			sum += scores[i];
		}
		
		System.out.println("총합 : " + sum); // 총합 : 260
		
		double avg = (double) sum / scores.length;
		System.out.println("평균 : " + avg); // 평균 : 86.66666666666667
		
	}

}
```



*(주의1) 값 목록으로 배열 객체를 생성할 때 배열 변수를 이미 선언한 후에는 다른 실행문에서 중괄호를 사용한 배열 생성이 허용되지 않는다.*

해결 방법 : new 연산자를 사용해서 값 목록을 지정한다.

```java
String[] names = null;
names = new String[] {"신용권", "홍길동", "감자바"}
```



*(주의2) 메소드의 매개값이 배열인 경우도 마찬가지!*  

(예시) 매개 변수로 int[] 배열이 선언된 add() 메소드가 있을 경우, 값 목록으로 배열을 생성함과 동시에 add() 메소드의 매개값으로 사용하고자 할 때에는 반드시 new 연산자를 사용해야 함

```java
int add(int[] scores) {...}

int result = add( {95, 85, 90} ); // 컴파일 에러
int result = add( new int[] {95, 85, 90} );
```



(예시)

```java
package sec02.exam02;

public class ArrayCreateByValueListExample2 {

	public static void main(String[] args) {
		int[] scores;
		scores = new int[] {83, 90, 87};
		
		int sum1 = 0;
		for (int i=0; i<scores.length; i++) {
			sum1 += scores[i];
		}
		System.out.println("총합 : " + sum1); // 총합 : 260
		
		int sum2 = add(new int[] {83, 90, 87});
		System.out.println("총합 : " + sum2); // 총합 : 260
	}
	
	// 점수 총합을 계산해서 리턴하는 메소드 
	public static int add(int[] scores) {
		int sum = 0;
		for (int i=0; i<scores.length; i++) {
			sum += scores[i];
		}
		return sum;
	}

}
```



#### new 연산자로 배열 생성

값의 목록을 가지고 있지 않지만, 향후 값들을 저장할 배열을 미리 만들고 싶다면 new 연산자로 배열 생성  

`타입[] 변수 = new 타입[길이]`   

길이는 배열이 저장할 수 있는 값의 개수를 의미함   

new 연산자로 배열을 처음 생성할 경우 배열은 자동적으로 기본값으로 초기화됨   



- 타입별 배열의 초기값  

| 분류            | 타입       | 초기값   |
| --------------- | ---------- | -------- |
| 기본 타입(정수) | byte[]     | 0        |
|                 | char[]     | '\u0000' |
|                 | short[]    | 0        |
|                 | int[]      | 0        |
|                 | long[]     | 0L       |
| 기본 타입(실수) | float[]    | 0.0F     |
|                 | double[]   | 0.0      |
| 기본 타입(논리) | boolean[]  | false    |
| 참조 타입       | 클래스     | null     |
|                 | 인터페이스 | null     |



배열이 생성되고 나서 특정 인덱스 위치에 새로운 값을 저장할 때에는 대입 연산자를 사용함  

`변수[인덱스] = 값`



(예시)

```java
package sec02.exam03;

public class ArrayCreateByNewExample {

	public static void main(String[] args) {
		int[] arr1 = new int[3];
		for (int i=0; i<arr1.length; i++) {
			System.out.println("arr1[" + i + "] : " + arr1[i]);
		}
		arr1[0] = 10;
		arr1[1] = 20;
		arr1[2] = 30;
		for (int i=0; i<arr1.length; i++) {
			System.out.println("arr1[" + i + "] : " + arr1[i]);
		}
		System.out.println();
		
		double[] arr2 = new double[3];
		for(int i=0; i<arr2.length; i++) {
			System.out.println("arr2[" + i + "] : " + arr2[i]);
		}
		arr2[0] = 0.1;
		arr2[1] = 0.2;
		arr2[2] = 0.3;
		for(int i=0; i<arr2.length; i++) {
			System.out.println("arr2[" + i + "] : " + arr2[i]);
		}
		System.out.println();
		
		String[] arr3 = new String[3];
		for (int i=0; i<arr3.length; i++) {
			System.out.println("arr3[" + i + "] : " + arr3[i]);
		}
		arr3[0] = "1월";
		arr3[1] = "2월";
		arr3[2] = "3월";
		for (int i=0; i<arr3.length; i++) {
			System.out.println("arr3[" + i + "] : " + arr3[i]);
		}
		System.out.println();
	}

}
```



### 05-2-4. 배열 길이

###### 배열 길이  

배열에 저장할 수 있는 전체 항목의 개수

코드에서 배열의 길이를 얻으려면 배열 객체의 length 필드를 읽으면 됨 (필드 : 객체 내부의 데이터)

*(중요!)* `배열 변수.length;`

*length 필드는 읽기 전용 필드이기 때문에 값을 바꾸는 데에는 사용할 수 없음*



### 05-2-5. 명령 라인 입력

main() 메소드의 매개값인 String[] args는 왜 필요한 것인가?  

`public static void main(String[] args) {...}`

명령 프롬포트에서 위 코드를 java 명령어로 수행하면 JVM은 길이가 0인 String 배열을 먼저 생성하고 main() 메소드를 호출할 때 매개값으로 전달함  

```java
String[] args = {}; // main() 메소드 호출 시 매개값으로 전달

public static void main(String[] args) {
  ...
}
```



아래와 같이 문자열 목록을 주고 실행하면, 문자열 목록으로 구성된 String[] 배열이 생성되고 main() 메소드를 호출할 때 매개값으로 전달됨  

`[JDK 11 이후 버전] java -p . -m 모듈명/패키지.클래스 문자열0 문자열1 문자열2 ... 문자열n-1`

`[JDK 8 이전 버전] java 패키지.클래스 문자열0 문자열1 문자열2 ... 문자열n-1`



```java
String[] args = {문자열0, 문자열1, 문자열2, ..., 문자열n-1}; // main() 메소드 호출시 전달

public static void main(String[] args) {
  ...
}
```

main() 메소드는 String[] args 매개 변수를 통해서 명령 라인에서 입력된 데이터의 수(배열의 길이)와 입력된 데이터(배열의 항목 값)를 알 수 있게 됨  



(예시)

```java
package sec02.exam05;

public class MainStringArrayArgument {

	public static void main(String[] args) {
		if(args.length != 2) {
			System.out.println("값의 수가 부족합니다.");
			System.exit(0); // 프로그램 강제 종료 
		}
		
		String strNum1 = args[0];
		String strNum2 = args[1];
		
		int num1 = Integer.parseInt(strNum1);
		int num2 = Integer.parseInt(strNum2);
		
		int result = num1 + num2;
		System.out.println(num1 + " + " + num2 + " = " + result);
	}

}
```

위의 예제를 그냥 실행하면 "값의 수가 부족합니다."가 출력됨  



- 이클립스에서 프로그램을 실행할 때 매개값을 주는 방법  
  1. Run - Run Configurations
  2. Main 탭에서 Project와 Main Class를 확인
  3. Arguments 탭에서 Program arguments 입력란에 공백으로 구분한 배열의 항목 값을 입력한 후 Apply 클릭
  4. Run 아이콘 클릭



매개값을 주고 실행할 경우의 출력 결과는 "10 + 20 = 30"



### 05-2-6. 다차원 배열

###### 2차원 배열

값들이 행과 열로서 구성된 배열

가로 인덱스와 세로 인덱스를 사용함  



자바는 2차원 배열을 중첩 배열 방식으로 구현함  

- 2 x 3 행렬의 구조

|      | 열0   | 열1   | 열2   |
| ---- | ----- | ----- | ----- |
| 행0  | (0,0) | (0,1) | (0,2) |
| 행1  | (1,0) | (1,1) | (1,2) |



`int[][] scores = new int[2][3]`

위 코드는 메모리에 다음과 같은 3개의 배열 객체를 생성함  

| 스택 영역 | 힙 영역                             |
| --------- | ----------------------------------- |
| scores    | int 타입 배열 A, length는 2 (0,1)   |
|           | int 타입 배열 B, length는 3 (0,1,2) |
|           | int 타입 배열 C, length는 3 (0,1,2) |

배열 변수인 scores는 길이가 2인 배열 A를 참조함  

배열 A의 scores[0]은 다시 길이가 3인 배열 B를 참조하며, scores[1]은 길이가 3인 배열 C를 참조함  



자바는 1차원 배열이 서로 연결된 구조로 다차원 배열을 구현하기 때문에 수학 행렬 구조가 아닌 계단식 구조를 가질 수 있음   

```java
int[][] scores = new int[2][];
scores[0] = new int[2];
scores[1] = new int[3];
```

위 코드는 메모리에 다음과 같이 배열 객체를 생성함

| 스택 영역 | 힙 영역                             |
| --------- | ----------------------------------- |
| scores    | int 타입 배열 A, length는 2 (0,1)   |
|           | int 타입 배열 B, length는 2 (0,1)   |
|           | int 타입 배열 C, length는 3 (0,1,2) |



그룹화된 값 목록을 가지고 있는 경우, 중괄호 안에 다시 중괄호를 사용해서 값 목록을 나열함

`타입[][] 변수 = { {값1, 값2, ...}, {값1, 값2, ...}, ... };`

(예시)

```java
int[][] scores = { {95, 80}, {92, 96} };

int score1 = scores[0][0]; // 95
int score2 = scores[1][1]; // 96 
```



(예시) 배열 속의 배열

```java
package sec02.exam06;

public class ArrayInArrayExample {

	public static void main(String[] args) {
		int[][] mathScores = new int[2][3];
		for(int i=0; i<mathScores.length; i++) {
			for(int j=0; j<mathScores[i].length; j++) {
				System.out.println("mathScores[" + i + "][" + j + "] = " + mathScores[i][j]);
			}
		}
		System.out.println();
		
		int[][] englishScores = new int[2][];
		englishScores[0] = new int[2];
		englishScores[1] = new int[3];
		for(int i=0; i<englishScores.length; i++) {
			for(int j=0; j<englishScores[i].length; j++) {
				System.out.println("englishScores[" + i + "][" + j + "] = " + englishScores[i][j]);
			}
		}
		System.out.println();
		
		int[][] javaScores = {{95, 80}, {92, 96, 80}};
		for(int i=0; i<javaScores.length; i++) {
			for(int j=0; j<javaScores[i].length; j++) {
				System.out.println("javaScores[" + i + "][" + j + "] = " + javaScores[i][j]);
			}
		}
	}

}
```



### 05-2-7. 객체를 참조하는 배열

기본 타입 배열은 각 항목에 직접 값을 갖고 있지만, 참조 타입 배열은 각 항목에 객체의 번지를 가지고 있음  

String은 클래스이므로 String[] 배열은 각 항목에 문자열이 아닌 String 객체의 번지를 가지고 있음  

즉, String[] 배열은 String 객체를 참조하게 됨  



(예시)

```java
package sec02.exam07;

public class ArrayReferenceObjectExample {

	public static void main(String[] args) {
		String[] strArray = new String[3];
		strArray[0] = "Java";
		strArray[1] = "Java";
		strArray[2] = new String("Java");
		
		System.out.println(strArray[0] == strArray[1]); // true
		System.out.println(strArray[0] == strArray[2]); // false
		System.out.println(strArray[0].equals(strArray[1])); // true
		System.out.println(strArray[0].equals(strArray[2])); // true
	}

}
```



### 05-2-8. 배열 복사

배열은 한 번 생성하면 크기를 변경할 수 없기 때문에 더 많은 저장 공간이 필요하다면 더 큰 배열을 새로 만들고 이전 배열로부터 항목 값들을 복사해야 함  



- 배열 간의 항목 값들을 복사하는 방법
  1. for문 사용하기
  2. System.arraycopy() 메소드 사용하기



1. for문으로 배열 복사

(예시)

```java
package sec02.exam08;

public class ArrayCopyByForExample {

	public static void main(String[] args) {
		int[] oldArray = {1, 2, 3};
		int[] newArray = new int[5];
		
		for(int i=0; i<oldArray.length; i++) {
			newArray[i] = oldArray[i];
		}
		
		for(int i=0; i<newArray.length; i++) {
			System.out.println(newArray[i]);
		}

	}

} // 실행 결과 : 1 2 3 0 0
```



2. System.arraycopy() 메소드를 이용해서 배열 복사

`System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)`

- src 매개값 : 원본 배열
- srcPos : 원본 배열에서 복사할 항목의 시작 인덱스
- dest 매개값 : 새 배열
- destPos : 새 배열에서 붙여넣을 시작 인덱스
- length : 복사할 개수

(예시)

```java
package sec02.exam09;

public class ArrayCopyExample {

	public static void main(String[] args) {
		String[] oldArray = {"java", "array", "copy"};
		String[] newArray = new String[5];
		
		System.arraycopy(oldArray, 0, newArray, 0, oldArray.length);
		
		for(int i=0; i<newArray.length; i++) {
			System.out.println(newArray[i]);
		}
	}

} // 실행 결과 : java array copy null null
```



### 05-2-9. 향상된 for문

자바는 배열이나 컬렉션을 좀 더 쉽게 처리하기 위해 향상된 for문을 제공함  

for문의 괄호()에는 배열에서 꺼낸 항목을 저장할 변수 선언과 콜론(:) 그리고 배열을 나란히 작성함  

배열 및 컬렉션 항목의 개수만큼 반복하고, 자동으로 for문을 빠져나감  



- 향상된 for문을 작성하는 형식과 실행 흐름

```java
for (② 타입 변수 : ① 배열){
  
  ③ 실행문;
  
}
```

1. for문이 처음 실행될 때 ① 배열에서 가져올 첫 번째 값이 존재하는지 평가한다.
2. 가져올 값이 존재하면 해당 값을 ② 변수에 저장한다.
3. ③ 실행문을 실행한다.
4. 블록 내부의 실행문이 모두 실행되면 다시 루프를 돌아 ① 배열에서 가져올 다음 값이 존재하는지 평가한다.
5. 만약 다음 항목이 존재하면 ② -> ③ -> ① 순서로 루프를 다시 진행하고, 가져올 다음 항목이 없으면 for문이 종료된다.

*for문의 반복 횟수는 배열의 항목 수!*



(예시)

```java
package sec02.exam10;

public class AdvancedForExample {

	public static void main(String[] args) {
		int[] scores = {95, 71, 84, 93, 87};
		
		int sum = 0;
		for(int score : scores) {
			sum += score;
		}
		System.out.println("점수 총합 = " + sum); // 점수 총합 = 430
		
		double avg = (double) sum / scores.length;
		System.out.println("점수 평균 = " + avg);
	} // 점수 평균 = 86.0

}
```





