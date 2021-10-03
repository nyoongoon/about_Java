# about_Java
Java를 공부하며 알게 된 것을 기록하는 저장소입니다.
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

<br><br>

# StringBuffer, StringBuilder
- String은 문자열이 변경되면 새로운 객체를 생성하기 때문에 성능이 낮아짐.
- 문자열 변경 작업이 많을 경우엔 StringBuffer나 StringBuilder 클래스를 사용.
- 두 클래스는 내부 버퍼에 문자열을 저장해두고, 그 안에서 추가, 수정, 삭제 작업을 할 수 있도록 설계되어 있음.
- StringBuffer는 동기화 적용되어 스레드에 안전.
- StringBuilder는 동기화 x. 단일 스레드환경에서만 사용해야함.

