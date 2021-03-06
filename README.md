리눅스 명령어 (top, ps, jobs, kill) & vim 에디터 매크로 사용법
====
### :heavy_check_mark: top : 시스템 프로세스/메모리 사용 현황을 실시간으로 출력 (프로세스 관리도구)
---
* 시스템의 상태를 전반적으로 가장 빠르게 파악 가능 (CPU, Memory, Process)
* 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌.

:point_right: __실행화면__ 

![image](https://user-images.githubusercontent.com/104743690/171988366-66d73c56-0a4f-413a-8318-f5c84e638d5e.png)

| top 출력정보||||
|:---:|:---:|:---:|:---:|
| **PID** |  프로세스 ID | **SIHR** | 프로세스가 사용하는 공유 메모리 크기 |
| **USER** | 사용자 계정 | **%CPU** | CPU사용량 |
| **PR** | 우선순위 | **%MEM** | 메모리 사용량 |
| **NI**| Nice값 | **TIME+** | CPU누적이용시간 |
| **VIRT** | 프로세스가 사용하는 가상 메모리 크기  | **COMMAND** | 명령이름 |
| **RES**| 프로레스가 사용하는 메모리 크기 | | |

:point_right: __프로세스 상태__

|||
|:---:|:---:|
| R | 실행 중(CPU 자원을 소모)
| S  | 20초 미만의 짧게 잠듦(sleep)  |
| D  | 디스크 입출력 대기 인터럽트 할 수 없는 대기 상태 |
| T  | 일시 정지 |
| Z  | 좀비(zombi) 프로세서 |

`좀비상태` : 프로세서가 사라질 때 시그널 처리의 문제로 완전히 소멸되지 못한 상태.

:point_right: __명령어 종류__

`Enter, Spacebar` : 화면을 다시 출력

`h, ? `: 도움말

` k ` : 프로세스 종료, kill. k 입력 후 PID번호 작성. (

` n ` : 출력한 프로세스 개수 바꿈

` u ` : 사용자에 따라 정렬

` shift + p ` : CPU 사용량에 따라 내림차순 정렬

` shift + m ` : 메모리 사용률 내림차순

` shift + t ` : 프로세스가 돌아가고 있는 시간 순

` a ` : 메모리 사용량에 따라 정렬

` b ` : Batch 모드로 작동
 
 `1` : CPU Core별로 사용량 보여줌.
 
` q ` : top명령종료

***ps 와 top의 차이점***
* ps는 ps한 시점에 proc에서 검색한 cpu 사용량
* top은 proc에서 일정 주기로 합산해 cpu 사용율 


---
### :heavy_check_mark: __ps : 프로세스 목록 보기__
---

#### ⛤ __ps \[option\]__


:point_right:  __실행화면__ 

![image](https://user-images.githubusercontent.com/104743690/171987771-15634b7d-e37c-48c1-b482-19aa1854a912.PNG)

* `PID` : 프로세스 번호

* `TTY`: 프로세스가 연결된 터미널




:point_right: __옵션 종류__

`-A, -e` : 모든 프로세스 출력

`a` : 다른 사용자의 프로세서도 출력

`-a` : 세션 리더 빼고 출력

`-r` : 현재 실행중인 프로세서만 출력

`-h` : 헤더 

:point_right:  __*필요한 프로세스에 대한 결과를 선택적으로 보고자 할때*__

`-e` : 현재 실행 중인 모든 프로세스 정보 출력

`-f` : 모든 정보 확인

`-a` : 실행중인 전체 사용자의 모든 프로세스 출력

`-u` : 프로세스를 실행하나 사용자와 프로세스 시작 시간 등을 출력

`-x` : 터미널 제어 없이 프로세스 현황 보기 / 실시간으로 터미널에 프로세스가 어떻게 변하는지 보여줌

![image](https://user-images.githubusercontent.com/104743690/171989250-f38fabe8-de39-4f0c-a6ca-b67c2bbdb820.PNG)

```
$ ps ax  #시스템에 동작중인 모든프로세스를 보고 싶을 때, BSD포맷으로 출력됨.
$ ps aux  #시스템에 동작중인 모든 프로세스를 소유자 정보와 함께 다양한 정보출력.
$ ps aux | grep apache  # 특정프로세스에 대해 보고싶을 때.
$ ps -ef | more  # 'ps -ef' 시스템에 동작중인 모든 프로세스를 full format(자세히)출력함. more= 한페이지씩 화면에 출력.
```

---
### :heavy_check_mark: job : 작업의 상태 표시
---
#### ⛤ __jobs \[option\] \[PID\]__

##### **작업이 중지된 상태 or 백그라운드로 실행되는 작업을 보여주는 명령어**

:point_right: __특징__
 * 각각의 터미널 마다 jobs는 따로 존재
 * jobs 또한 kill을 통해 종료 가능

:point_right: __실행화면__ 

![image](https://user-images.githubusercontent.com/104743690/171989930-1ac54fba-39cf-49f0-992b-922bcaf9f8cf.PNG)

|job의 출력상태||
|:---:|:---:|
| Running | 작업이 계속 진행중임 |
| Done |  작업이 완료되어 0을 반환 |
| Stopped | 작업이 일시 중단 |
| Stopped (SIGTSTP or SIGSTOP or SIGTTIN or SIGTTOU) | (....) 시그널이 작업을 일시 중단 |

* `jobs %(번호)` :  해당번호 작업정보 출력 ( 중지 or 백그라운드에 돌고 싶은 작업이 있을 때 사용)
* `+` : 현재 실행되고 있는 or 실행예정
* `-` : 현재 진행중인 job이 끝나면 바로 다음에 수행될 프로세스

:point_right: __옵션 종류__

`-ㅣ` : 프로세스 그룹 ID를 state 필드 앞에 출력

`-n` : 프로세스 그룹 중에 대표 프로세스 ID를 출력

`-p` : 각 프로세스 ID에 대해 한 행씩 출력

 `command` : 지정한 명령어를 실행


---
### :heavy_check_mark: kill : 프로세스 종료
---
#### ⛤ __kill \[option\] \[PID\]__

:point_right: __옵션 & signal number 종류__

`-l` : 사용 가능한 시그널 목록을 출력

`-1`(숫자) : 재실행(SIGHUP)

`-9` : 강제종료(SIGKILL) 

`-15` : 정상 종료(SIGTERM) , 작업종료

'signal number' or '옵션'을 지정하지 않으면 기본적으로 작업종료로 사용한다.

![image](https://user-images.githubusercontent.com/104743690/171989377-53363431-29de-4781-9de2-c996f3c71c24.PNG)

---
### :ballot_box_with_check: vim 에디터 매크로 사용법
---

- 사전 조건 : \[Normal/Command 모드\]
- 매크로가 저장될 register 주소(매크로명) = a ~ z 사용 가능.

### :small_blue_diamond: **매크로 기록**

**명령어 형태: q <저장할 매크로명>**

**동작 수행**
```
* qA -> 매크로 작성 -> q (A 문자에매크로 내용 기록)
* q로 시작해서 q로 끝남.
```
레코딩 끝난 후 기록된 내용을 보려면 **reg**명령어 이용. 
ex) `:reg A`

### :small_blue_diamond: **매크로 실행**
1) 특정 문자에 저장한 매크로 실행   **@ \< 저장한 매크로 문자\ >**
2) 매크로 반복실행   **반복횟수@ \< 저장한 매크로 문자\ >**
3) 마지막에 수행한 매크로 실행   **@@**

ex) `3qA  #3회 반복 실행`

### :small_blue_diamond: **매크로 편집**
* 현재 커서 위치에 기록된 매크로 내용 표시.

` "Ap `

* 출력된 매크로 내용에서 작업 수정 / 추가 등을 한 후 편집한 내용 다시 등록.

`"Ayy `

### :small_blue_diamond: **매크로 저장**

작성한 매크로를 저장해서 계속 재사용하기 위해 보통 VIM설정 파일에 기록해 둔다.

1) 현재 편집중 내용을 저장 후 **vim 설정 파일**열기 (:e / :r) - 사용하는 vim종류 등에 따라
```
 :w
 :e ~/.vimrc (설정파일)
```
2) insert모드 전환 후 저장할 매크로 이름을 변수로 하여 사용한 매크로 저장하기
```
i/a
let @<변수명>='ctrl+r ctrl+r <마지막사용 매크로문자>'
:wq! or :x
```


