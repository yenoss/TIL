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



## 4. zero copy

* 일반적으로 application에서 copy가 일어날경우 4번의 context swtiching이 일어난다. 
  * 이는 보통 성능에 영향을 미치게된다.
  * harddrive -> kenerlbuffer ->user buffer -> socket buffer -> protocol engine 
* swtiching을 최소하 하기 위한 방법이 고안됬다.
* zerocopy 컨셉은 userspace를 최소한 접근해 kernel내부에서 read write하는 것이다.
  * harddrvie kernelbuffer로 카피하고 kurnel buffer에서 socke buffer에게 descriptor를 붙인다.
  * discriptor는 kernelbuffer에 어디영역에 얼마사이즈로 데이터가 있는지에대한 정보를 가지고 있다.
  * 이 정보를 가지고. socketbuffer는 실제 데이터를 protocol engine에게 copy 한다.
* kernel레벨에서 모든것이 끝났음으로 실제 작업이 syscall로 이루어지고 application에서 sendfile하고 protocol에 가피되는 2과정만 진행됨으로 실제 context swtiching은 2번만 일어나게 된다.






## REF

[systemCtl](http://haker.tistory.com/51)

[zerocopy](https://www.linuxjournal.com/article/6345)