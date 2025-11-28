# 오픈소스SW개론 과제 2

## 주제 : 리눅스 명령어 중에서 top, ps, jobs, kill에 대해서 조사해보자.

### 1. top(Table Of Process)

시스템의 프로세스들을 실시간으로 모니터링 할 수 있게 해주는 명령어입니다.

#### 기본 사용법 : 
```bash
top
```

| 옵션 | 설명 | 예시 |
|------|-----|-----|
| -d (숫자) | 몇 초마다 갱신 | `top -d 5` |
| -n (숫자) | 갱신 횟수 지정 후 종료 | `top -n 3` |
| -p (PID) | 특정 프로세스만 모니터링 | `top -p 1111` |
| -u (사용자명) | 특정 사용자만 모니터링 | `top -u root` |
| -i | idle 프로세스 숨기기 | `top -i` |
| -H | Threads 단위로 표시 | `top -H` |

> ### **화면 구성**
> 
> `top - 03:40:44 up 3 min,  0 users,  load average: 0.12, 0.06, 0.01`
> 
> 첫번째 줄 : 현재 시간 , 가동 시간, 사용자 수, load average(1분, 5분, 15분 부하 평균)
>
> `Tasks:   2 total,   1 running,   1 sleeping,   0 stopped,   0 zombie`
>
> 두번째 줄 : total(전체 프로세스), running(실행 중 프로세스), sleeping(대기중인 프로세스), stopped(중지 프로세스), zombie(좀비 프로세스)
>
> `%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 99.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st`
>
> 세번째 줄 : CPU 사용률 { us(user space), sy(kernel space), ni(nice 값이 조정된 프로세스), id(idle time), wa(I/O Wait),
> 
> hi(hardware interrupt), sw(software interrupt), st(steal time(VM)) }
>
> `MiB Mem :   7837.0 total,   7199.9 free,    331.0 used,    306.2 buff/cache`
>
> 네번째 줄 : 메모리 사용량(MiB 단위) { total(메모리 총량), free(빈 메모리 공간), used(사용된 공간), buff/cache(캐싱 공간) }
> 
> `MiB Swap:   1024.0 total,   1024.0 free,      0.0 used.   7342.9 avail Mem`
>
> 다섯번째 줄 : Swap 메모리 사용량(MiB 단위) { total(메모리 총량), free(빈 메모리 공간), used(사용된 메모리 공간), avail Mem(사용 가능 메모리)
>
> 프로세스 목록 :
>
> ```
> PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
>  1 root      20   0    4144   3328   2736 S   0.0   0.0   0:00.01 bash
> ```
>
> PID(Process ID), USER(사용자명), PR(priority), %CPU(CPU 사용률), %MEM(메모리 사용률), TIME+(실행 시간) 이하 생략.
>
#### 실행 중 명령어
```bash
q : 종료
(space) : 즉시 갱신
h or ? : 도움말 표시
k : 프로세스 종료(PID 입력 후 시그널 선택)
r : nice 값 변경
M : 메모리 사용량 기준으로 정렬
P : CPU 사용량 기준으로 정렬
T : 실행 시간 기준으로 정렬
u : 특정 사용자 필터링
1 : CPU 코어별 사용률 토글
c : 전체 명령어 경로 토글
f : 표시할 필드 선택
```
___

### 2. ps

현재 실행 중인 프로세스의 스냅샷을 보여주는 명령어입니다.

top와는 달리 정적으로 한번 만 보여줍니다.

특정 프로세스가 존재하는지 확인하거나, PID를 확인해서 kill 하려고 할 때에 사용합니다.

#### 기본 사용법 : 
```bash
ps
```
| 옵션 | 설명 | 예시 |
|------|-----|-----|
| -A | 모든 프로세스를 출력 | `ps -A` |
| -a | 데몬 프로세스처럼 터미널에 종속되지 않은 모든 프로세스 출력 | `ps -a` |
| -e | 커널 프로세스를 제외한 모든 프로세스를 출력 | `ps -e` |
| -f | 출력을 풀 포맷으로 표기(UID, PID, PPID 등이 함께 출력) | `ps -f` |
| -o | 출력 포맷을 지정 | `ps -o` |
| -m | 프로세스 뿐만 아니라 커널 threads도 함께 출력 | `ps -m` |
| -u (사용자) | 특정 사용자의 프로세스 정보 출력 | `ps -u root` |

> ### **출력 항목 **
> 
> ```
>   PID TTY          TIME CMD
>   1 pts/0    00:00:00 bash
>  13 pts/0    00:00:00 ps
> ```
> 
> PID : 프로세스 ID, TTY : 프로세스와 연결된 터미널, TIME : 총 CPU 사용 시간, CMD : 프로세스의 실행 명령행
> 
> `ps -f` 처럼 -f 옵션을 주어 출력할 경우 더 많은 항목이 표기됩니다.
>
> ```
> UID        PID  PPID  C STIME TTY          TIME CMD
> root         1     0  0 03:51 pts/0    00:00:00 /bin/bash
> root        14     1  0 04:00 pts/0    00:00:00 ps -f
> ```
> 
> PPID : 부모 프로세스 ID, C : 짧은 기간 동안의 CPU 사용률, STIME : 프로세스가 시작된 시간
>
> `ps -ef | more`로 많은 프로세스 목록 출력할때 주면 가독성이 좋아지고,
> 
> `ps -ef | grep (찾는 키워드)`옵션을 주면 특정 키워드를 쉽게 찾을 수 있습니다.

### 3. jobs

### 4. kill
