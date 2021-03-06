# 멀티 프로세싱, 멀티 태스킹, 멀티 프로그래밍, 멀티 쓰레딩

## 멀티 프로세싱
여러 개의 프로세서가 서로 협력적으로 일을 처리하는 것.  
즉, cpu 여러개가 작업처리를 같이 병렬적으로 수행하는 것이다.  

<br>

## 멀티 태스킹
Task을 말 그대로 일을 동시에 처리하는 것이다.  
Task란 작업의 단위. 프로세스, 쓰레드 모두 작업의 단위가 될 수 있음.  
멀티 쓰레딩, 멀티 프로그래밍의 상위 개념이라고 할 수 있다.  
동시에라고 하지만 조금씩 번갈아가며 처리하기에 동시에 라고 느끼는 것이라고 하는게 더 좋은 표현이겠다.  
ex) 멜론으로 노래들으며 코딩하기  

어떻게 번갈아가며 처리할까?를 해결해주는게 멀티 태스킹 스케쥴링 방식이다.  
다른 말로 [CPU 스케쥴링](https://github.com/RokwonK/til/blob/master/OS/cpu_scheduling.md) 이라고 한다
- 비선점형 : CPU를 차지하는 쓰레드가 자신이 이제 연산이 필요없다라고 할때, CPU를 넘겨주는 것
- 선점형 : OS가 트리거를 통해 CPU 사용을 강제로 빼앗아 올 수 있게 하는 것
    - 대부분의 OS가 사용하는 방식


프로세스 간의 자원을 공유하지 못한다.  
자원 공유를 위해서 IPC(Inter Process Communication)를 구현해야함

<br>

## 멀티 프로그래밍
단일 프로세서 안에서 여러개의 프로세스가 동시에 실행되는 것.  
(동시에 보다는 번갈아가며 처리해 동시에 라고 느낌. ), (하나의 프로세서에서 하나의 일만 처리 가능)  
즉, 각 프로세스를 조금씩 처리함으로써 동시에 실행되는 것 처럼 보이게하는 것이다.  

<br>

## 멀티 쓰레딩
쓰레드는 프로세스 안에서 생성되고 일을 처리할 수 있는 하나의 주체이다.  
이런 쓰레드를 한 프로세스안에서 여러 개 만들어 사용하는 것이 멀티 쓰레딩  
멀티 태스킹과의 차이는 일부 자원을 공유 (힙(전역 변수), stack 중 Data영역(프로그램 변수, 스택 공간) )을 공유한다.
Context Switching이 빠르게 일어나 효율이 두 프로세스간의 Context Switching보다 30%이상 좋다고 한다.