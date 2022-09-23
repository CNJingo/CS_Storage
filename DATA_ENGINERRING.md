# 데이터 엔지니어링



</details>

### Hadoop의 동작
<details>
   <summary> 자세히 보기 </summary>
 
 <br>


![lRpoU](https://user-images.githubusercontent.com/55564829/191906711-ac0f4302-f58a-484f-948d-59619453e691.jpeg)


사용자는 본인의 비즈니스 로직은 Mapper, Reducer클래스에 맞춰서 작성한다.
  
사용자의 코드는 분산환경의 slave node에서 실행된다.
  
InputFormat은 inputSplit() 함수를 통해서 input file을 small piece들로 쪼갠다.
  
그다음 RecordReader가 raw data를 key-value 형태의 데이터로 변환시킨다.
  
Mapper가 이 key-value형태의 데이터를 가공한 뒤에 OutputCollector에게 보낸다.
  
Reporter() 함수가 유저에게 mapping task가 끝났음을 알린다.
  
Reduce() 함수는 매퍼로 부터 온 key-value데이터를 최종 데이터 형태로 만든다.
  
OutputFormat은 최종 데이터를 HDFS에 기록한다.


### Shuffling은 왜 필요한 것인가? 

→ 매퍼로 부터 나온 데이터를 같은 키 별로 묶어서 리듀서에게 전달해주기 위해 필요한 과정이다.

  ### sort는 왜 필요한 것인가?

→ 키를 기준으로 정렬하여 리듀서에게 이전의 키들과 구분이 가능하게 하여 새로운 리듀서의 생성을 용이하게 해준다. 

우리는 Mapper에서만 실행되는 (Reducer 없이) Job을 생성할 수 있다. 
job.setNumreduceTasks(0) 이 설정을 넣어준다면 Reducer가 없이 Mapper에서 나온 output이 최종 output이 되는 job을 생성할 수 있다.

이 것의 장점은 shuffle과 sorting이 자원을 많이 잡아먹는 Task이기 떄문에 reducer가 꼭 필요한 상황이 아니라면 해당 설정을 사용할 수 있다.



### Data locality
큰 볼륨의 데이터로 인해 발생하는 cross-swtich network traffic을 해결하기 위해 나온 것이다.

큰 볼륨의 데이터를 계산하는 곳으로 옮기는 것이 아닌 계산을 데이터 근처에서 하는 것을 의미한다.

하둡에서 dataset은 datanode에 저장되어 있다. 유저가 MapReduce job을 실행시키면 이 job은 관련 있는 데이터 노드로 가서 실행된다.


</details>

