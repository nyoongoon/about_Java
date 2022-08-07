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

# 접근제어자
자바에는 변수와 함수, 클래스에 대한 접근을 제한하는 문법이 있습니다. 접근을 제한하는 이유는 객체가 가진 고유의 멤버 변수값들이 외부에서 잘못 변경되는 것을 막기 위해서입니다. 사전에 멤버 변수와 함수들의 성격을 규정하고 차단함으로써 의도치 않은 실수를 줄이기 위한 의도가 깔려 있습니다. 총4가지가 있는데 public 과 private 를 가장 많이 사용합니다.


# 상속
자바에는 상속(Inheritance)이라는 개념이 존재합니다.

쉽게 말해 부모 클래스(상위 클래스)와 자식 클래스(하위 클래스)가 있으며, 자식 클래스는 부모 클래스를 선택해서, 그 부모의 멤버를 상속받아 그대로 쓸 수 있게 됩니다.

상속을 하는 이유는 간단합니다. 이미 마련되어 있던 클래스를 재사용해서 만들 수 있기 때문에 효율적이고, 개발 시간을 줄여주게 됩니다.

상속을 하더라도 자식 클래스가 부모의 모든 것들을 물려받는 것은 아닙니다

1. reflection 관련 클래스들

자바 API에는 reflection이라는 패키지가 있다. 이 패키지에 있는 클래스들을 사용하면 JVM에 로딩되어 있는 클래스와 메서드를 정보를 읽어 올 수 있다. 주요 클래스의 종류와 각 클래스에서 제공되는 메서드에는 어떤 것들이 있는지 간단히 알아보자.




* * * 
* * * 
* * * 




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

## Static
- 변수나 메소드의 특성을 바꾸는 키워드
### Static 특징
- 메모리에 한 번만 할당됨
- 즉, Static 변수나 메소드는 공유되는 특성을 가짐
- 객체가 만들어지기 전에(프로그램 시작 시) 클래스 변수, 클래스 메소드가 메모리에 할당되어 있음. 
### Static 클래스 변수
- 해당 클래스의 각 객체들이 값을 공유
### Static 클래스 메소드
- 객체를 생성하지 않아도 호출 가능. 

``` java
class Car{
	static String name = "None";
	String type;
	Car(String name, String type){
		this.name = name;
		this.type = type;
	}
	public void printCarInfo(){
		System.out.println("name: " + name);
		System.out.println("type: " + type);
	}
	public static void getName(){
		System.out.println("Car name: " + name);
	}
}

public class Main{
	public static void main(String[] args){
		Car.getName(); //static은 객체 생성하지 않아도 이미 메모리에 올려져있음.
		Car myCar1 = new Car("a", "sedan");
		Car myCar2 = new Car("b", "suv");
		myCar1.printCarInfo(); //name:b type:sedan
		myCar2.printCarInfo(); //name:b type:suv ==> name은 static이라 공유됨!! 
	}
}
```

# 상속 
- 부모 클래스의 필드와 메소드가 상속 됨
- 생성자, 초기화 블록은 상속되지 않음
- 자식클래스는 하나의 부모 클래스만 상속 가능. 
- private, default 멤버를 자식 클래스에서 접근 불가.
- default의 경우 내부 패키지의 자식 클래스는 가능. 
## super, super()
- super : 부모 클래스와 자식 클래스의 멤버 이름이 같을 때 구분하는 키워드
- super() : 부모 클래스의 생성자 호출 

## 오버라이딩
- 부모클래스의 메소드를 자식클래스에서 재정의
- 메소드 선언부 부모 클래스의 메소드와 동일해야함
- **반환 타입에 한해서**,
- 부모 클래스의 반환타입으로 변환할 수 있는타입으로 변경 가능
- 부모 클래스의 메소드보다 접근제어자를 더 좁은 범위로 변경 불가
- 부모 클래스의 메소드보다 더 큰 범위의 예외 선언 불가 

# 다형성
- 하나의 객체가 여러가지 타입을 가질 수 있는 것 
- 부모클래스 타입의 참소변수로 자식 클래스 인스턴스 참조 
## 타입변환 (업캐스팅, 다운캐스팅)
```java
// 타입 변환 Student extends Person
Person pp1 = null;
Student ss1 = null;

Person pp2 = new Person();
Student ss2 = new Student();
Person pp3 = new Student(); // 업캐스팅(다형성)

pp1 = pp2;
pp1 = ss2;

ss1 = ss2;
// ss1 = pp2; 안됌
// ss1 = pp3; 이대론 안되지만
ss1 = (Student) pp3; // 다운캐스팅 이렇게 하면 가능 (원래 Student였는데 업캐스팅된 상태였음)

```



# 추상 클래스 & 추상 메소드 

```java
abstract class Person{
	abstract void printInfo();
}

class Student extends Person{
	public void printInfo(){
		System.out.println("Student.printInfo");
	}
}

public class Main{
	public static void main(String[] args){
		// 추상 클래스 사용
		// Person p1 = new Person();
		Student s1 = new Student();
		s1.printInfo();

		Person p2 = new Person(){ // 추상클래스 익명클래스를 통해 구현가능
			@Override
			void printInfo(){

			}
		};
	}
}
```

# 인터페이스
- 다중상속처럼 사용할 수 있는 기능
- 추상메소드와 상수만으로 이루어짐. 
```java
접근제어자 interface 인터페이스 이름{
	public static final 타입 상수입름 = 값;
	public abstract 반환타입 메소드이름(매개변수);
}
```

# 내부클래스
## 특징
- 내부 클래스에서 외부 클래스 멤버에 접근 가능
- 외부에서는 내부 클래스 접근 불가
## 종류
- 인스턴스 클래스
- 정적 클래스
- 지역 클래스
- 익명 클래스

### 익명 클래스
- 이름을 가지지 않는 클래스
- 선언과 동시에 객체 생성
- 일회용 클래스
```java
클래스이름 참조변수이름 = new 클래스이름(){
...
};
```

# 입출력
## 콘솔 입력
```java
System.in.read()
InputStreamReader reader = ...
BufferedReader br = ...
Scanner ...
```

- 예시 코드
```java
//System.in
int a = System.in.read() - '0'; //System.in.read()=>하나의 캐릭터 읽음
System.out.println("a = " + a);
System.in.read(new byte[System.in.available()]); // 입력스트림에 남아있는 개수 만큼 바이트만큼 읽어서 소진 (엔터키값 등)

//InputStreamReader
InputStreamReader reader = new InputStreamReader(System.in); //여러 글자 받음
char[] c = new char[3]; //여러 데이터 받기 때문에 그 만큼의 배열 길이 필요
reader.read(c); // 여기서 받음
System.out.println(c); //출력

//BufferedReader
//위의 2개가 합쳐진 개념. 
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String s1 = br.readLine(); // 여기서 받음.
System.out.println("s1 = " + s1);

//Scanner 
Scanner sc = new Scanner(System.in);
System.out.println(sc.next()); // 데이터 하나 받기 => 엔터키 소진 필요
sc.nextLine(); //엔터키 소진 

System.out.println(sc.nextInt()); //정수 값 받기 - 다른타입 에러 

System.out.println(sc.nextLine()); //가장 많이 사용 ! 

```

## 콘솔 출력 
```java
System.out.println(...);
System.out.print(...);
System.out.printf(...);
```
- printf 예시
```java
String s = "자바";
int number = 3;
System.out.println(s+ "는 언어 선호도 " + number +"위 입니다.");
System.out.printf("%는 언어 선호도 %d위 입니다.\n", s, number);

// 서식문자 
// %d 정수형
// %o 8진수
// %x 16진수 
// %f 실수 System.out.printf("%f\n", 5.2f);
// %c 문자
// %s 문자열 

// 여백
System.out.printf("%5d\n", 123); // "  123"
System.out.printf("%-5d\n", 123); // "123  "

// 소숫점 자리수 표현
System.out.printf("%.2f\n", 1.12645f); // 1.13 // 마지막자리 반올림한값 !!
```

# 파일 입출력 
## 파일 입력
- 입출력 방식 중 파일로부터 입력 받는 방법 
```java
FileInputStream ...
BufferedReader ...
```

```java
// 파일 입력
BufferedReader br = new BufferedReader(new FileReader("./memo.txt"));
//String line = br.readLine(); //한줄 씩 읽기 

while(true){
	String line = br.readLine();
	if(line == null){
		break;
	}
	System.out.println(line);
}
br.close();
```

## 파일 출력(파일 쓰기)
- 입출력 방식 중 파일로 출력(쓰기)하는 방법 
```java
FileOutputStream ...
FileWriter ...
PrintWriter ...
```

- 예시
``` java
// 1. 파일(로) 출력(쓰기)
// FileWriter
FileWriter fw = new FileWriter("./memo.txt");
String memo = "헤드 라인\n";
fw.wirte(memo);

memo = "1월 1일 날씨 맑음\n";
fw.write(memo);

fw.close();

//PritWiter 
PrintWriter pw = new PrintWriter("./memo.txt");
memo = "헤드 라인";
pw.println(memo); //ln자동추가
memo = "1월 1일 날씨 맑음";
pw.println(memo); //ln자동추가

pw.close();


// 파일 이어 쓰기
FileWriter fw2 = new FileWriter("./memo.txt", true); //append:  true
memo = "1월 2일 날씨 완전 맑음\n";
fw2.write(memo);
fw2.close();


PrintWriter pw2 = new PrintWriter(new FileWriter("./memo.txt", true));
memo = "1월 3일 날씨 또 맑음!";
pw2.println(memo);
pw2.close();
``` 


# 예외 처리
## 예외 (Exception)
- 정상적이지 않은 Case;
## throw, throws
- throw : 예외를 발생시킴
- throws : 예외를 전가시킴. 
``` java
...func(){
	throw new Exception(); // 발생 !!! // @예외 발생시킴(동사원형)
}
...func() throws Exception{ // 전가 !!! //func()가 @예외 발생시킨다.(3인칭단수)
	...
}
``` 

- 커스텀 예외
```java
//RuntimeException 상속 
class CustomException extends RuntimeException{}
```
- 예시
```java
class NotTenException extends RuntimeException{}

public class Main{
	public static boolean checkTenWithException(int ten){ // 예외 발생 예시 !!!
		try{
			if(ten != 10){
				throw new NotTenException(); //예외 이곳에서 처리 !!!
			}
		}catch(NotTenException e){
			System.out.println("e == " + e); //위의 사항 여기서 잡힙
			return false;
		}
		return true;
	}

	public static boolean checkTenWithThrows(int ten) throws NotTenException{ // 예외 전가 예시 !!!
		if(ten != 10){
			throw new NotTenException(); // 예외가 발생하면 일반 밖으로 보냄
		}
		return true;
	}

	public static void main(String[]args){
		// 예외 발생 예제인 경우 예외가 함수 안에서 처리됨 !!!
		Main.checkTenWithException(9); //false 리턴 //e == NotTenException 출력됨.

		//예외 전가 예제인 경우 예외가 밖으로 나와서 호출한 곳에서 처리 해주어야함 !!!

		try{
			checkTenWithThrows(9);	//false !!!
		}catch(NotTenException e){
			System.out.println("e == " + e); //e == NotTenException 출력됨.
		}
		
	}
}
```

# 컬렉션 프레임워크
- 여러 데이터를 편리하게 관리할 수 있게 만들어 놓은 것.
- 자료구조 및 알고리즘을 구조화
## 대표 인터페이스
- List 인터페이스, Set 인터페이스, Map 인터페이스.  

## List 인터페이스
- 순서가 있는 데이터의 집합
- 데이터 중복 허용
- 대표 구현 클래스 : ArrayList, LinkedList, Vector 

## Set 인터페이스
- 순서가 없는 데이터의 집합
- 데이터의 중복 허용하지 않음
- 대표 구현 클래스 : HashSet, TreeSet 

## Map 인터페이스
- 키와 값의 쌍으로 이루어진 데이터 집합
- 순서 유지하지 않음
- 대표 구현 클래스 : HashMap, TreeMap 

### ArrayList
```java
list.size()
list.contains(value) /// 값의 유무 
list.indexOf(value) // 값의 인덱스
```

### LinkedList
``` java
list.addFirst(value)
list.addLas(value)
list.removeFirst()
list.removeLast()
```

### HashSet
```java
set.add(1);
set.add(2);
set.add(3);
System.out.println(set); // set = [1, 2, 3] //toString()오버라이드 ..?
```

### TreeSet
```java
set.add(10);
set.add(5);
set.add(15);
System.out.println(set); // set = [5, 10, 15] // 정렬되어 출력됨
set.first();
set.last();
set.lower(10); //5
set.higher(10); //15
```

### HashMap
```java
System.out.println(map); // map {1="kiwi", 2="apple", 3="mango"}
```

### TreeMap
```java
map.put(10, "kiwi");
map.put(5, "apple");
map.put(15, "mango");
System.out.println(map); // map = {5=apple, 10=kiwi, 15=mongo} // 정렬되어 출력됨 
System.out.println(map.firstEntry()); // 5=appler
System.out.println(map.firstKey()); // 5
System.out.println(map.lastEntry()); //15=mango
System.out.println(map.lastKey()); // 15
System.out.println(map.lowerEntry(10)); //5=apple
System.out.println(map.higherKey(10)) // 15=mango
```

### 컬렉션 프레임워크 예제 - 로또 번호 만들기
```java
public static void main(String[] args){
	HashSet set = new HashSet();
	for(int i = 0; set.size() < 6; i++){
		int num = (num)(Math.random() * 45) + 1; //Math.random() 
		set.add(num); // 중복되면 사이즈 증가하지 않으므로 분기문없이 for문의 조건문으로 충분함.
	}
	LinkedList list = new LinkedList(set); // set을 그냥 LinkdList에 넣어서 생성했음 !!! 
	Collections.sort(list);

}
```

# 람다식
- 메소드 대신 하나의 식으로 표현하는 것
- 익명 함수
```
public int sum(int x, int y){ // 일반 함수
	return x + y;
}
(int x, int y) -> {return x + y;}
```

## 장점
- 코드 간결
- 코드 가독성 높아짐
- 생산성 높아짐
## 단점
- 재사용 불가능(익명)
- 디버깅 어령무
- 재귀함수로는 맞지 않음 (이름이 없기 때문)

## 람다식 예시
```java
interface ComputeTool{
	public abstarct int compute(int x, int y);

	//public abstarct int compute2(int x, int y); // 추상메소드 2개일 경우에 람다 사용 불가 (기본 익명 클래스는 그냥 오버라이딩하면 가능)
}
public class Main{
	public static void main(String[] args){
		ComputeTool cTool1 = new ComputTool(){ // 기본 익명 클래스
			@Override
			public int compute(int x, int y){
				return x + y;
			}
		};
		System.out.println(cTool.compute(1, 2)); //기본 사용

		// 람다식 !!!
		CoumputTool cTool2 = (x, y) -> { x + y}; // 위의 기본 익명 클래스와 같은 기능 
		System.out.println(cTool2.compute(1, 2)); // 람다 사용. 람다에서 메소드명 지정 안해줘도 인터페이스의 메소드 명을 사용할 수 있음. 
	}
}
```

# 스트림 
- 배열, 컬렉션 등의 데이터를 하나씩 참조하여 처리 가능한 기능
- for문의 사용을 중려 코드를 간결하게 함.
- 크게 3가지로 구성
- Stream 생성
- 중개 연산
- 최종 연산
- 데이터소스 객체.Stream생성().중개연산().최종연산();
## 스트림 생성
- 배열 스트림
```java
String[] arr = new String[]{"a", "b", "c"}
Stream stream = Array.Stream(arr);
```
- 컬렉션 스트림 
```java
ArrayList list = new ArrayList(Arrays.asList(1,2,3));
Stream stream = list.stream();
```
## 스트림 중개연상
- Filtering
- filter 내부 조건에 참인 요소들을 추출 
```java
IntStream intStream = IntStream.range(1, 10).filter(n->n%2==0);
```
- Mapping
- map 안의 연산을 요소별로 수행 
```java
IntStream intStream = IntStream.range(1,10).map(n -> n+1);
```

## 스트림 최종연산
- Sum, Average
```java
IntStream.range(1, 5).sum()
IntStream.range(1, 5).average().getAsDouble()
```
- min, max
```java
IntStream.range(1, 5).min().getAsInt();
IntStream.range(1, 5).max().getAsInt();
```

## 예제
- 스트림 생성 예시
```java
// 배열 스트림
Stream stream1 = Arrays.stream(arr);
stream1.forEach(System.out::println);

// 컬렉션 스트림
Stream stream2 = list1.stream();
        //stream2.forEach(System.out::println); -> 스트림 최종 연산 이후에 더 작업할 수 없음 !
stream2.forEach(num -> System.out.println("num = " + num));

// 스트림 builder
Stream StreamBuilder = Stream.builder().add(1).add(2).add(3).build();
streamBuilder.forEach(System.out::println);

// 스트림 generate
Stream streamGenerator = Stream.generate(()->"abc").limit(3); // 3번반복
streaGenerator.forEach(System.out::println);

// 스트림 iterate
Stream streamIterate = Stream.iterate(10, n -> n * 2).limit(3);
streamIterate.forEach(System.out::println);

// 기본타입 스트림
IntStream intStream = IntStream.ranget(1, 5);
intStream.forEach(System.out::println);
```
- 스트림 중개 연산 예시
```java
// Filtering(필터링)
IntStream intSteam2 = IntStream.range(1, 10).filter(n -> n % 2 == 0); //참인경우찾기
intStream2.forEach(System.out::println);

// Mapping(매핑)
IntSrteam intStream3 = IntStream.range(1, 10).map(n -> n+1); // 연산위주
intStream3.forEach(n -> System.out.print(n + " "));
System.out.println();

// Sorting
IntSream intStream4 = IntStream.builder().add(5).add(1).add(3).add(4).add(2).build();
IntSream intStreamSort = intStream4.sorted(); // 정렬
intStreamSort.forEach(System.out::println);
```

- 스트림 최종 연산 예시
```java
// Sum, Average
int sum = IntSream.range(1, 5).sum();
double average = IntStream.range(1, 5).average().getAsDouble();

// Min, Max
int min = IntStream.ranget(1, 5).min().getAsInt();
int max = IntStream.ranget(1, 5).max().getAsInt();

// reduce
Stream<Integer> stream3 = new ArrayList<Integer>(Arrays.asList(1,2,3,4,5));
stream3.reduce((x,y)->x+y).get(); // 연쇄적인 연산 => 1+2. 3+3. 6+4. 10+5.

// forEach
IntSream.range(1, 10).filter(n -> n ==5 ).forEach(System.out::println);
```
- 예제
```java
// 예제: 1~10 숫자 중 짝수 들의 합
int sum2 = IntStream.range(1, 11).filter(x -> x % 2 == 0).sum();
```



# 기초 수학

- 집합
- 경우의 수
- 순열 / 조합
- 점화식과 재귀함수
- 지수와 로그
- 알고리즘 복잡도 



# 집합
- 컬렉션 프레임워크 이용한 구현
- 직접 구현

## 집합의 개념
- 집합(Set)
- 특정 조건에 맞는 원소들의 모임
### 집합 표현 방법
- 원소 나열법 => A={1,2,3}, B={2,4,6}
- 조건 제시법 => A={A|A는 정수, 1<=A<=3}, B={2B|B는 정수, 1<=B<=3}
- 벤다이어 그램
#### 교집합
- 두 집합이 공통으로 포함하는 원소로 이루어진 집합
#### 합집합
- 어느 하나에라도 속하는 원소들을 모두 모은 집합
#### 차집합
- A(orB)에만 속하는 원소들의 집합
#### 여집합
- 전체집합(U) 중 A의 원소가 아닌 것들의 집합
## 집합 사용 예시 코드
```java
//1. 자바에서 집합사용 - HashSet
//2. 집합 연산
//2-1. 교집합
HashSet a = new HashSet(Arrays.asList(1,2,3,4,5));
HashSet b = new HashSet(Arrays.asList(2,4,6,8,10));
a.retainAll(b);// a교집합 b //[2, 4]
//2-2. 합집합
a.addAll(b); //a합집합 b[1,2,3,4,5,6,8,10]
//2-3 차집합
a.removeAll(b); //a차집합b[1,3,5]
```

# 경우의 수
- 합의 법칙, 곱의 법칙을 구분하기
- 경우의 수를 자바 프로그래밍으로 구현하기 
## 경우의 수 개념
- 어떤 사건에서 일어날 수 있는 경우의 가짓수
```
예시1) 동전을 던지는 사건 : 경우의 수 2
예시2) 주사위를 던지는 사건 : 경우의 수 6
- 사건 A가 일어날 경우의 수 : n(A)
```

## 합의 법칙 곱의 법칙
- 주사위 예시 경우의 수
- 최대공약수, 최소공배수
- 최소공배수공식) lcm = numA * numB /gcd;

### 합의 법칙 개념
- 사건 A 또는 사건 B가 일어날 경우
- 사건 A와 사건 B의 합의 법칙 : n(A ∪ B)
- n(A ∪ B) = n(A) + n(B) - n(A∩B)
```
예시) 두 개의 주사위를 던졌을 때 합이 3 또는 4의 배수일 경우의 수
```

### 곱의 법칙 개념
- 사건 A와 사건 B가 동시에 일어날 경우의 수
- 사건 A와 사건 B의 곱의 법칙: n(A x B)
- n(A x B) = n(A) x n(B)
```
예시) 두 개의 주사위 a, b를 던졌을 때 a는 3의 배수, b는 4의 배수인 경우의 수 
```


# 순열 / 조합
- 팩토리얼 (반복문, Stream)
- m개 숫자를 이용 n자리 자연수

## 순열
- 1. 팩토리얼
- 2. 순열
- 3. 중복 순열
- 4. 원 순열

### 팩토리얼
- 1에서 n까지 모든 자연수의 곱(n!)

### 순열(Permutation)
- 순서를 정해서 나열
- 서로 다른 n개 중에 r개를 선택하는 경우의 수 (순서 O, 중복 X)
- 예시) 5명을 3줄로 세우는 방법
- 예시) 서로 다른 4명 중 반장, 부반장 뽑는 방법. 
- n! / (n-r)! ==> n부터 n-r+1까지의 곱.!!!

### 중복 순열
- 서로 다른 n개 중에 r개를 선택하는 경우의 수 (순서O, 중복 O)
- 예시) 서로 다른 4개의 수 중 2개를 뽑는 방법(중복 허용)
- 예시) 후보 2명, 유권자 3명일 때 기명 투표 방법. 
- n^r

### 원순열
- 원 모양의 테이블에 n개의 원소를 나열하는 경우의 수
- 예시) 원모양의 테이블에 3명을 앉히는 경우
- n!/n = (n-1)!


## 조합
- 1. 조합
- 2. 중복 조합 
- 조합 개념의 이해와 경우의 수 계산
- 프로그래밍으로 조합의 각 case 출력 

### 조합(의 개념)
- 서로 다른 n개 중에서 r개를 선택하는 경우의 수 (순서X, 중복X)
- 예시) 서로 다른 4명 중 주번 2명을 뽑는 방법 (순열은 반장,부반장, <-> 조합은 주번)
- nCr = n! / (n-r)!r! = nPr / r! (0 < r <= n)

### 중복 조합
- 서로 다른 n개 중에서 r개를 선택하는 경우의 수 (순서X, 중복O)
- 예시) 후보 2명, 유권자 3명일 때 무기명 투표 방법
- nHr = n+r-1 C r

# 점화식과 재귀함수 
- 점화식과 재귀함수 개념 이해
- 점화식 유형을 파악하고 재귀함수로 구현 가능
- 여러가지 점화식을 재귀함수로 구현
- 최대공약수를 재귀함수로 구현

## 점화식(Recurrence)
- 어떤 수열의 일반항을 그 이전의 항들을 이용하여 정의한 식
- 예시) 피보나치 수열. 

## 재귀함수
- 어떤 함수가 자신을 다시 호출하여 작업을 수행하는 방식
```
반환타입 함수이름 (매개변수){
    종료조건
    ...
    함수이름(...)
}
```

# 지수와 로그
- 지수와 로그를 Math 클래스 사용한 구현
- 직접 구현
- 1. 제곱, 제곱근, 지수
- 2. 로그
## 제곱, 제곱근, 지수 개념
- 제곱 : 같은 수를 두 번 곱함
- 거듭 제곱 : 같은 수를 거듭하여(2번 이상) 곱함
- 제곱근 (=root)
- a를 제곱하여 b가 될 때 a를 b의 제곱근이라고 함
```
2^3 = 2 x 2 x 2
4^1/2 = 2^2x1/2 = 2
a^x -> a: 밑, x : 지수
```
- 자바 Math 클래스 활용
```java
// 2^3
Math.pow(2, 3); // 8
Math.pow(2, -3); // 1/2^3 == 1/8
Math.pow(2, 30); // 1.073741824E9 //10의 9승
//루트 16
Math.sqrt(16);	//4
Math.pow(16, 1.0/2); //4

// cf)절대값 구하기
Math.abs(-5) == Math.abs(5)
```

## 로그
- log a b
- a가 b가 되기 위해 제곱해야하는 수
```
log 2 4 = 2
log 10 1000 = 3
log e 2.718281828459... = 1  => (자연상수)
``` 
- 자바 Math 클래스 활용
```java
Math(E); // 자연상수 == 2.718281828459045
Math.log(2.718281828459045); // 1.0
Math.log10(1000); // 3
//log 2 4 계산하기(밑이 다른 로그)
Math.log(4) / Math.log(2) // 2.0  


```

# 알고리즘 복잡도
- 시간복잡도, 공간복잡도 개념 이해
- 빅오 표기법 이해와 코드에 대한 복잡도 산출 가능 
- 시간 복잡도 예시 코드
- 공간 복잡도 예시 코드 

## 복잡도
- 알고리즘 성능을 나타내는 척도
- 시간 복잡도 : 알고리즘의 필요 연산 횟수
- 공간 복잡도 : 알고리즘의 필요 메모리
- 시간 복잡도와 공간 복잡도는 Trade-off 관계 

## 시간 복잡도
- 어떤 분제를 해결하기 위한 알고리즘의 필요 연산 횟수
- 빅오 표기법을 통해 나타냄
- O(1) < O(logN) < O(N) < O(NlogN) < O(N^2) < O(2^n) 
- 상수시간<로그시간 < 선형시간 < 로그선형시간< 이차시간 < 지수시간 

## 공간 복잡도
- 어떤 문제를 해결하기 위한 알고리즘의 필요 메모리 사용량
- 빅오 표기법을 통해 나타냄
- 일반적으로 메모리 사용량 기준은 MB 단위
```java
int[] a = new int[1000]; //4KB
int[][] a = new int[1000][1000]; //4MB
```









