# Spring-basic




## 1. WAS(Web Application Server)

#### WAS?

* 웹 애플리케이션이 배포되는 공간.
* html등의 정적파일 전달 => web 서버.
* php,jsp,asp 동적페이지 생성 서버 => WAS.WAC
* 동적 컨텐츠 제공 처리가 목표.
* 작동
  1. 웹서버로 요청을 컨테이너가 받음
  2. web.xml을 통해 servlet쓰레드 생성과 객체 생성 전달.
  3. 컨테이너가 servlet(JAVA EE사양의 일부)호출
  4. 해당 servlet의 스레드에서 해당 작업(post/get)
  5. 컨테이너가 응답객체를 웹서버에 전달하고 작업과정에 필요한 객체들 소멸
* Tomcat..



#### CLASS LOADER

* JVM이 클래스를 실행하기 위해 클래스를 로딩하는 과정을 해주는 것.
* 특징
  * 계층적.
  * 위임 가능.
  * 가시적규약.(로딩가능한 범위 존재)
  * 언로딩 불가능.
    * 가비지 컬렉터나 was 재시작 할때 초기화됨
* 유형
  * Bootstrap class loader.
    * JVM런타임 실행을 위해.
    * rt.jar와 연관.
      * Java Runtime Environment를 위한 모든 컴파일된 파일들 클래스들을 포함함. 
  * Extension class loader.
    * 로딩이 끝나면 ExtensionClass loader가 Object객체를 포함 자바 API를 로드하게됨.
  * System class loader.
    * JVM 구현관련 클래스들을 포함한다.
    * classpath 환경변수 등에서 찾은 파일들을 로드한다.
  * User-defined class loader.( 개발자 정의)



#### war?

* WebApplication Archive. 웹 패키징.
* wac가 war의 web-inf폴더로 클래스 파일들을 로드함.
* 상세
  * dcontent directory(html..css..)
  * web-inf(web.xml)
  * classes
  * libs(jar)



#### Webapplication calss loader

* 웹 어플리케이션 자체 api제공을 위한 클래스 로더 와
* 사용자의 JSP, War파일들을 다루기위한 ServletContext loader를 사용.
* ServlectContext -> ServletContainer -> SystemCalss loader 계층.
* Web-Inf/classes파일들 로딩 후 INF/libs에 있는 jar파일들 로드.



## 2. Spring

* 엔터프라이즈 개발을 편하게 해주는 애플리케이션 프레임워크.



#### IOC(Inversion of Control)

* 애플리케이션 자체가 라이프 사이클을 가지지 않고, Framework가 주된 라이프 사이클을 가지고 필요에 따라 애플리케이션 코드를 호출하는 것.
* 일반적인경우(애플리케이션이 컨트롤은 가짐)와 다르기때문에 IOC와 같은 용어가 생김.
* 객체에 대한 제어, 생성, 소멸등의 모든것을 framework내의 container가 하게되는 것임.
* 인터페이스 기반 설계가 가능하고, 체계적이고 효율적인 의존성관리가 된다.



## DI(Dependency Injection)

* IOC를 함에따라 framework가 객체를 컨트롤하게되는데 그렇게 하기위해선   객체 사이의 의존관계를 등록(주입) 해주어야한다.

* 간단한 service 예제.

  ~~~java
  class WorkService{
  	WorkManager workManager;
      void setWorkManager(WorkManager workManager){
          this.workManager = workManager;
      }
      void callBos(){
          this.workManager.callBos();
      }
  }
  ~~~

  ```java
  class main{
  	WorkService workService = new WorkService()
  	WorkManager boss =new WorkManager()
  	workService.setWorkManager(boss)
      workService.callBos();
  }
  ```

  * 위와 같은 코드를 보면 workservice에 workmanager를 등록(주입) 해서 service가 workmanager에 대한 객체를 받아 해당 객체를 다룬다.

* Spring에서는 위의과정을 Bean을 통해 처리한다. 

* applicationContext.xml에서의 설정을 아래와 같이 하게되면

~~~java
<?xml>
<bean id="myWorkService" class="basic.WorkService">
	<property name="workmanager">
		<ref bean = "boss">
	</property>
</bean>
~~~

~~~java
class springApp{
    ...
	WorkService workService = context.getBean("MyWorkService",WorkService.class);
    workService.callBoss();
	...
}
~~~

* setWorkManager를  new를 통해 등록했던것을 똑같이 구현할 수 있다.
* Bean을 이용하여 의존성 주입을 대신해주게 되는 것이다. 더 많은 new해야 할 것들이 있다면 이와같이 bean의 등록하는 것만으로 주입을 할 수 있다.
* 현재 이와같은 방식을  `autowired` annotation을 붙임으로 좀더 쉽게 구현할 수있다.
* 생성과 소멸이 프레임웤에서 관리됨으로 생명주기 제어를 이해 `onCreated()`,`onDestroyed()`와 같은 method를 제공해 준다.



## REF.

[rt.jar?](https://stackoverflow.com/questions/5073967/what-is-the-use-of-rt-jar-file-in-java)

[class-loaders](https://www.baeldung.com/java-classloaders)

[IOC](https://jongmin92.github.io/2018/05/20/Spring/toby-8/)

[IOC2](https://jongmin92.github.io/2018/02/11/Spring/spring-ioc-di/)