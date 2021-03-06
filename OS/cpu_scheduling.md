# CPU 스케줄링

선점형과 비선점형 방법이 있다. CPU의 사용을 프로세스가 강제로 뺏을 수 있는가 없는가로 나누어 진다.  

스케쥴링의 효율을 분석하는 기준
- CPU Utilization(이용률 %) : CPU 수행 비율
- Throughput(처리율, job/sec) : 단위 시간당 처리량
- Turnaround time(반환시간) : 프로세스가 모든 작업을 끝내고 종료하는데 걸린 시간
- Waiting time(대기 시간) : CPU를 점유하기 위해 ready queue에서 기다린 시간
- Response time(응답시간) : 입력에 대한 반응 시간

<br>

## 스케줄링 알고리즘

### **First-Come First-Served(FCFS)**
먼저 온 프로세스가 CPU를 점유  
단순해서 좋음. But, 먼저 들어온 프로세스의 처리시간이 길면 다른 프로세스의 Waiting time이 길다.  
비선점형 방식 중 하나임.  

### **Shortest-Job-Frist(SJF)**
말 그대로 짧은 수행시간을 가진 프로세스가 먼저 CPU를 점유.  
효율적으로 보이지만 현실적으로 프로세스의 수행시간을 완벽히 알기가 어려움(여러가지 변수가 존재하기 때문에)  
예측해서 사용할 수 있지만 오버헤드가 큰 작업이다.  
비선점형 방식 중 하나임.  

Shortest-Remaining-Time-Frist(SRT)로 SJF의 선점형 방식.  
새로운 프로세스가 도착할때, 현재 수행중인 프로세스의 남은 수행시간(burst time)보다 짧다면,  
그 프로세스에게 cpu를 뺏긴다.  
처리시간이 긴 프로세스는 오래동안 처리하지 못하는 단점이 있다.  


### **Priority**
우선순위(중요도(작은 값이 우선순위가 높다.))가 높은 프로세스를 먼저 선택.  
But, 우선순위가 높고 처리시간이 긴 프로세스가 오래동안 cpu를 잡을 경우 다른 프로세스는 오래동안 처리하지 못한다.  
해결방안으로 **aging**이 있다.  
ready queue에서 일정시간이 지나면 우선순위를 높여주는 것이다. 즉, queue에 오래 머무를 수록 우선순위를 높여 빨리 처리하게 만드는 것이다.  
선점형 방식 중 하나임.  

### **Round-Robin(RR)**
원 모양으로 프로세스가 돌아가게 하는 방법(시분할 시스템에서 주로 사용)  
일정 시간을 정해 프로세스가 실행 후 대기 상태로 돌아감 이런 일을 반복한다.  
일정시간을 Time Quantum이라고 부른다.  
선점형 방식 중 하나임.  

