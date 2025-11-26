# 오픈소스SW개론 과제 2

## 주제 : 리눅스 명령어 중에서 top, ps, jobs, kill에 대해서 조사해보자.

### 1. top(Table Of Process)

시스템의 프로세스들을 실시간으로 모니터링 할 수 있게 해주는 명령어입니다.

기본 사용법 : 
```bash
top
```
> 화면 구성
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



| 옵션 | 설명 |
|------|-----|
| -n | nnnnn |
| -n | nnnnn |
| -n | nnnnn |
| -n | nnnnn |

### 2. ps

### 3. jobs

### 4. kill
