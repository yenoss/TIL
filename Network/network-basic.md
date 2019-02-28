# ELK_ISSUE

## WHAT?
+ 네트워크에 대한 기본적인 지식들을 적습니다.

## 1.localhost 란? 
> localhost는 네트워크에서 사용하는 루프백(의도적으로 원래의 장비로돌아가는 것) 호스트명으로 자신의 컴퓨터를 의미한다.

+ IPv4에서는 127.0.0.1과, IPv6에서는 ::1(0:0:0:0:0:0:0:1)과 일맥상통하다. 
+ 127.0.0.1 과 127.255.255.254 까지의 ip 대역대를 모두 자기자신을 나타내는 포트로 가지고 자기자신으로 loop back한다.
+ 이중 localhost는 127.0.0.1을 말한다.



## 2. ARP(Address Resolution Protocol) 란?

* ??
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

* ??
  * 너무 많이 쓰인느 용어

> 서브네트워크. 나와 같은 네트웤인가?

* subnetmask
  * 다른 ip가 나와 같은 network에 있는지 확인 할때 사용함.
  * ip가 172.12.1.1 , subnetmask가 255.255.0.0. 이라면 and  연산을 통한결과가 172.12 이다. => 이는 곧 172.12.x.x로 시작하는 모든 ip는 나와 같은 ip라는것이 된다. 
  * 만약 172.12(A)가 아닌 다른 network  ip를 가진  172.11(B)과 같은 ip를 보게되면 이는 스위치가아닌 라우터를 통해 통신할 수 있다는 의미가 된다.
* default gateway
  * 라우터를 의미한다. 
  * 만약 위에 다른 network ip를 가진 ip(B)와 통신하고싶다면 첫번쨰로 Default Gateway를 가지는 라우터를 통해서 통신해야 된다. 
  * 당연히 이 라우터는 나와 같은 network에 묶여 있게 된다.






## REF.
[wiki_localhost](https://ko.wikipedia.org/wiki/Localhost)

[netmania subnet/gateway](https://www.netmanias.com/ko/?m=view&id=blog&no=5403)