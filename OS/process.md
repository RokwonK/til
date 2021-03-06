# 프로세스

## 프로세스
- 고유 stack 메모리를 가지고 있음
- 고유 메모리를 가지고 있음 (Protection)
- 고유 파일스크립터를 가지고 있음
- 고유 PID(프로세스 아이디)를 가지고 있음

<br>

### **어떻게 만들어지는가?**
fork() => 시스템 콜 함수(다른 프로세스(자식 프로세스)를 생성)  

<br>

### **좀비, 고아 프로세스**
프로세스가 종료될 때,  
자식이 부모한테 SIGCHLD를 보냄(종료한다는 뜻)  
=> 메모리 등 자원을 수거함  
=> 부모는 wait() (수거를 준비하기 위해)  
=> 수거하지 못하고 자식 프로세스가 사리잔다면?  
=> 그 자원들을 쓰지 못함 이런 프로세스를 `좀비 프로세스`라고 함.  

자식보다 부모 프로세스보다 먼저 종료된다면?  
=> 자식 프로세스를 `Orphan(고아) 프로세스`라고 함.
=> 자식 프로세스는 다른 부모 밑에 붙게 됨.(1번 루트 프로세스)

<br>

### **프로세스 상태**
1. New  
프로세스가 생성
2. Ready  
자원을 사용할 수 있는 상태 But, CPU가 이 프로세스를 돌리지 않고 있음
3. Running  
CPU가 이 프로세스를 돌리고 있는 상태
4. Waiting  
외부 이벤트(입출력) 시, 자식 프로세스가 끝날 시 기달는 상태
5. Terminated  
프로세스가 끝남

<br>

### **프로세스의 정보**  
각 프로세스들은 자신들의 정보를 담는 Process Control Block을 가지고 있음.  
- Process ID
- Parent PID,Next process block(linked list로 구현되어 있음)
- Process state(프로세스 상태)
- TCBs( 쓰레드 컨트롤 블락 )
- CPU information
    - 자신이 가지고 있던 register 정도들을 저장해 놓음.  
    - Context Switching이 일어날때 자신의 정보를 저장해 두고  
    다시 자신이 CPU를 사용 시, 저장해둔 정보를 가져와서 사용함.
- 등등...

<br>

### **여러개의 프로세스가 어떻게 하나의 CPU를 공유하며 사용 가능한가?**  
- Context Switching(커널에서 실행)  
1. 프로세스1 -> 프로세스2로 CPU사용이 옮겨간다고 보자.  
2. 프로세스1의 cpu 사용정보를 자신의 PCB에 저장.
3. 프로세스2는 자신이 전에 사용했떤 cpu 사용정보를 가져와 cpu에 넘김
4. 프로세스2의 동작을 수행함

Context Switching은 누가 일으키는 걸까?  
kernel에서 프로세스 메니지 블락, 스케줄러 블락에서 실행함  

Context Switching의 문제점?  
프로세스 정보를 저장 및 가져올때의 시간소비(Overhead)가 있음.  
