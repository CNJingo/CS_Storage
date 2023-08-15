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
	
 하지만 조상클래스를 자손클래스로 초기화했을때 조상클래스가 자손클래스의 변수를 가지고 있기는하다. 다만 참조는 안될뿐이다.
	
그렇기 때문에 해당 조상클래스를 자손클래스로 type casting한다면 자손클래스의 변수에도 값이 들어있는 것을 확인할 수 있다.

그래서 아래와 같이 초기화할떄 사용되었떤 자손 클래스의 변수를 타입캐스팅만 하면 해당 값에 접근할 수 있다.
	
<img width="399" alt="스크린샷 2022-12-14 오후 2 09 16" src="https://user-images.githubusercontent.com/55564829/207511072-ded91ecf-d170-4592-8ffa-a6729bebf4eb.png">

	
   
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

### Generics
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   지네릭스는 클래스, 인터페이스, 메소드를 정의할때 타입을 파라미터로 사용할 수 있게 해주는 기술이다. 타입 파라미터는 같은 코드를 여러가지 인풋에 맞게 사용할 수 있도록 해준다. 기존 파라미터는 값인 반면에 제네릭은 타입을 제공한다.

지네릭을 사용할때의 장점은 타입 캐스팅을 없애준다. 만약 지네릭이 없으면 오브젝트 클래스로 사용해야 하는데 이는 해당 객체를 사용할때 구체적인 클래스로 형변환이 필요하다. 하지만 지네릭을 사용하면 형변환이 따로 필요 없다.
	
generic을 구현하기 위해서 자바 컴파일러는 type erasure를 컴파일러에 적용해놨다. erasure는 raw java code를 해석하고 그것을 plain ordinary class, interface, method로 컴파일 타임에 변환한다. 그렇기 떄문에 generic은 런타임 오버헤드가 존재하지 않는다. type erasure는 제네릭을 지워버리고 Object나 해당 타입의 슈퍼클래스로 대체한다. 그리고 타입캐스팅을 집어넣어서 type safy를 보장한다.


```
List list = new ArrayList();
list.add("hello");
String s = **(String)** list.get(0);
```

```
List<String> list = new ArrayList<String>();
list.add("hello");
String s = list.get(0);   // no cast
```



    
</details>


### multithread 환경에서 singleton 생성
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   singleton을 만들기 위해서 우리는 일반적으로 private생성자를 생성해놓고 정적 팩터리 메서드를 생성하여 인스턴스가 없으면 새로 생성하고 이미 존재한다면 기존 인스턴스를 리턴하는 형식으로 싱글턴 객체를 생성한다.
   
   위의 방법이 아무 문제 없어 보이지만 멀티스레드 환경에서는 얘기가 다르다.
   
   멀티 스레드 환경에서는 
   
   ```
   if (instance == null) {
      return new Singleton();
   }
   ```
   
   이런식의 코드를 작성해도 여러개의 스레드가 동시에 if문 안으로 들어가게되면 하나의 객체 생성이 아닌 여러개의 객체가 생성될 수 있다.
   
   그렇다면 해당 인스턴스를 생성하는 부분 전체를 lock을 걸어서 여러개의 멀티스레드가 동시에 객체를 생성하는 것을 방지해야 될 것이다.
   
   이는 synchronized 키워드 또는 lock 키워드를 통해서 가능하다.
   
   하지만 인스턴스 생성함수 전체에 lock을 걸게 된다면 이미 인스턴스가 생성된 후에도 lock이 걸리므로 굉장히 성능에 악영향을 줄 것이다.
   
   그래서 이경우 
   
   ```
   if (instance == null) {
      synchronized (mutex) {
		   result = instance;
			if (result == null) {
				instance = result = new ASingleton();
         }
      }  
   }
   ```
   
   이렇게 instance가 널일 경우 그 안에서만 락을 걸어서 한번더 인스턴스의 null체크를 하고 인스턴스를 생성하는 로직을 만들게 되면 이미 인스턴스가 생성되지 않은 상태에서는 lock이 걸리지 않으므로 성능을 높일 수 있다.
   
   여기서 또 주의해야될 사항은 instance에 새로운 객체를 넣어주는 행위는 스레드가 돌고 있는 코어의 캐시에 저장되고 램 메모리에 동기화 되지 않는다. 원래 스레드는 코어의 캐시에 업데이트를 하고 해당 내용을 ram과 언제 동기화할지는 아무도 알 수 없다.
   
   그렇기 때문에 A라는 스레드가 instance를 생성했어도 B스레드 입장에서는 여전히 null로 확인될 수 있는 것이다.
   
   이 경우를 방지하기 위해서 instance 변수에 volatile 키워드를 넣어서 변화가 생기면 바로 ram과 동기화를 강제로 시킨다면 위와 같은 문제를 해결할 수 있다.


    
</details>
	
	
### String vs StringBuilder vs StringBuffer
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
String은 final class이다. 한번 생성되고 나면 그 값이 변하지 않는다. String안에 value라는 바이트 배열은 final로 선언돼있기 때문이다.
	
String은 final class로 선언돼있어서 몇가지 이점을 갖는다. 일단 불변한 객체이므로 멀티스레드 환경에서 접근할때 안전하다.
	
readOnly이기 때문이다.
	
그렇기 때문에 같은 스트링은 재 생성하지 않고 기존에 있는 String pool에서 가져다 쓰므로 메모리 절감 효과도 가져온다.

StringBuilder 역시 byte 배열을 내부적으로 가지고 있다.
하지만 String과 달리 final클래스가 아니다. 그래서 Append를 하면 내부적으로 str.getBytes()를 호출하여 String byte배열을 System.arraycopy로 StringBuilder에서 사용하는 byte배열로 퍼담는다.

물론 이 과정을 진행하기 전에 byte배열의 크기를 살피고 capacity를 초과하는 경우 value 배열에 Arrays.copy를 통해서 기존 값을 담음과 동시에 새로운 length를 부여한다.

위 과정은 ArrayList에 값을 추가하는 과정과 매우 유사하다.
내부적으로는 배열로 선언돼있지만 동적으로 작동하는 것처럼 보이기 위해 element를 추가할때마다 capacity를 확인하고 부족하면 늘린뒤에 copy함수를 통해 기존 값들을 담는다.
	
StringBuffer와 StringBuilder는 둘다 AbstractStringBuilder를 상속한 클래스이다.

두개의 차이점은 StringBuffer는 AbstractStringBuilder의 메소드를 오버라이드 할때 전부 synchronized keyword를 붙였다는 점이 다르다. 이는 메소드에 진입할때 락을 건다는 뜻이고 멀티스레드 환경에서 안전한 사용을 보장받을 수 있다. 하지만 매번 메소드 호출마다 락을 걸기때문에 성능면에서는 StringBuilder보다 느릴 수 밖에 없다.

그러기 때문에 단일 스레드 환경에서는 StringBuilder를 쓰는게 더 효율적이라고 볼 수 있다.

    
</details>

### for loop vs stream
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
for loop이 일반적으로 속도가 빠르다  하지만 들어오는 인풋의 길이가 엄청나게 크다면 stream이 유리하다.

왜냐하면 stream은 병렬처리가 가능하기 때문에 큰 데이터일수록 유리해진다.

병렬처리에 사용되는 overhead가 존재하기 때문에 작은 데이터에는 알맞지 않다.

stream이 좋은 이유는 몇가지 더 존재한다.

첫번째는 가독성이다. functional programming을 사용하여 가독성을 높인다. 함수형 프로그래밍의 장점은 해당 함수가 어떤식으로 동작할지 예측이 가능하다는 점이다. map이나 filter와 같이 어떤역할을 할지 명확하게 보이며 해당 함수의 파라미터로 원하는 동작을 하는 함수를 넣어서 사용할 수 있다.

보통 for loop같은 경우에는 내부코드를 뜯어봐야지만 어떤 동작을 하는지 알 수 있다.

두번째는 mutability가 낮다. stream은 기존의 element들을 변경하지 않고 새로운 stream을 생성해낸다. 그렇기 때문에 원본을 바꾸지 않기 떄문에 변화 가능성을 낮춰서 디버깅하기 쉬운 프로그래밍을 할 수 있다.

    
</details>
	

### Volatile
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
	
 volatile 키워드는 멀티스레드 환경에서 중요한 키워드이다. 스레드는 성능적인 이슈 때문에 메인 메모리에 있는 변수를 스레드 캐시에 복사해서 사용하게 된다. 만약 서로 다른 스레드가 서로 다른 프로세서 위에서 실행되고 있다면 스레드가 변경한 변수는 언제 메인 메모리에 동기화 될지 모른다. 이 때문에 해당 변수의 상태는 불일치 상태가 될 확률이 매우 높다.

해당 변수를 volatile로 선언하게 되면 변수를 변경하게 되면 변경사항이 바로 메인메모리에 동기화 된다. 그렇게 되면 해당 변수를 사용하는 모든 스레드가 최신 상태의 변수를 사용할 수 있게 된다.

volatile 키워드는 주로 다음과 같은 상황에 사용된다.
1. 하나의 스레드가 write를 하고 다른 스레드는 read를 하고 있을때
2. 여러개의 스레드가 공유변수에 writing을 하고 있고 그 operation이 atomic할때

valatile은 하지만 synchronized 키워드와 달리 non-atomic operation이나 composite operation이 공유번수에 작용할때 thread safety를 보장하지는 못한다.

synchornized는 크리티컬 섹션에 오직 하나의 스레드만 허용하여 다른 스레드를 블락 시킬 수 있기 때문에 thread safety를 보장한다.
	
	
</details>


### JVM
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
	
 JVM의 메모리 영역은 HEAP, STACK, naitve method area, pc register, method area

 크게 다섯가지로 나뉜다.

 heap 메모리는 java7까지 permgen이라는 특별한 영역을 가지고 있었는데 이 메모리 공간은 런타임 클래스나 메소드에 대한 메타데이터나 static variable, 상수 풀같은 것들을 저장해두는 역할을 하였다.
 하지만 java8부터는 permgen이 사라지고 metaspace라는 영역으로 바뀌었따 metaspace는 os레벨에서 관리되는 메모리 영역이기 때문에 permgen보다 훨씬 더 많은 메모리 영역을 사용할 수 있다.
 permgen이 metaspace로 바뀌면서 metaspace에서 클래스와 메소드에 관련된 메타데이터를 가지게 되었고 static variable의 저장소는 heap메모리에 남게 되었다.

 native method area는 JVM에서 시스템콜을 호출할때 C로 랩핑돼있는 함수를 호출해야할 필요가 있는데 (JNI를 사용해서) 이때 이러한 메소드들이 저장되어 있는 영역이다.

 method area는 클래스나 메소드에 대한 메타데이터를 저장하고 있다. 여기서 헷갈릴 것이 permgen이랑 겹치는거 아니냐는 의문을 가질 수 있다. 찾아보니 method area는 permgen에 포함된 영역이였다.

 오라클 reference를 확인해보니 permgen도 heap의 영역중 일부란다. 그럼 method area는 permgen의 일부이고 permgen은 heap의 일부이니 method area역시 heap메모리에 포함관계라고 생각해야겠다.

 pc register는 현재 스레드들이 실행하고자 하는 instruction의 주소가 저장되는 공간이다.

 https://www.baeldung.com/jvm-static-storage

 https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
	
</details>
