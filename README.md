리눅스 명령어 (top, ps, jobs, kill) & vim 에디터 매크로 사용법
====
### :heavy_check_mark: top : 시스템 프로세스/메모리 사용 현황을 실시간으로 출력 (프로세스 관리도구)
---
:point_right: __실행화면__ 

![다운로드 (1)](https://user-images.githubusercontent.com/104743690/171988366-66d73c56-0a4f-413a-8318-f5c84e638d5e.png)

| top 출력정보||||
|:---:|:---:|:---:|:---:|
| **PID** | 프로세스 ID | **SIHR** | 프로세스가 사용하는 공유 메모리 크기 |
| **USER** | 사용자 계정 | **%CPU** | CPU사용량 |
| **PR** | 우선순위 | **%MEM** | 메모리 사용량 |
| **NI**| Nice값 | **TIME+** | CPU누적이용시간 |
| **VIRT** | 프로세스가 사용하는 가상 메모리 크기  | **COMMAND** | 명령이름 |
| **RES**| 프로레스가 사용하는 메로리 크기 | | |


:point_right: __명령어 종류__

`Enter, Spacebar` : 화면을 다시 출력

`h, ? `: 도움말

` k ` : 프로세스 종료

` n ` : 출력한 프로세스 개수 바꿈

` u ` : 사용자에 따라 정렬

` M ` : 메모리 크기에 따라 정렬

` p ` : CPU 사용량에 따라 정렬

` q ` : top명령종료


### :heavy_check_mark: __ps : 프로세스 목록 보기__
---

#### __ps \[option\]__


:point_right:  __실행화면__ 

![ps](https://user-images.githubusercontent.com/104743690/171987771-15634b7d-e37c-48c1-b482-19aa1854a912.PNG)

* `PID` : 프로세스 번호

* `TTY`: 프로세스가 연결된 터미널




:point_right: __명령어 종류__

||||
|:---:|:---:|:---:|
| -r | 현재 실행중인 프로세서를 보여준다. |
| S  | 20초 미만의 짧게 잠듦(sleep)  |
| D  | 디스크 입출력 대기 인터럽트 할 수 없는 대기 상태 |
| T  | 일시 정지 |
| Z  | 좀비(zombi) 프로세서 |

`좀비상태` : 프로세서가 사라질 때 시그널 처리의 문제로 완전히 소멸되지 못한 상태.




:point_right:  __*필요한 프로세스에 대한 결과를 선택적으로 보고자 할때*__

`-e` : 현재 실행 중인 모든 프로세스 정보 출력

`-f` : 모든 정보 확인

`-a` : 실행중인 전체 사용자의 모든 프로세스 출력

`-u` : 프로세스를 실행하나 사용자와 프로세스 시작 시간 등을 출력

`-x` : 터미널 제어 없이 프로세스 현황 보기 / 실시간으로 터미널에 프로세스가 어떻게 변하는지 보여줌

![캡처](https://user-images.githubusercontent.com/104743690/171989250-f38fabe8-de39-4f0c-a6ca-b67c2bbdb820.PNG)

### :heavy_check_mark: job : 작업의 상태 표시
---
#### __jobs \[option\] \[PID\]__

#####**작업이 중지된 상태 or 백그라운드로 실행되는 작업을 보여주는 명령어**





### :heavy_check_mark: kill : 프로세스 종료
---
#### __kill \[option\] \[PID\]__

:point_right: __명령어 종류__

`-l` : 사용 가능한 시그널 목록을 출력

`-1`(숫자) : 재실행(SIGHUP)

`-9` : 강제종료(SIGKILL) 

`-15` : 정상 종료(SIGTERM) , 작업종료

'signal number' or '옵션'을 지정하지 않으면 기본적으로 작업종료로 사용한다.

![캡처](https://user-images.githubusercontent.com/104743690/171989377-53363431-29de-4781-9de2-c996f3c71c24.PNG)


