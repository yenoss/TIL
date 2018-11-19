## Go

#### Go 언어?

* 켄톰슨, B언어 유닉스 개발자
* 특징
  * 정적타입
  * 컴파일언어
  * GC
  * Concurrency
  * ..

#### 1.1 정적타입, 동적타입

* 자료형을 compile시 결정? => 정적타입
* Runtime시 결정? => 동적타입 (루비,자바스크립트 파이선) 
  * 동적타입인 이유는 Interprinting 언어이기때문



#### 1.2 약타입, 강타입

* weakly type => 값의 타입을 바꿀 수 있다.

* c랭은 약타입 언어임으로 자룧ㅇ이 달라도 암시적 변환

  ```
  int a =1;
  float b = 1.1f;
  float c = a+b;
  ```

* Strongly-typed => 타입을 바꿀수 없음.
* 컴파일,런타임시 자료형이 다르면 에러(Go)

```go
	var a int = 1
    var b float32 = 1.3
    var c float32 = a + b
# command-line-arguments
./main.go:8:23: invalid operation: a + b (mismatched types int and float32)
```





#### 1.3 컴파일/인터프린터언어

#### Go

* 컴파일 언어이면서 네이티브 바이너리 형식 =>  c,c++처럼 완전한 실행팡리을 만듬
* java,c#같은경우 실행파일이아닌 바이트코드,IL를 생성 이 두가지는 가상머신위에서 실행됨. Go언어는 JavaC#과달리 vm이 필요없음.
* IL 에 관한 상세한 정보는 [여기](https://ko.wikipedia.org/wiki/%EA%B3%B5%ED%86%B5_%EC%A4%91%EA%B0%84_%EC%96%B8%EC%96%B4)





#### 1.5 가비지 컬렉션

*  python,ruby,javascript 등도 가상머신에서 가비지 컬렉션기술을 이용.
* Go언어의 가비지 컬렉션은 실행파일안에 있음. 



#### 1.6 병행성

* Concurrency를 제공.
* Parallelism과의 차이는?
  * 병행성:  동시처리의 논리적 개념. 단일 코어에서 스레드를 여러개 생성하면 동시에 여러개로 보이지만 시분할로 실행됨.
  * 병렬성: 동시처리의 물리적개념. 작업을 나누어 CPU 코어에 동시처리
* go는 go키워드로  함수 여러개를 동시에 실행할 수 있음. => 고루틴이라함. 
* 스레드는 운영체제 커널에서 제공하는 리소스 => 생성할수록 부담.
* go는 적정량의 스레드를 생성해 알아서 고루틴을 처리. 또한 최대 프로세서 갯수에 따라 멀티코어도 지원.

* 채널을 통해 고루틴끼리 정보공유.



#### 1.7 컴파일 속도

* c,c++은 헤더파일이 많아 속도가 매우 느림.
* Go는 헤더가 없고 소스코드를 패키지화 하여 변경된 부분만 컴파일함으로 속도가 빠름.

#### 2.1 기본디렉토리 설정

* bin: 소스파일을 컴파일하여 실행파일이 생성되는 디렉터리
* pkg: 패키지를 컴파일하여 라이브러리 파일이 생성되는 디렉터리 
* src:  내가 작성한 소스파일과 인터넷에서 받아온 소스파일이 저장되는 디렉터리
* GOPATH: 설정된 패스를 고 루트페이지로 인식한다.



#### 6 기본문법

* 중괄호는 구문의 맨뒤에서 시작.
* tab을 통한 들여쓰기.

#### 7,8,9 기본문법

~~~go
//타입 생략가능 그러나 무조건 입력해줘야댐
var age = 10

//자료형 입력하면 선언만 가능
var age int

//:=를 사용하면 var와 자료형 키워드를 사용하지 않고 간단히 초기화까지가능
name := "hello" 
//아래와 같이 여러 변수들을 동시에 선언가능
var name = "hello"
var x, y int = 30, 50
var age,name = 10, "vvv"

a,b,c, := 1, 2, false

var (
    x, y int = 10,20
    age, name =  10,"v"
)
//선언만 하고 사용안하면 안됨그러나 아래와같이 _ 에 할당해주면 에러는 안남
	a, b, c := 1, 2, 4
	_ = a
	_ = b
	_ = c
import _ "time"



~~~

* 선언만하고 사용하지 않으면 컴파일 에러가남!

* import패키지를 사용하지 않으면 컴파일 에러가남!

* rune
  * utf-8 문자 코드를 저장할때 사용.

  * '' 작은 따옴표를 이용하여 묶어주어야함.

  * ~~~go
    	var r1 rune = '한'
    	var r2 rune = '\ud55c'
    ~~~

* `unsafe.Sizeof(t)` 는 바이트를 반환.

#### fmt.print vs print

*  print와 같은 경우 stdout이아닌 stderr로 보냄.
* fmt.print는 stdout 으로 보냄.
* print는 간단히 디버그용이고, 실제 프로덕션용 프린트는 fmt를 쓰는게 일반적이고 많은 기능들을 가짐.





### Machine Epsilon?
