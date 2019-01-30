## Ubuntu

## 1. vi 에서 화살표가 영문자로 타이핑된다면..

* vim ~/.vimrc에서 아래와같이 설정해주면 된다.

~~~ 
set nocompatible 
~~~



## 2. SystemCtl?

* SystemD
  * 최상위 프로세서로 유저레벨에서 최초 실행된다.
  * 실행된 서비스 및 유닛들을 관리
  * PID=1
* Systemctl은 systemD를 관리하는 명령어
  * status: 유닛상태정보
  * is-active: 실행확인
  * start, stop, restart 등의 명령어가 있음.



## 3. Command

* **top**
  - memory cpu 사용량 watch
  - 진보버전(htop)
* **df**
  - 마운트된것 usage로 보기
* **lsblk** 
  - 모든 마운트된것 리스트로 보여주기
* **ctrl + R**
  - 이전에 쳤던 linux명령어 찾아서 바로 실행 할 수 있도록 하기
* **netstat -tnlp**
  * 열린 포트 확인

## REF

[systemCtl](http://haker.tistory.com/51)