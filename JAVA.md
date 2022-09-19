# JAVA

### Hashcode and equals() method
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   equals 메소드는 객체 두개를 파라미터로 받아서 두객체의 동일성을 비교하는 함수이다.

   public boolean equals(Object obj) {
        return (this == obj);
    }
    
    equals 메소드는 오버라이드가 가능하지만 몇가지 제약사항을 가지고 있다.
    1. x.equals(y) 가 true 라면 y.equals(x)도 true 여야 한다.
    2. x.equals(y) 와  y.equals(z) 가 둘다 true 라면 x.equals(z)도 true 여야 한다.
    3. equals 메소드가 수정되지 않는한 항상 equals() 호출은 늘 같은 값을 리턴해야 한다.
    
    hashcode() 는 오브젝트가 가지고 있는 native method이다. object의 hash 값을 리턴하는 함수이다.
    
    hashcode() 메소드에도 몇가지 제약사항이 존재하는데
    1. hashcode()를 호출할떄마다 늘 같은 결과를 리턴해야 한다.
    2. 애플리케이션 실행시마다 hashcode()의 값은 달라진다.
    3. 만약 equals() 메소드로 같은 같은 오브젝트로 판명된다면 두 오브젝트는 같은 hashcode() 값을 가지고 있어야 한다.
    4. 만약 equals() 메소드로 같지 않은 오브젝트로 판명된다면 두 오브젝트는 같은 해쉬 값을 가질 수도 아닐 수도 있다.
    
    4번 제약 사항은 아래를 의미한다.
    If o1.equals(o2), then o1.hashCode() == o2.hashCode() should always be true.
    If o1.hashCode() == o2.hashCode is true, it doesn’t mean that o1.equals(o2) will be true.
    
    만약 당신이 equals() 메소드를 오바라이딩 한다면 거의 대부분의 경우 hashcode()도 오버라이드 해줘야 제약사항을 지킬 수 있다.
    만약 당신이 제약사항을 어겼지만 해당 클래스를 해쉬 테이블의 키로 사용할 것이 아니라면 문제가 발생하지 않는다.
    
</details>
