# Spring

### Spring AOP란 무엇인가?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>

Spring에서 Aspect Oriented Programming을 가능케 해주는 기능이다. 
Spring AOP를 위해서는 필수적으로 알아야할 개념이 3가지 정도가 존재한다.

Joint point: 에러 핸들링 또는 함수의 실행을 시작할 포인트를 얘기한다. Spring AOP에서는 언제나 함수의 실행이 joint point가 된다. 

Pointcut: 조인포인트와 매칭되는 표현식을 얘기한다. pointcut은 한개 이상의 jointpoint를 담고 있을 수 있다. 
한마디로 어떤 조인포인트에서 함수를 실행시킬지 범위를 뜻한다.

Advice: 포인트 컷에 매칭되는 조인포인트에서 실행되는 것을 얘기한다.

이러한 AOP는 트랜잭션과 같이 자주 중복되는 관심사를 모듈로 빼내어 효과적으로 관리할 수 있을 뿐만 아니라 보일러 플레이트 코드를 줄일 수 있다는 장점이 있다. 

또한 기존의 코드 로직은 변경시키지 않은채 새로운 작업을 추가시킬 수 있어서 기능 확장에 유리하다.

</details>
