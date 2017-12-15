# AWS-Basic

## WHAT?
+ aws 용어 정리.

## 1. avilityzone
+ aws ec2는 전세계에서 제공된다. 리전별로 각각의 `가용영역` 이라고 알려진 분리된 위치를 여러개를 가지며 각 위치에 리소스등을 배치하여 서비스를 이용하게 한다.
+ 분리된 IDC라고 생각하면 쉽다. 다른 가용역역에서 각종 물리적 천재지변등으로 작동불능이 되더라도 다른 가용영역에서 서비스를 운영할 수 있다.
+ 그러므로 같은 리전안에서 여러 가용영역에 서비스를 올려 분리한다면 보다 안전하게 운영 할 수 있을 것이다.

## 2. VPC(VirtualPrivateCloud)

+ 사용자의 상황에 맞게 여러가지 내부 네트워크를 구성할 수 있다.
+ aws는 기본적으로 1개의 public vpc를 만들어준다. 이 vpc내부에서 추가한 ec2,rdb등이 작동된다. 
+ 기본 서브넷의 인스턴스는 
	- private ipv4 주소, public ipv4 주소를 가진다.
	- private한 주소는 내부에서만 사용할 수 있게되고, public은 인터넷을 통해 외부와 액세스가 가능해 진다.
	- 물론 private 주소도 elastic ip등을 사용하면 유연하게 확장이 가능하다.
	
+ VPC의 IP주소 범위를 정하여 `subnet`을 정할 수 있다.
+ subnet은 말그대로 vpc내부의 특정 ip 대역의 서브 네트워크를 의미한다. 
+ 지정된 subnet을 가지고 aws리소스를 시작할 수 있다.(내부적으로 통신할경우 이러한 private subnet을 사용하여 보다 견고하게 작업할 수 있다.)

+ 아 어렵다.. 네트워크...파이팅..

## REF.
[aws-vpc](http://docs.aws.amazon.com/ko_kr/AmazonVPC/latest/UserGuide/VPC_Introduction.html)