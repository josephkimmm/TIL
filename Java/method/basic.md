2025.03.09

벌써 학원을 다닌지 3개월이란 시간이 지났지만 Servlet과 JSP 수업을 수강하던중 Java에 대한 기초가 부족하여 
이해하기가 쉽지않다. 앞으로 있을 Spring과 기본기를 다지기 위해 Java에 대한 복습을 하고자 TIL 작성을 시작하게되었다.

먼저 그동안 수업내용과 중간중간 헷갈리는 개념에 대해서 복습하고자 한다.

1.  메서드 호출과 용어 정리

```java
call("hello", 20)
int call(String str, int age)
```

인수(Argument) =  인 + 수
호출하는 쪽에서 "hello", 20 처럼 넘기는 값을 인수 또는 인자 라고 한다.

매개변수(Parameter) =  매개 + 변수
메서드를 정의할 때 선언한 변수인 String str, int age를 매개변수, 파라미터라고 한다.
메서드를 호출할 때 인수를 넘기면 => 매개변수에 대입

2. void와 return의 생략
모든 메서드는 항상 return을 호출해야한다 그런데 반환 타입 void의 경우에는 예외로 printfooter()와 같이 생략해도된다. 
자바 컴파일러가 반환 타입이 없는 경우에는 return을 마지막줄에 넣어준다. 참고로 return을 만나면 해당 메서드는 종료된다.

3. 자바는 항상 변수의 값을 복사해서 대입한다!!===> 대원칙

```java
public class MethodValue {

  public static void main(String[] args) {
    int num1 = 5;
    System.out.println("1. changeNumber 호출 전, num1: ", num1);
    changeNumber(num1);
    System.out.println("4. changeNumber 호출 후, num1: ", num1);
  }

  public static void changeNumber(int num2) {
    System.out.println("2. changeNumber 호출 전, num2: ", num2);
    num2 = num2 * 2;
    System.out.println("3. changeNumebr 호출 후, num2: ", num2);
  }

}
```

```java
//실행결과
1. changeNumber 호출 전, num1: 5
2. changeNumber 호출 후, num1: 5
3. changeNumber 호출 전, num2: 10
4. changeNumber 호출 후, num2: 5
// num2의 변경은 num1에 영향을 주지 않는다. 왜냐하면 값을 복사해서 전달했기 떄문이다.
```

아직 너무나도 부족한 생각이든다. 수료가 2개월도 남지않은 시점이지만 Java+DB+Client+Servlet/JSP+Spring(boot) 까지 해야될 것이 많다...
화이팅
