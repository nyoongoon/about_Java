# about_Java
Java를 공부하며 알게 된 것을 기록하는 저장소입니다.


# ArrayList VS LinkedList 

<img width="1069" alt="스크린샷 2022-07-13 오전 9 20 13" src="https://user-images.githubusercontent.com/68639744/178623357-ace870bb-3fd9-4d53-9e6d-1189a8d166ce.png">

- java에서 기본형 또는 인스턴스를 저장하기 위해 보통 배열을 사용.
- 하지만 배열의 초기길이를 지정해야 하며, 생성된 배열의 길이는 동적으로 변경할 수 없음.
- 이에 대한 대안으로 List인터페이스를 구현한 ArrayList와 LinkedList를 사용.
### 동기화 이슈
- List는 Thread-safe를 개발자가 고려해야하며 필요하다면 아래와 같이 Collections 클래스를 통해 동기화 제공하는 List 생성 가능.
```java
Collections.synchronizedList(List\<T\> list);
```

## ArrayList
<img width="257" alt="image" src="https://user-images.githubusercontent.com/68639744/178623507-2aa3a3c2-3499-4a01-9d40-05997a840334.png">

- 내부적으로 데이터를 배열에서 관리하며 데이터의 추가, 삭제를 위해 임시 배열을 생성해 데이터를 복사.
- -> 대량의 데이터 추가/삭제 하는 경우에는 데이터 복사가 많이 일어나게 되어 성능저하. 최악 O(n)
- -> 반면 각 데이터 인덱스 가지므로 한번에 참조가 가능해 데이터 검색에 유리 O(1)

## LinkedList
<img width="496" alt="image" src="https://user-images.githubusercontent.com/68639744/178623624-4ca503c5-858b-4253-8a0f-fece21b45608.png">

- 데이터를 저장하는 각 노드가 이전 노드와 다음 노드의 상태만 알고 있음.
- -> 데이터 복사가 없어 데이터의 추가, 삭제에 유리 O(1)
- -> 데이터 검색시 처음부터 순회해야하므로 성능상 불리. 최악 O(n)
- 또다른 단점은 데이터가 메모리에 산재해 저장되기 때문에 참조자를 위한 추가적 메모리 할당이 필요.
<br/><br/><br/><br/><br/>


# HashSet VS HashTable
- https://d2.naver.com/helloworld/831311


<br/><br/><br/><br/><br/>


# String

- 자바의 문자열은 String 클래스의 인스턴스로 관리 됨. 소스 상에서 문자열 리터럴(데이터 값)은 String 객체로 자동 생성되지만, String 클래스의 생성자를 이용해서 직접 String객체를 생성할 수도 있다. 

### split() vs StringTokenizer
: 문자열이 특정 구분자(delimiter)로 연결되어 있을 경우, 구분자를 기준으로 부분 문자열을 분리하기 위해서는 String의 split() 메소드를 이용하거나, java.util 패키지의 StringTokenizer 클래스를 이용할 수 있다. split()은 정규 표현식으로 구분하고, StringTokenizer는 문자로 구분한다. 

``` java
String[] result = "문자열".split("정규표현식");
```

- split() 함수는 문자열 배열을 리턴한다.

```java
StringTokenizer st = new StringTOkenizer("문자열", "구분자");
```
- 구분자를 생각하면 공백이 기본 구분자가 된다. 
- 메소드들을 이용해서 전체 토큰 수, 남아 있는 토큰 여부, 토큰을 읽기

```java
String text = "홍길동/이수홍/박연수";

// 방법 1. 전체 토큰 수를 얻어 for 문으로 루핑
StringTokenizer st = new StringTokenizer(text, "/");
int countTokens = st.countTokens(); //토큰 수 얻기
for(int i = 0; i<countTokens; i++){
	String token = st.nextToken(); //토큰 하나 꺼내오면 st에 해당 토큰 사라짐.
	System.out.println(token);
}

// 방법 2. 남아 있는 토큰을 확인하고 while문으로 루핑
st = new StringTokenizer(text, "/"); //위의 st는 다 사용했기 때문에 새로 생성
while(st.hasMoreTokens()){
	String token = st.nextToken();
	System.out.println(token);
}
```

<br><br><br/><br/><br/>

# StringBuffer, StringBuilder
- String은 문자열이 변경되면 새로운 객체를 생성하기 때문에 성능이 낮아짐.
- 문자열 변경 작업이 많을 경우엔 StringBuffer나 StringBuilder 클래스를 사용.
- 두 클래스는 내부 버퍼에 문자열을 저장해두고, 그 안에서 추가, 수정, 삭제 작업을 할 수 있도록 설계되어 있음.
- StringBuffer는 동기화 적용되어 스레드에 안전.
- StringBuilder는 동기화 x. 단일 스레드환경에서만 사용해야함.
<br/><br/><br/><br/><br/>


# 캡슐화

캡슐화란?

캡슐화(encapsulation)는 객체 지향 프로그래밍에서 다음 2가지 측면이 있습니다.
객체의 속성(data fields)과 행위(메서드, methods)를 하나로 묶는다.
실제 구현 내용 일부를 외부에 감추어 은닉한다.

* * * 
* * * 
* * * 




# Part 01 - Java 기초
# 코딩테스트 유형 (simple)
## 1. 정렬
- 정렬 문제 단독으로 나오는 경우 거의 없음.
- 풀이를 위한 사전 과정. 
- 버블, 선택, 퀵, 합병, 우선순위 큐 ...

## 2. 탐색
- 주어진 데이터에서 특정 값 찾기 (2차원/3차원 데이터에서 인접한 /가능한 경로 찾기)
- 단순 풀이로 접근 시 대부분 시간초과로 실패
- 완전, 이진, 투 포인터, BFS, DFS ...

## 3. 부분 문제의 합 - 분할정복/DP 
- 최대 값 찾기 / 부분 수열의 최대 길이 / 0-1Knapsack 문제 ...
- 단순 반복, 조건문 나열로는 풀기 복잡한 문제
- 해귀함수를 통한 작은 문제의 반복적 해결 구조 또는 계산 결과의 재사용
- 분할정복 , DP

## 4. 최적선택 - 그리디
- Activity Selection / 거스름돈
- 특정 조건 만족 시 빠르게 문제를 해결할 수 있는 방법
- 최적해가 아닌 근사치를 얻을 수도 있으므로 사용 시 주의 필요
- 그리디 

## 5. 기타 시뮬레이션
- 조건에 따른 문자열 입력/삭제/수정 문제
- 문제의 요구사항을 잘 읽고 해결하는 문제
- 특정 알고리즘 분류로 매핑되지 않는 경우 많음 


# 3-3 학습환경 구성 - Tool 사용
- 디버깅 사용방법 
- 중단점, 
- Step over: 한줄 씩 이동. 함수를 타고 들어가진 않음. 
- Step Into: 하위구조를 타고 들어감. 
- Step Out: 들어왔던 하위구조를 나감 

# 자바
## 자바 프로그램 작성 실행 과정
- 자바소스코드 - 자바컴파일러 - 바이트 코드 - jvm - 실행
# 변수와 자료형
- 변수 : 데이터를 저장하는 메모리 공간에 붙여준 이름
# 자료형
## 숫자형
- 정수 / 실수 / 2진수, 8진수, 16진수
```java
//2진수 0b~
int numBase2 = 0b1100;
System.out.println("0b" + Integer.toBinaryString(numBase2)); //2진수로출력
//8진수 0~
int numBase8 = 014;
System.out.println("0" + Integer.toOctalString(numBase8));//8진수로출력
//16진수 0x~
int numBase16 = 0xC;
System.out.println("0b" + Integer.toHexString(numBase16));//16진수로출력
```

- 실수
```java
float floatNum = 1.23f; //뒤에 f 붙이기
double doubleNum = 1.23;
```

## 문자열
- equals(), indexOf(), replace(), substring(), toUpperCase()
```java
String s3 = "Hi";
String s4 = "Hi";
String s5 = new String("Hi");
System.out.println(s3.equals(s4)); //true
System.out.println(s3 == s4); //true
System.out.println(s3.equals(s5)); //true
System.out.println(s3 == s5); // false
```

## 자료형: StringBuffer
- 문자열을 자주 추가하거나 변경할 때 사용하는 자료형
- 문자열은 데이터가 변경될 때마다 객체가 변하지만, StringBuffer는 객체 안에서 변경됨 ..?
```java
StringBuffer sb1 = new StringBuffer("HelloWorld!"); 
sb1.append("1234"); 
```
- append(), insert(), substring()

## 자료형 : 배열
## 자료형 : 리스트
- add(), get(), size(), remove(), clear(), sort(), contains()
```java 
ArrayList l1 = new ArrayList(); //아무 자료형이나 넣을 수 있었네..??
l1.add(1);
l1.add("hello");
l1.add("world!");
System.out.println("l1 == " + l1); // l1 = [1, "hello", "world!"]

l1.add(0, 1); // (index, element)
System.out.println("l1 == " + l1); // l1 = [1, 1, "hello", "world!"]->추가됨

//remove
l1.remove(0); // 인덱스 0번 지우기
l1.remove(Integer.valueOf(2)); // int 2 값 찾아서 지우기 

//clear
l1.clear() // 모든 데이터 지우기 

//sort
l1.sort(Comparator.naturalOrder()); //오름차순
l1.sort(Comparator.reverseOrder()); //내림차순

//contains(element) //데이터 존재 유무 true || false 
```
## 자료형 : 맵
- put(), get(), size(), remove(), containsKey()
```java
map.remove("key") // 값 있었으면 출력 || 없었으면 null 출력 
```
## 자료형 : 제네릭스
- 자료형을 명시적으로 지정
- 제한적일 수 있지만 안정성을 높여주고 형변환을 줄여줌. 
- ArrayList, Map 등 제네릭 사용안하면 하나의 자료구조에 다양한 타입 저장가능. 


# 연산자
- 단항 연산자, 이항 연산자, 삼항 연산자.
- 대입 연산자
- 부호 연산자
- 산술연산자
- 증가/감소 연산자 
- 관계 연산자
- 논리 연산자 
- 복합 대입 연산자 

## 2진법 비트연산자
- 2의 보수 : 2의 제곱수에서 뺴서 얻은 이진수 
- 자리 올림이 필요한 만큼의 수. 
- ex)2진수 3의 2의 보수 : 11 -> 01 
- => 11에서 자리올림(100)이 되려먼 01을 더해야함.
- 2의 보수로 음수 표현을 하기도 함 (자릿수를 올려서 0 비트로 만들기)

## 비트연산자
- 기본연산자 -> && , || 
- 비트연산자 -> & , | 
- & : 두 개의 비트가 모두 1인경우에만 1
- | : 두 개의 비트값 중 하나라도 1이면 1
- ^ (XOR 연산자) : 같으면 0 다르면 1 
- ~ (반전연산자) : 0을 1으로, 1을 0으로 
 
``` java
int num1 = 5;
result = ~num1;
System.out.println("result = " + result); // -6
System.out.printf("%04d\n", Integer.parseInt(Integer.toBinaryString(num1)));
// => 0101
System.out.printf("%s\n", Integer.parseInt(Integer.toBinaryString(result)));
// => (앞에 1 28개)1010 ==> 32비트에 나머지 앞의 자리가 1(부호)로 전부 바뀌었음 
```
- 비트이동연산자 (\<\<, \>\>, \>\>\>)
- \<\< :비트를 왼쪽으로 이동 
- 3\<\<1  =>  0011 => 0110 (\*2의 효과)
- \>\> : 비트를 오른쪽으로 이동
- 3\>\>1 => 0011 => 0001  (/2의 효과)
- \>\>\> : 연산자 
- 비트를 오른쪽으로 이동(부호비트 상관없이 0으로 채움) 
```java
numA = -5;
result = numA >> 1;
System.out.printf("%s\n", Integer.toBinaryString(numA));
// => (1이 28개) 1011
System.out.printf("%s\n", Integer.toBinaryString(result));
// => (1이 28개) 1101 (부호연산 그대로)
result = numA >>> 1;
System.out.printf("%s\n", Integer.toBinaryString(result));
// => (0하나) (1이 27개)1101 (부호연산 0으로)
```

# 조건문 
## if, case

## for, while

# 다차원 배열

# 클래스와 객체 1
- 객체를 정의하는 설계도. 
## 객체(Object)
- 실체
## 인스턴스
- 클래스와 객체의 관계
- 클래스로부터 객체를 선언. 
- 어떤 객체는 어떤 클래스의 인스턴스. 
## this, this()
- this => 객체 자신을 의미
- this() => 생성자


# 클래스와 객체 2
## 오버로딩
- 한 클래스 내에서 같은 이름의 메소드를 여러 개 정의
### 오버로딩의 조건
- 메소드의 이름이 같아야함
- 매개변수의 개수 또는 타입이 달라야함. 
- 리턴타입의 차이만으로 오버로딩되지 않음. 
## 접근제어자
- 클래스의 변수나 메소드의 접근에 제한을 두는 키워드
### 접근제어자 종류
- private : 해당 클래스에서만 접근 가능
- public : 어디서든 접근 가능
- default : 해당 패키지 내에서만 접근 가능
- protected: 해당 패키지 및 상속받은 클래스에서 접근 가능. 

public class KBBank implements Bank{

	@Override
	public void withDraw(int price) {
		System.out.print("KB은행만의 인출 로직...");
		if(price < Bank.MAX_INTEGER){
			System.out.println(price+" 원을 인출한다.");	
		}else{
			System.out.println(price+" 원을 인출실패.");	
		}
	}

	@Override
	public void deposit(int price) {
		System.out.println("KB은행만의 입금 로직..."+price+" 원을 입금한다.");
	
	}

}
