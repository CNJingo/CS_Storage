# Spring

### Spring AOP란 무엇인가?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
![spring-aop-diagram](https://user-images.githubusercontent.com/55564829/176193666-7dfdc8ea-a3a0-41d3-9827-f62a762ca763.jpg)

Spring에서 Aspect Oriented Programming을 가능케 해주는 기능이다. 
Spring AOP를 위해서는 필수적으로 알아야할 개념이 3가지 정도가 존재한다.

Joint point: 에러 핸들링 또는 함수의 실행을 시작할 포인트를 얘기한다. Spring AOP에서는 언제나 함수의 실행이 joint point가 된다. 

Pointcut: 조인포인트와 매칭되는 표현식을 얘기한다. pointcut은 한개 이상의 jointpoint를 담고 있을 수 있다. 
한마디로 어떤 조인포인트에서 함수를 실행시킬지 범위를 뜻한다.

Advice: 포인트 컷에 매칭되는 조인포인트에서 실행되는 것을 얘기한다.

이러한 AOP는 트랜잭션과 같이 자주 중복되는 관심사를 모듈로 빼내어 효과적으로 관리할 수 있을 뿐만 아니라 보일러 플레이트 코드를 줄일 수 있다는 장점이 있다. 

또한 기존의 코드 로직은 변경시키지 않은채 새로운 작업을 추가시킬 수 있어서 기능 확장에 유리하다.

</details>


### filter VS Handler interceptor?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>

두 가지 모두 요청이 Controller로 오기전에 요청으로 가로채서 특정한 작업을 수행한다는 점에서 동일하다. 하지만 두개는 요청을 가로채는 시점이 다르다. filter는 spring mvc와 무관하게 적용될 수 잇다.
   
   ![filters_vs_interceptors-768x287](https://user-images.githubusercontent.com/55564829/176193620-e32cf887-f398-4183-b989-dbaf4927ea95.jpg)

filter는 제일 앞단에서 들어오는 요청과 나가는 응답에 대해서 제어를 하며 handler interceptor는 Dispatcher servlet과 Controller사이에 위치하여 그 사이의 요청들을 제어한다.
   
filter는 모든 요청에 대해서 제일 앞단에서 요청을 관리한다는 점에서 조금 더 범용적인 용도로 사용될 수 있다.  
   
   * 인증
   * 로깅
   * 데이터 압축
에 주로 사용된다.

   반면 Handler interceptor는 spring mvc 안에서 동작하므로 조금 더 application specific한 동작들을 처리하는데 특화되어 있다.
   
   * 애플리케이션 로그
   * 디테일한 유저 권한 체크
   
Filter역시 Spring boot내에서는 bean으로 등록되어 있기 때문에 커스텀이 가능하다.

   Spring security역시 Filter가 추가되어서 앞단에서 유저에 대한 인증을 진행하고 있다.
   
   Spring security는 DelegatingFilterProxy라는 것에 많이 의존하고 있는데 이것은 spring framework에서 제공하는 웹 모듈로  javax.Servlet.Filter interface를 구현한 모든 클래스를 filter chain에 등록하여 스프링이 관리할 수 있는 filter로 바꿔주는 역할을 한다.

</details>

### 싱글톤이란?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>

   디자인 패턴중 하나로서 하나의 애플리케이션에서는 하나의 인스턴스만 존재하게끔 하는 것이다.
   
   공유 자원을 관리할때나 로깅처럼 여러 곳에서 공통적으로 사용되는 서비스를 제공하는데 이점이 있다.
   
   또한 여러개의 요청에 각각의 인스턴스를 생성하는 것은 메모리 낭비가 심하기 때문에 이를 하나의 객체만 생성해놓고 돌려 쓰는 것은 효율적일 수 있다.
   
   스프링은 IOC container에서 하나의 Bean만 생성하여 관리한다. 즉 싱글턴패턴으로 객체를 관리한다.
   
   그럼 스프링은 모두 싱글턴 패턴이냐? 그 것은 아니다. 왜냐하면 애플리케이션 내에서 여러 Spring Container를 사용할 수 있기 때문이다.
   
   <img width="882" alt="스크린샷 2022-07-08 오후 11 24 32" src="https://user-images.githubusercontent.com/55564829/178011507-24595250-b9d0-4fb1-bc93-603492840cfd.png">

   스프링은 어떠한 객체의 인스턴스를 사용할때 컨테이너로 부터 주입받아서 사용한다. 즉 New 키워드를 사용해서 새로운 객체를 생성하지 않는다.
   
   이는 IOC Container에서 관리하는 Bean을 주입받아서 사용하는 것이다. 이때 IOC Continainer가 하나였다면 싱글턴 패턴으로 객체를 사용할 수 있는 것이다.
   
   싱글톤은 Spring에서 default bean scope로 지정하고 있다 bean scope를 바꿔주게 되면 더이상 그 bean은 싱글턴으로 작동하지 않게 된다.
  

</details>

### 템플릿 / 콜백 패턴이란?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
   템플릿 콜백 패턴은 주로 변하지 않는 부분의 보일러 플레이트 코드가 자주 발생할때 사용된다.
   
   예를들면 JDBC를 사용하여 데이터를 다룰때 우리는 JDBC connection의 반환 문제 때문에 try catch finally를 사용하게 된다. 이때 JDBC의 자원을 반환하는 코드는 중복돼서 나타나고
   
   JDBC를 사용해서 데이터를 다루는 SQL부분은 변화하게 된다.
   
   우리는 이런 상황에서 변하지 않는 부분과 변하는 부분을 구분하고 변하지 않는 부분에 대해서 템플릿이라는걸 만들 수 있다.
   
   템플릿은 변하지 않은 부분에 대한 것을 따로 클래스로 분류해내고 변하는 부분은 템플릿 안에 있는 메소드의 파라미터로 전달받아서 사용할 수 있게끔 구조를 변경하는 것이다.
   
   변하는 부분에 대해서는 템플릿을 사용하는 클라이언트 입장에서 메소드를 넘겨야 한다. 하지만 자바는 메소드의 argument로 메소드를 넘길 수 없다.
   
   그래서 여기서 콜백이라는 개념이 등장한다. 콜백 함수는 내가 실행시키는 함수가 아닌 다른 함수에게 실행을 위임할 함수를 얘기한다.
   
   하지만 자바는 기본적으로 함수의 argument로 함수를 넘길 수 없다. 그렇기 때문에 일반적으로는 콜백 함수를 포함하고 있는 오브젝트를 넘긴다.
   
   그렇게 되면 템플릿 메소드는 오브젝트를 파라미터로 넘겨받아 오브젝트의 콜백 함수를 실행시킬 수 있게 된다.
   
   하지만 자바 8 부터는 람다의 도입으로 익명의 클래스와 익명함수를 람다 표현식을 통해 제공할 수 있으므로 코드가 간결해지고 깔끔해지는 효과를 얻을 수 있다.
   
   이렇게 되면 중복되는 코드는 템플릿 클래스를 통해 하나가 되고 변하는 부분에 대해서만 콜백 함수로 넘기면 되므로 기능 확장을 많이 하더라도 코드의 양이 많이 늘어나는 것을 방지할 수 있다.
   
   
   
   
</details>
