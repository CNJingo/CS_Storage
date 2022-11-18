# Spring

### Spring AOP란 무엇인가?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
![spring-aop-diagram](https://user-images.githubusercontent.com/55564829/176193666-7dfdc8ea-a3a0-41d3-9827-f62a762ca763.jpg)

   우리는 비즈니스 로직을 짤때 비즈니스로직과 관련있는 부가기능들을 넣어주곤 한다. 예를 들면 트랜잭션 경계설정과 같이 비즈니스 로직과 매우 밀접한 관련이 있지만 분리할 수 있는 코드들이 존재한다.
   
   이러한 코드들은 단순히 하나의 비즈니스로직과 관련있는 것이 아니라 여러 곳에서 쓰이는 경우가 많다. 그렇다면 이러한 중복 코드를 없애면서 비즈니스 로직에 부가적인 기능을 추가적으로 얹는 것이 가능할까? 
   
   가능하다. 프록시 패턴을 사용하여 타깃 오브젝트에 작동하기 전에 앞에서 미리 프록시처럼 동작하여 타깃 오브젝트의 결과값에 부가적인 기능을 더해줘서 사용자에게 전달할 수 있다.
  
   하지만 이렇게 구현할 경우 일일이 타겟 오브젝트의 메소드들을 구현한 인터페이스가 필요하고 여러개의 클래스에게 적용하려면 각각 프록시를 만들어줘야 하는 번거로움이 존재한다.
   
   이를 해결하기 위해 스프링에서 제공해주는 기능을 사용할 수 있다. 일명 DefaultAdvisorAutoProxy이다. 이는 빈 후처리기라고도 불리며 프록시 적용대상인 빈들에 대하여 프록시가 적용된 빈 오브젝트로 대체하여 빈을 등록하게 해준다. 즉 프록시 적용대상인 빈은 컨테이너에 최종적으로 프록시가 적용된 빈을 가지고 있게 된다.
   
   이는 ProxyFactoryBean을 통해서 일일이 빈을 등록하지 않아도 타겟 오브젝트에 자동으로 프록시가 적용될 수 있게끔해준다.
   
Spring AOP를 위해서는 필수적으로 알아야할 개념이 3가지 정도가 존재한다.

Joint point: 에러 핸들링 또는 함수의 실행을 시작할 포인트를 얘기한다. Spring AOP에서는 언제나 함수의 실행이 joint point가 된다. 

Pointcut: 조인포인트와 매칭되는 표현식을 얘기한다. pointcut은 한개 이상의 jointpoint를 담고 있을 수 있다. 
한마디로 어떤 조인포인트에서 함수를 실행시킬지 범위를 뜻한다.

Advice: 포인트 컷에 매칭되는 조인포인트에서 실행되는 것을 얘기한다.
   
Advisor = Pointcut + Advice
   
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

### Exception

<details>
   <summary> 자세히 보기 </summary>

 <br>
   Spring에는 checked exception과 unchecked exception 두개가 존재한다.

   checked exception은 예외처리를 강제하는 exception이다. 주로 chcked exception은 애플리케이션 외의 상황에서 문제가 생기는 exception들을 포함하고 있다.

   예를 들어 파일을 읽으려고 했는데 존재하지 않는 I/O exception이나 db connection을 가져오지 못해서 생기는 SQLException 같은 것들이다.

​	checked exception은 특이한 점이 spring에게 예외처리를 강제한다. 이는 compile time에서 에러가 날 수 있는 상황을 미리 감지하고 throw 구문을 강제한다. 

​	그런데 만약 checked exception이 발생해도 예외를 던지는 것 외에는 할 수 있는게 없다면? 그냥 이것을 런타임 exception으로 포장해서 던지는게 낫다. 왜냐하면 checked exception은 상위 메소드로 에러를 던지기 때문에 계속 throw 구문을 불필요하게 적어줘야 하기 때문이다.

​	만약 checked exception이 발생했을때 예외를 해결하기 위해 시도할 수 있는 방법이 있다면 catch로  exception을 잡아서 해당 처리를 해주는게 좋다. 

   unchecked exception은 런타임 exception을 상속받은 모든 exception이다. 주로 애플리케이션 로직에 에러가 있을때 발생한다. 그렇기 떄문에 이는 런타임시에 발생된다. NullpointException, ArithmeticException과 같은 에러가 있다.

​	이러한 에러에 대해서 예외복구가 불가능한 상황이라면 최대한 에러메시지를 구체화해서 개발자에게 알려주는 것이 좋다. 하지만 이런 생각이 든다. 에러를 throw하고 아무런 처리를 하지 않는다면 프론트 입장에선 예상했던 response entity가 아닌 error를 뱉고 아무런 응답을 주지 않는 서버라면 이를 처리하기가 곤란할 것이다.

​	Spring에서는 이러한 것을 방지하기위해 @ControllerAdvice, @ExceptionHandler와 같은 어노테이션을 제공한다. @ExceptionHandler는 선언되어 있는 클래스 안에서 발생하는 에러들을 잡고 @ControllerAdvice는 모든 컨트롤러에서 발생하는 에러를 잡을 수 있다. throw로 에러를 던지면 이 어노테이션이 선언되어 있는 메소드로 에러가 가는 것이다.

​	그렇게 되면 해당 메소드들에서 에러를 잡아서 에러 메시지를 프로그램에서 정의해놓은 response entity에 실어서 보낼 수 있다. 이러한 로직을 만들게 되면 프론트에서는 항상 같은 response를 받을 수 있다.

​	마지막으로 exception은 주로 구체적이지 않고 범용적인 에러인 경우가 많기 때문에 이러한 경우 조금더 세부적인 내용을 담고 있는 custom한 에러를 선언해줘서 해당 에러를 상속받아서 더 구체적이고 명시적인 에러를 만들어서 뱉는 것이 바람직하다.



</details>


### filter는 스프링 빈으로 어떻게 등록이 가능한가?

<details>
   <summary> 자세히 보기 </summary>
   
   
 <br>
   
   원래 filter는 spring mvc 밖에 존재하면서 dispatcher servlet으로 요청이 들어가기 전에 존재한다. 즉 클라이언트의 요청을 제일 먼저 받는 곳이 필터이다.
   
   그렇기 때문에 원래 filter는 spring bean으로 등록될 수 없다. 하지만 delegatingFilterProxy는 서블릿 필터를 스프링 빈으로 등록 가능케 해준다.
   
   delegatingFilterProxy는 필터 이름을 가져와서 해당 필터 이름을 가진 빈을 spring application context로 부터 가져온다.
   
그렇게 하면 해당 필터를 거치는 요청은 모두 해당 필터를 이름으로 가진 빈에게 가게 되는 것이다.

delegatingFilterProxy는 spring security에서 주요하게 사용하는 기술이다.

이 delegatingFilterProxy는 Spring boot에서는 필요 없다.

그 이유는 Spring boot는 tomcat과 같이 서블릿 컨테이너도 관리하고 있기 때문에 필터를 빈으로 등록해주는 추가적인 작업이 필요치 않게 된다. 그 말의 의미는 톰캣이 이미 스프링 빈으로 관리되고 있다는 뜻이다.

그렇기 때문에 서블릿 필터도 이미 스프링 빈으로 자동적으로 등록되어 있다.
   
   
 <br>


</details>


### @Mock과 @InjectMock의 차이

<details>
   <summary> 자세히 보기 </summary>
   
 <br>
@mock 과 @InjectMock의 차이점은 Mock은 정말 목 오브젝트이지만 InjectMock은 실제 클래스의 인스턴스를 생성한다. 그리고 Mock 오브젝트를 의존성으로 주입받는 오브젝트이다.

   JUnit4 에서는 @RunWith(MockitoJUnitRunner.class) or Mockito.initMocks(this)를 사용하여 반드시 주입시킬 Mock오브젝트를 초기화 시켜줘야 한다.
   
   JUnit5 에서는 @ExtendWith(MockitoExtension.class)로 Mock 오브젝트 초기화가 가능하다.
   
   sample code
   ```
   @RunWith(MockitoJUnitRunner.class) // JUnit 4
// @ExtendWith(MockitoExtension.class) for JUnit 5
public class SomeManagerTest {

    @InjectMocks
    private SomeManager someManager;

    @Mock
    private SomeDependency someDependency; // this will be injected into someManager
 
     // tests...

}
   ```
   
   
   
 <br>
   
</details>
   
### Spring transaction propagation

<details>
   <summary> 자세히 보기 </summary>
   
 <br>
Spring tansaction propagation은 트랜잭션에 관한 것이다. 트랜잭션 설정이 돼있는 메소드가 다른 메소드를 호출했을때 해당 메소드가 기존에 존재하던 트랜잭션 안에서 실행될 것이나 아니면 새로운 트랜잭션을 생성해서 실행될 것이냐로 나뉜다.
   
   propagation_requires_new 는 새로운 트랜잭션을 생성해서 실행하는 것이고
   
   <img width="858" alt="스크린샷 2022-10-04 오후 11 27 50" src="https://user-images.githubusercontent.com/55564829/193846206-f6744f28-fc6c-42ad-bc30-60cda7cb3a29.png">
   
   
   propagation_required는 기존 트랜잭션 실행 흐름에서 실행되는 것을 얘기한다.
   
<img width="883" alt="스크린샷 2022-10-04 오후 11 28 28" src="https://user-images.githubusercontent.com/55564829/193846363-e8c89b1d-5772-4493-8122-b6b82ef1c62a.png">


 <br>
   
 </details>
   
 ### Spring security에서 JWT기반 유저인증

<details>
   <summary> 자세히 보기 </summary>
   
 <br>
   JWT기반 로그인에서 Spring security는 유저를 인증한다. 해당 JWT가 유효한 JWT가 맞다면 유저의 정보를 Security context holder에 저장해놓는다. 이 Security context holder에 유저 정보를 저장해놓으면 인증 이후 실행될 API에서 쉽게 유저의 정보에 접근하여 꺼낼 수 있다.
   
   이게 어떻게 가능한 것인가? 그것의 비밀은 바로 threadlocal에 있다. thread 로컬은 스레드내에 정보를 저장할 수 있게하여 해당 스레드가 살아있는 동안은 어디서든 해당 정보에 접근할 수 있다.
   그렇기 때문에 컨트롤러에서 유저의 정보를 쉽게 꺼내볼 수 있는 것이다. 하지만 이러한 것이 가능하려면 일단 spring seucirty filter에서 유저의 정보를 스레드로컬에 저장하는 작업이 필요하다.
   
   이는 filter를 새로생성하여 doFilter() 메소드 내에서 쿠키를 뒤지고 쿠키내에서 JWT를 확인한다면 해당 JWT의 유효성 검증 후 security context holder에 유저 정보를 저장해두는 필터를 생성하면 된다. 여기서 주로 사용되는 필터는 OncePerRequestFilter이다. 이 필터가 왜 주로 사용되냐면 서블릿은 여러개가 존재할 수 있고 필터들이 중복되는 경우가 발생할 수 있다. 이러한 경우를 대비하여 OncePerRequestFilter는 딱 한번만 실행될 수 있게끔 강제하기 때문에 유저의 인증과 같은 한번만 이뤄져야하는 작업에 대해서 구현할때 매우 유용하다.
   
   spring mvc와 같은 서블릿 컨테이너는 thread pool을 가지고 있다. 이는 여러개의 스레드를 미리 생성해놓고 요청에 스레드를 하나씩 할당하는 것이다. 우리가 만약 threadlocal에 정보를 저장하고 해당 요청이 끝난뒤에 thread를 그대로 반납하게 되면 memeory leak이 발생할 수도 있으며 다른 요청이 threadlocal에 남아있는 정보를 사용하다가 문제를 발생시킬 수도 있따.
   
   그러므로 threadlocal을 다 사용한 뒤에는 반드시 remove를 통해 저장된 정보를 지우고 threadpool에 반납해야 한다.
   이를 쉽게 하려면 ThreadPoolExecutor 를 상속받아서 beforeExcute()나 afterExcute()를 오버라이딩 하면 된다. ThreadPoolExecutor의 함수는 thread는 빌려주기 전 또는 반납 받기 전에 트리거 되는 함수를 제공하고 있으므로 이를 오버라이딩 한다면 따로 비즈니스로직에서 스레드로컬의 정보를 일일이 삭제하는 번거로움을 덜 수 있다.  
   
 <br>
   
 </details>

  
   
 ### proxy pattern과 decorator pattern

<details>
   <summary> 자세히 보기 </summary>
   
 <br>
   
   우리는 클라이언트가 의존하고 있는 클래스 (target class라고 부르기로 하겠다.)에 대해서 부가적인 기능을 더하고 싶을때 프록시 패턴과 데코레이터 패턴을 사용할 수 있다.
   
   두 패턴이 이름이 다르지만 근본적으로는 프록시 클래스를 사용하여 클라이언트의 타겟에 대한 요청을 대신 처리한다는 개념으로 같고 다른 점은 의도가 차이가 난다.
   
   프록시 패턴은 프록시 객체가 접근제어 역할을 하는 것이 주이다. (캐싱, 권한 체크)
   
   데코레이터 패턴은 타겟클래스의 행동에 대해서 부가적인 행동을 추가해주는 것을 의미한다. (로깅, 데이터 변환 등)

   이는 타겟 클래스에 추가적인 코드를 작성하지 않아도 새로운 기능을 추가할 수 있다는 점에서 확장에  유리해진다는 장점이 있다. 만약 100여개의 구현 클래스가 존재하는 인터페이스에 로깅 기능을 추가하고 싶다면 일일이 모든 구현 클래스에 로그를 추가해야될 것이다. 하지만 해당 인터페이스앞에 프록시 객체를 두고 로깅을 적용한다면 어떠한 구현 클래스를 수정하지 않아도 원하는 바를 이룰 수 있다.




   
 <br>
   
 </details>



   
