# Docker

#### 1.1 가상머신

- VMWare,Hyper-V,Xen,KVM등 가상머신과비슷
- 전가상화(FullVirtualizatin)
  - VMWare Hyper-V 가상화소프트 위에서 게스트OS가 들어감. 즉 게스트os 그대로사용.
  - DOM0를 통해 모든 요청이 Hypervisor로 요청.
  - 전체가상화임으로 드라이버최적화가 관건.
  - 하드웨어 에뮬레이터라고 생각하면 쉬움. VMWare
- 반가상화(Paravirtualization)
  - 게스트OS를 수정해 게스트OS가 가상화됨을 인식하여 하이퍼바이저가 필요할 경우 자동호출되도록함. 
  - 하이퍼바이저를 최소화해 성능향상되지만, 게스트OS가 수정되야되기에 OS소스 코드접근해야함
  - 필요에따라 하이퍼콜 인터페이스를 이용하여 하이퍼바이저에게 요청을 날린다.
  - dom0 os에서 직접 하드웨어 와 드라이버로 붙어있고 나머지 os는 hypercall interface만 가져 콜을 날리는 식.
  - 호스트OS필요 ㄴㄴ
- 하이퍼바이저란 [링크1](https://m.blog.naver.com/PostView.nhn?blogId=jkssleeky&logNo=220766390227&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F) [링크2](http://nitw.tistory.com/179)
  - 호스트컴에서 다수의 os를 동시에 실행시키기위한 논리적 플랫폼
  - 타입1(baremetal)
    - 하드웨어에서 직접실행
    - 호스트OS 필요 ㄴㄴ 하드웨어에서 하이퍼바이저 
    - dom0 os(control)에서 관리
    - xen
  - 타입2
    - 일반프로그램과같이 호스트os에서 실행, 맥에서 virtualbox설치
    - virtualBox,parallels,KVM
    - 물리컴퓨터의하드웨어를 에뮬레이터하는 방식 오버헤드가큼.
  - 하이퍼콜 => 게스트os에서  직접서비스
    - 시스템콜: 어플 -> 커널
    - 하이퍼콜: 게스트os -> 하이퍼바이저

#### Docker?

- GuestOS를 따로 설치하지않고. HostOS에서 OS자원을 호스트와 공유. 
- SystemCall사용([cgroups](https://access.redhat.com/documentation/ko-kr/red_hat_enterprise_linux/6/html/resource_management_guide/ch01)-어느 그룹이 어떤자원을 프로세스로 할당하는 것).
- chroot를 이용해서 내부에 host와 비슷한 환경을 만듦.
- 완벽한 isolation환경을 만드는것 NameSpace



## 1.2 이미지 컨테이너

- 베이스이미지 => 리눅스 배포판(ubuntu)
- 베이스이미지에 필요한 프로그램과 라이브러리를 설치하면 베이스이미지에 바뀐부분만 이미지로 생성하고 실행시 베이스이미지와 합쳐서 실행.
- ubuntu:1.03 에서 nginx를 추가하면 ubuntu:1.03에 nginx 설치부부만 설치되어 새로운 nginx:1.0이미지가 만들어짐
- 컨테이너는 이미지를 실행한 상태. 하나의 이미지로 여러컨테이너 생성가능.