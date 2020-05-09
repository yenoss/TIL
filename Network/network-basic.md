# ELK_ISSUE

## WHAT?
+ 네트워크에 대한 기본적인 지식들을 적습니다.
## 6.bonding 란? 
* 왜?
  * 너무 많이 들어봄.. 
> 여러 네트웤 인터페이스를 묶어 하나의 채널로 사용하는것. 

* linux kernel의 기술로 2개 이상의 network interface card를 하나처럼 사용하게 되는데 이렇게 사용되면 몇 장점 이있다.
   + ha 구성; 하나의 닉카드가 죽어도 bonding되어 있다면 장애에 대응할 수 있다.
   + 대역폭 상승; 1g짜리 4개를 bonding하게 되면 4g짜리 처럼 쓸 수 있다.
 
* 여러가지 모드를 제공한다.
   + mode0 (roud-robin): active/active 모드로 순차적으로 패킷을 분산하고 닉 갯수대로 대역폭 상승을 이론적으로 기대할 수 있다.
   + mode1 (active-backup): slave가 standby상태로 대기하게된다. 
   + mode3,4 도 다양한 방식으로 본딩을 기술적 지원해준다.


## 5.localhost 란? 
> localhost는 네트워크에서 사용하는 루프백(의도적으로 원래의 장비로돌아가는 것) 호스트명으로 자신의 컴퓨터를 의미한다.

+ IPv4에서는 127.0.0.1과, IPv6에서는 ::1(0:0:0:0:0:0:0:1)과 일맥상통하다. 
+ 127.0.0.1 과 127.255.255.254 까지의 ip 대역대를 모두 자기자신을 나타내는 포트로 가지고 자기자신으로 loop back한다.
+ 이중 localhost는 127.0.0.1을 말한다.



## 4. ARP(Address Resolution Protocol) 란?

* 왜?
  *  routing, switch를 보다보니 arp를 통해 통신한다고함.

> IP주소에 해당하는 NIC의 mac주소를 알아내는 프로토콜

* 세부 프로토콜 내용은 조금 복잡하니 [참고](https://yellowh.tistory.com/20)
* 작동과정
  *  연결된 모든 장비에 Request를 보낸다. 
  * ARP request를 받은 장비들은 누구에게 전달된 Request인지 확인하고 해당 destination IP가 본인일경우 Reply를 해준다. 
* ARP Cache Table
  * 매번 Broadcast로 요청을해서 mac을 알아오는 방식은 부하가 너무 크기때문에 한번 알아온 정보를 ARP Table에 일정시간 저장하고 통신하고자하는 목적지 mac 주소가 ARP table에 저장되엉 있다면 저장된 것을 사용한다. 
* 예시
  * arp -a
  * 위 명령어를 사용하면 arp cache된 정보를 확인할 수 있다. 



## 3. SubnetMask, Default Gateway

* 왜?
  * 너무 많이 쓰인 용어

> 서브네트워크. 나와 같은 네트웤인가?

* subnetmask
  * 다른 ip가 나와 같은 network에 있는지 확인 할때 사용함.
  * ip가 172.12.1.1 , subnetmask가 255.255.0.0. 이라면 and  연산을 통한결과가 172.12 이다. => 이는 곧 172.12.x.x로 시작하는 모든 ip는 나와 같은 ip라는것이 된다. 
  * 만약 172.12(A)가 아닌 다른 network  ip를 가진  172.11(B)과 같은 ip를 보게되면 이는 스위치가아닌 라우터를 통해 통신할 수 있다는 의미가 된다.
* default gateway
  * 라우터를 의미한다. 
  * 만약 위에 다른 network ip를 가진 ip(B)와 통신하고싶다면 첫번쨰로 Default Gateway를 가지는 라우터를 통해서 통신해야 된다. 
  * 당연히 이 라우터는 나와 같은 network에 묶여 있게 된다.



## 2. [VirtualNetworking](http://linux.systemv.pe.kr/virtual-networking-in-linux/)

*  왜?
  * vm들은 각각의 네트워크가 존재하는 것처럼 보여야한다. 가상으로 떠있기 때문에… 하지만 실제로는 서버 한대에 묶여있기때문에 내부의 vm끼리의 네트워킹 등을 처리해야할 방법이 필요하다. 
* 해결?
  * 하이퍼자이버내에서 가상의 네트워크를 구축하여 가상의 vm들이 통신되어 실제 물리 네트워킹까지 붙도록해주어야한다.
  * 즉 가상의 네트워크 인터페이스가 설계되어있는 꼴.



## 1. Bridge

- 브릿지는 한카드로 두개의 트래픽을 받고싶을때 사용한다. host,guest network를 연결하여 두개의 네트워크를 하나의 네트워크로 사용할때 쓴다.
- host,guest모두 같은 네트웤을 가지기때문에 호스트가 public ip 를 할당받는일이있어도 동일한 IP대역을 받을 수 있다.





## REF.
[wiki_localhost](https://ko.wikipedia.org/wiki/Localhost)

[netmania subnet/gateway](https://www.netmanias.com/ko/?m=view&id=blog&no=5403)
