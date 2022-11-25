### Batch update returned unexpected row count from update [0]; actual row count: 0; expected: 1;
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
  
  하나의 서비스 함수가 다른 서비스 함수를 호출하는데 호출하는 함수가 굉장히 시간이 오래걸리는 함수였다.
  
  첫번째 서비스 함수에는 @Transactional이 붙어있었지만 해당 함수가 호출하는 다른함수에는 어노테이션이 따로 없어서 transaction의 propagation 레벨을 살펴보았다. default는 required로 새로운 트랜잭션이 발생해도 부모 트랜잭션이 존재하는 상황이라면
  기존 트랜잭션을 그대로 사용한다. 그렇다면 해당 트랜잭션이 시간이 많이 소요되는 부가적인 함수를 호출했고 트랜잭션이 길어지면서 다른 트랜잭션이 동일한 entity의 값을 업데이트 하려다가 발생한 것이다.
  
  마치 git push를 하기전에 원격저장소가 다른 요인에 의해 변경되었다면 먼저 pull로 로컬 저장소의 sync를 맞춰야하는 것처럼 말이다.
  
  처음에는 해당 에러에 ObjectOptimisticLockingFailureException이라는 Exception log가 남아있어서 JPA에서 default로 optimistic locking을 사용하는 줄 알았지만 JPA에서 optimisitc locking을 사용하려면
  @Version 에노테이션이 붙은 Integer타입의 인스턴스 변수가 필요하다는 것을 알게되었다.
  
  그래서 나는 문제 해결을 위해 without @Version annotation OptimisicLockingException is occured와 같은 키워드로 구글링을 하였다.
  
  이 문제를 해결하려면 트랜잭션에서 Lock을 걸고 사용하면 같은 문제가 발생하지 않을 것이다. 하지만 Lock에 대한 오버헤드는 크고 경쟁 상황이 많이 일어나지 서비스이므로 Lock을 고려하지는 않기로 하였다.
  
  만약 경쟁상황이 많이 일어나느 서비스여서 트랜잭션이 실패하고 재생성되는 횟수가 많아진다면 Lock을 고려하는 것이 더 낫다.
  
  ref:
  https://stackoverflow.com/questions/2743130/hibernate-batch-update-returned-unexpected-row-count-from-update-0-actual-row/46989666#46989666

</details>
