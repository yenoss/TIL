# Ubuntu

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
* mkisofs
  * 특정 파일 디렉토리를 iso파일로 만들어준다. 
  * 옵션으로 파일명, 이미지이름 윈도우 호환여부 등이 있다.



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



## 5. dfs

* 분산파일시스템. 
* network를 통해 공유되어지는 파일 시스템
* nfs같은 프로토콜이 여기에 속한다. network기반이기에 bandwith가 중요할듯 보인다. 
* server-clieent구조를 가지며 하나이상의 서버가 파일시스템구조를 클라이언트에게 제공하게된다.



## 6. lvm

* logical volume maanager의 약자. 할당받은 파티션을 자유롭게 확장 축소 시켜준다.
* 물리적 볼륨에 논리적 레이어를 얹어 불륨을 동작시킬 수 있다.
* 볼륨그룹이 존재하고 여기에 하드가 매핑되는 형태이며 볼륨그룹에서 관리하게 된다.



## 7. Raid

* 여러개의 하드디스크를 묶어 하나의 디스크를 사용하는것과 같은 방식이다.
* 몇개의 하드가 고장나도 기술적으로 보완가능하다.
* Raid0
  * 하드를 하나로 묶어 동시저장
  * 빠르지만, 고장나면 끝
* Raid1
  * 미러링 하나와 똑같은 저장장치 만들기
  * 안전하지만 비쌈
* Raid5
  * 기존 용량보다 몇개의 하드디스크를 예비용으로 두고 고장나면 대기하고있던 디시크가 붙음
  * 커버가 좀 되나 인접하드가가같이 고장날 수 있음
  * 이 이후레이어 부터는 패리티정보사용으로 복구가가능한레이어
  * 각 디스크에 패리티 체크 정보를 하나씩 가지게 됨.
  * 에러 검출은 xor 방식
    *  1011 xor 0110 => 1101  
    * 두번째  0110이 사라졌다면 1011 과 1101을 가지고 0110을 복구할 수 있게됨. 



## 8. Parity 

* parity check 는 odd/even 두 가지가 있으며
* 오류검출을 아래와 같이 할 수 있다.
  * 짝수 체크 0 0 0 1 (data) + 1 (parity)  패리티 비트를 하나 추가하여 항상 1의 갯수를 짝수로 맞춘다. 
  * 만일 온데이터의  1의 수가 홀수 이면  에러!


## 9. %? (exit code)
* linux 계열은 exit code 라는게 존재한다. [link](https://www.tldp.org/LDP/abs/html/exitcodes.html)
* 실행가능 프로그램이 상위프로세스에게 리턴해주는 코드이다. 
* 위 명령어를 치면 방금전에 종료되었던 프로세스의 exitcode를 출력한다
* consul의 service health chck의 bash 성공여부의 판단 기준은 exicode가 된다. 

## 10. jq 
* Pretty json in command

~~~
sudo apt-get install jq
cat someText.txt | jq .
~~~

## 11.proc
* linux 에서는 process들의 정보를  proc에 모아둔다.  ps도 proc에 있는 내용들을 취합해 보여주는 것.

## REF

[systemCtl](http://haker.tistory.com/51)

[zerocopy](https://www.linuxjournal.com/article/6345)

[raid](https://jerrystyle.tistory.com/56)

[mkiofs](https://idchowto.com/?p=8294)

