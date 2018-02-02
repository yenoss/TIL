# BetterCode

## WHAT?
+ 코드 작성, 명명 팁등을 적습니다.


## 시작.

+ 특정한 단어를 올바르게 상황에 맞게 정해야한다.

```
//다운로드해서 가져오는 것이라면..
getPage() => downloadPage() 

//무엇을 수행하는지 안정해져있고, Resume이 있다면  Pause같은것이 더 좋다.
stop() 
```

+ tmp등의 무의미한 이름을 함부로 사용해선 안된다.
```
//scope에 따라 달라질 수 있지만 일반적으로 좋지 않다.
// 다만 4~5줄의 작은 코드내에서 빠르게 변수를 파악할 수 있다면 괜찮다고본다.
var tmp; 
var m;
```

+ 단위를 포함하자. 특정 정보를 부과하자.

```
//시작 시간이지만 단위를 이용해 시간이라는 정보를 구체적으로 줄수있다.
var start_time; => var start_ms 

//utf8으로 인코딩되었다면 아래와 같은 코드도 나쁘진 않아보인다.
var data_utf8;
```

+ 경계를 포함배제는 나눠서 사용하자

```
//12345의 배열에서 모두를 포함할경우
getRange(first,last); 

//12345의 배열에서  마지막을 포함하지 않을경우
getRange( begin,end); 

```

+ boolean변수는 긍정으로 넣는 편이 읽기 좋다.

```
//인증하였는가.
var is_auth = true;

//ssl사용여부.
var use_ssl = true;
```

+ 기본시그널을 주석으로 잘 사용해라.
+ 중요한건 코드를 읽는 사람 입장에서 생각해서 작성하라.

```
TODO:
FIXME:
HACK: 아름답지않은 해결.
XXX: 위험하다.
```

+ 함수의 동작을 명확히 설명해라. 이해하기 어렵다면 예를 추가해라.

```
// 파일안의 새줄을 판단하는 \n이 몇개인지 센다.
int countLines(String filename)
```

+ 삼항연산자는 좋은가?
	+  매번 고민되는 이슈.. 가끔 나도 삼항연산자를 쓰는데.. if else보다 간결하면서 한번에 읽을 수 있을때 사용한다. 
	+  즉, 너무 복잡한 구문을 한줄로 쓰려고하면 그것은 오히려 가독서을 헤침으로 별루인 듯하다.


+ 상태를 설정할 수 있는가?
	+ 어떠한 변수를 정할때 해당 변수를 보다 명확히 하기위해 새롭게 선언하는 경우가 있다.
	+ 이는 같은스코프내에서 효과적으로(한번에) 변수를 이해하고 사용하기 위함이다.


```
//아래와 같이  request.user를 하나의 유저로 할당하는 식이다.
var user = request.user
if(user) {

//아래와 같이 불리언으로 설정해 둘수도있다.
var isCenterId = (request.user.id  == center.id)
```



## REF.
[cordova-versioning](https://stackoverflow.com/questions/35190434/cordova-installation-error-path-issue-error-code-enoent)
