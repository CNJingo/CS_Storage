# 운영체제


   
   
</details>

### non blocking vs blocking & sync vs asnyc
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   blocking과 non-blocking의 주요한 차이는 제어권을 가지고 있느냐 호출한 함수에게 넘기느냐 입니다.
  
  제어권을 호출한 함수에게 넘기게 된다면 호출자는 호출한 함수가 끝날때까지 기다려야 합니다.
  
  하지만 non blocking은 제어권을 넘기지 않기 때문에 해당 함수를 호출해놓고 본인이 해야될 일을 그대로 진행할 수 있습니다.
  
  sync와 async는 결과의 처리관점에서 보면 됩니다.
  
  sync는 호출한 함수가 반환한 결과를 바로 처리해야 하지만 asnyc같은 경우 호출한 함수의 결과값을 그 즉시 처리해도 되고 안해도 됩니다.
  
</details>
