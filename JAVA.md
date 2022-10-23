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

### 상속관계에서의 다형성
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
   
   조상 클래스의 참조변수는 자손 클래스의 인스턴스로 초기화가 가능하다.
   
   예를 들어
   
   ```
   class Car {
      
   }
   
   class SportsCar extends Car {
   
   }
   ```
   다음과 같은 클래스가 있을때 Car car = new SportCar(); 과 같은 초기화가 가능하다는 것이다.
   
   이렇게 초기화를 할경우 조상클래스에 있는 멤버들만 사용가능하다는 제약이 있다. 당연히 조상클래스를 자손클래스로 초기화했으니 자손클래스의 멤버변수나 메소드에는 접근이 불가능한 것이다.
   
   역으로 자손클래스를 조상클래스로 초기화가 가능한가? 그건 아니다.
   
   왜냐하면 자손클래스의 멤버가 조상클래스보다 더 많기 때문에 이를 허용하지 않는다.
   
   
</details>

### 인터페이스의 default method
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
   
   자바 1.8부터는 인터페이스에서 default method라는 기능을 제공한다.
   
   이는 모두 추상 메서드로 이루어져있는 기존의 인터페이스와 달리 구현체가 있는 메소드를 선언할 수 있게 해준 것이다.
   
   왜냐? 인터페이스 설계는 보통 구현체들의 공통 요소를 뽑아서 추상화를 잘 해야한다.
   
   하지만 설계를 아무리 잘해도 인터페이스에 메소드가 추가돼야할 경우가 생긴다.
   
   이런 경우에 인터페이스의 메소드를 추가하는 경우 그 인터페이스를 구현한 모든 구현체에서 해당 메소드를 다시 구현해줘야 하므로 많은 변경이 생기게 된다.
   
   하지만 이런 경우 default method를 추가해준다면 구현체들에서 해당 메소드를 구현해주는 번거로움을 덜 수 있다. (구현을 안해줘도 된다 default method는)
   
</details>

### 생성자 vs 정적 팩터리 메서드
<details>
   <summary> 자세히 보기 </summary>
   
 <br>
   
 
   클래스의 인스턴스를 생성할때 생성자보다 정적 패터리 메서드가 더 선호된다. 이유는 세가지가 있다.
   
   첫번째는 생성자는 클래스이름과 동일한 반면 (이름이 강제됨) 정적 팩터리 메서드는 조금 더 유의미한 함수 이름을 통해서 생성자를 만들 수 있다.
   
   예로들어 BigInteger.probablePrime()과 BigInteger() 두개 중 어떤 값이 소수인 BigInteger를 반환할 것 같은가? 
   
   정적 팩터리 메서드는 함수 명을 통해서 어떤 인스턴스를 받을 것인지 예상이 쉽게 만들어준다.
   
   두번째는 호출될때마다 인스턴스를 새로 생성하지 않아도 된다는 점이다.
   
   정적 팩터리 메서드를 사용하면 계속 새로운 인스턴스를 생성하는 것이 아니라 이미 인스턴스가 있다면 해당 인스턴스를 리턴해준다거나 또는 아예 인스턴스를 생성하지 않는등 인스턴스를 통제할 수 있는 방법을 제공해준다.
   
   예를들어 어떤 클래스의 인스턴스를 싱글턴으로 강제하고 싶으면 정적팩터리 메서드 패턴으로 가능하다.
   
   세번째는 반환 타입의 하위 타입 객체를 반환할 수 있다.
   
   인터페이스의 정적메서드를 통해서 구현체인 여러개의 클래스중 하나를 반환할 수 있게끔 할 수 있다. 이는 구현 클래스를 공개하지 않고도 해당 객체를 반환할 수 있게하여 API를 작게 유지할 수 있다.
   
   네번째는 매개변수에 따라서 다른 클래스의 객체를 반환할 수 있다. 이는 세번쨰의 장점을 활용한 것인데 매개변수에 따라서 서로 다른 클래스의 인스턴스를 반환하게끔하여 클라이언트로 하여금 유연하게 상황에 맞는 클래스를 사용할 수 있게끔 할 수 있다.
   
   
 <br>

</details>

### private 생성자
<details>
   <summary> 자세히 보기 </summary>
   
   
 <br>
   
   
   private 생성자는 보통 객체를 싱글턴으로 만들기 위해서 사용된다.
   
   왜냐하면 private 생성자는 클라이언트 입장에서 호출할 수 없기 떄문에 클라이언트가 생성자를 호출해서 새로운 인스턴스를 생성하는 것 자체가 불가능해지기 때문이다.
   
   이럴경우 멤버변수로 인스턴스를 생성해놓고 변수자체를 public 하게 하거나 정적 팩터리 메서드를 제공하여 인스턴스를 리턴하는 방식 두가지로 싱글턴 객체를 구현할 수 있다.
   
   싱글턴의 전형적인 예로는 무상태 객체나 설계상 유일해야하는 컴포넌트로 사용한다.
   
   싱글턴 객체는 mock 오브젝트 생성이 어려워 테스트하기가 어렵다는 단점이 있다.

   여기서 주의할 점은 리플렉션 api를 사용하여 private생성자를 호출할 수 있기 때문에 생성자를 수정하여서 두번째 객체가 생성되려고 한다면 아래와 같이 예외를 던지게끔 구현해놓는 것이 좋다.
   
   ```
   private Test() {
    if (INSTANCE != null)
        throw new IllegalArgumentException("Instance already created");
   }
   ```
   
   private생성자는 첫번째 방법이고 싱글턴을 만드는 두번째 방법은 정적 팩터리 메서드를 public static으로 제공하는 것이다. private static final 인스턴스를 반환하게끔 하여서 제2의 인스턴스가 생성되는 것을 방지한다.
   
   만약 싱글턴 객체를 직렬화 하려면 단순히 serializable을 구현하는 것만으로는 부족하다. readResolve메서드를 제공해야 한다. 이렇게 안하면 역직렬화 과정에서 새로운 인스턴스가 생성되기 때문에 readResolve 메소드를 통해서 본디 생성돼있는 객체를 반환하게끔 만들어줘야 한다.
   
   그리고 private 생성자를 만들었을 경우에는 상속이 안된다. 그 이유는 모든 생성자는 따로 명시하지 않아도 상위 클래스의 생성자를 호출하게 되는데 private 생성자는 다른 클래스에서 호출이 안되기 때문이다.
   
</details>


### Autoboxing Unboxing
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
   Autoboxing은 primitive type을 랩핑한 클래스를 사용하는 것을 얘기한다. unboxing 반대로 wrapping 된 클래스에서 primitive type으로 변환하는 것을 얘기한다.
   
   이러한 작업은 JVM에서 자동으로 이루어진다. JAVA8 에서는 모든 primitive type에 대한 wrapper class가 존재한다. 이게 왜 필요한가? primitive type에 대한 여러가지 미리 정의된 method들을 제공하기 때문에 유용하게 사용할 수 있다.
   
   그리고 wrapper class는 객체이기 때문에 레퍼런스를 저장하고 있다. 그래서 null값을 가지고 있을 수도 있다. 그리고 wrapper class는 Object를 예상되는 곳에서 사용할 수 있다.
   
   예를 들면 ArrayList같은 Collection은 Object배열 형태로 값을 저장해야 하는데 여기서는 객체가 예상되므로 primitive type을 사용할 수 없다.
   
   그래서 우리가 ArrayList<int> 는 선언 자체가 안되고 ArrayList<Integer>로 선언해야 하는 것이다.
   
   그렇다면 모든 primitive type을 wrapper class로 대신해서 사용해도 되나? 그건 아니다.
   
   wrapper class는 객체이기 때문에 새로운 메모리공간을 사용하게 된다. 우리가 primitive type으로 선언할 수 있는걸 굳이 wrapper class로 사용하게 된다면 불필요한 객체를 다수 생성하게 될 수 있다.
   
   예를 들어
   
   ```
   Long sum = 0;
   for (long i = 0; i < 10; i++) {
      sum += i;                        
   }
   ```
   
   만약 위와 같은 코드가 존재한다면 i가 하나씩 증가할때마다 새로운 sum 객체가 생성될 것이다.
                           
   이는 프로그램의 속도를 매우 느려지게할 뿐 아니라 불필요한 메모리 공간을 너무 많이 생성한다.
                           
   이때 sum을 long으로 선언한다면 primitive 타입에 값을 더하기만 하면 되어 불필요한 객체 생성을 막을 수 있다.
   
   
    
</details>



