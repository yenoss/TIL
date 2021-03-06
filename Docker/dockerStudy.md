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



### 4. Dockerfile

* VOLUME: 호스트에 내용 연결하면서 올리기

* chown -R [user:group] target : 그룹과 유저를 설정해주고 해당 폴더에 할당해준다 nginx폴더에  유저인 www-data가 되도록하는 과정



### 6. Docker registry image

* 도커의  레지스트리 이미지를 이미지로 받아온다.
  * `sudo docker pull registry:latest`
  * `sudo docker run -d -p 3000:3000 --name regitry -v /tmp/regitry:/tmp/regitry regitry`
  * 이미지를 컨터이너로 실행했다.

* `sudo docker push {regiturl}/{image}:{tag}` 와 같은 형식으로 올리면됨.

* sudo docker pull {regiturl}/{image}:{tag}로 다시받아올 수 있음.





### 7. DockerFiles

### run

* Run <명령어>  
* Run [실행파일, 매개변수1,2,] 형식.
  * RUN["apt-get","install","-y","nginx"]
  * RUN["docker", "--help"] 
* 기본적으로 DockerFiles들은 캐시된 결과를 사용함으로 캐시 데이터를 사용하지 않으려면 docker build시 `--no-cache`명령어 사용.



### CMD

* 컨테이너가 시잭되었을때 실행하는 명령

* from에서 이미지에 폼한된 bash실행파일이 있을경우. 그냥 명령어 바로 입력.

  * `CMD touch /home/heool/heool.txt`

* 쉘없이 바로실행할경우

  - `CMD["redis-server"]`



## Entry Point

* docker run , start 명령으로 컨테이너가 생성 혹은 정지된 컨테이너가 시작될때 실행됨. 
* 사용법은 위의 Run,Cmd와 같음.



## ENV

* 환경변수 설정. 
* RUN,CMD,ENTRYPOINT 에 모두 이용할 수있음.

```shell
ENV NAME 1234
CMD echo $NAME
```



## ADD&COPY

* 모두 이미지에 파일을 올리는 방식.
* copy는 add와 달리 URL방식의 파일을 등록할 수 없고, tar파일을 압축한 상태로 등록.





## VOLUME

* 컨테이너 특정 영역 저장내용을 호스트에 저장하도록 함.
* `VOLUME /data VOLUME ["/data","var/log/hello"]` 
  * 첫번째 볼륨은 호스트, 두번쨰 볼륨은 컨테이너 디렉터리 를 함.
* 볼륨은 선언만해주는것이고 실제 run할때 -v옵션으로 디렉터리를 연결해주어야 함.





##  On Build

* 후에 현재 이미지가 다른 이미지의 from으로 사용될 경우 실해되는 명령어.
* `ONBUILD RUN touch /hello.txt`