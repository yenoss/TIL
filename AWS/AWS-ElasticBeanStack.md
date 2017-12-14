# ElasticBeanStack

## WHAT?
+ ElasticBeanStack 관찰기.

## 1. ElasticEeanStack 설정.

#### New Environment
+ webServer: 웹서비스
+ worker: SQS로 내부적 워커 구현


#### EnvironmentType
+ configure: 언어설정.
+ environtment type:  single/autoscaling


Application Version

source: upload zip or s3 or sample

#### deployment preference
+ Deployment policy: 배포방식(한번에 업데이트,롤링업데이트..)
+ Healthy threshold: 헬스체크 정도 즉 얼마나 민감하게 헬스체크를 할것이냐
+ Ignore Health check: 헬스체크 무시할지, 아니면 스레시 홀드에 맞게 진행할지.
+ Batch size: 롤링업데이트일경우, 얼만큼의 사이즈로 롤링을 할지 결정, percentage로 혹은 정해진 인스턴스 갯수로 결정

#### Environment Information
+ Environment name: 환경설정 이름
+ Environment url: 환경설정 url 위치, 해당 환경설정이 저장될 위치이다. aws에서 중요한 가용성 부분에 해당한다
+ Description: 상세설명


####  Additional Resource
+ 여기서는 해당 애프리케이션을 위한 인스턴스를 위한 디비를 만들것인지의 여부를 판별하고, 내부 VPC를 구축할것인지 여부를 결정한다. 
+ rds 설정은 크게 복잡하지 않음으로 패스한다

####  Configuration Details
+ instance type: 배포될 instance type
+ EC2 Key: 사용할 ec2키이다
+ email address: 배포사항을 리포팅받을 이메일 주소
+ application healthCheckUrl: 해당 애플리케이션 헬스체크용 url
+ rolling updates type: 어떤 상태에서 롤링 업데이트할지를 결정, 헬스체크기준인가, 시간 기준인가
+ crosszone load  balancing: 다른 가용범위에서도 로드밸런싱 가능하도록
+ connection draining: 로드밸렁싱할때 과거 진행중인 요청을 완료하기위해 유지하는 옵셔
+ connection draining timeout: 위옵션이 유지되는 맥스 시간
+ health Reporting: 헬스체크 보고 타입 디테일하게받기위해서(?) enhanced로 설정
+ rootvolume: 서버 하드 사이즈 

####  Environment Tags
+ 해당 환경설정에서 쓸 기본 key value를 등록







## REF.
[beanstack](https://www.youtube.com/watch?v=L5LDS0vhpZ8)
[beanstack2](http://pyrasis.com/book/TheArtOfAmazonWebServices/Chapter23/04)