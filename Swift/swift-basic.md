# Swift-basic

## WHAT?
+ Swift 문법에 대한 이야기를 적습니다.

## 1.[err] binary operator '*' cannot be applied to operands of type 'Float' and 'Int'

+ 여러 함수에서 여러타입의 function에서 * 연산을 하려고 했는데 위와 같은 에러가 발생했다.

```
scoreToFloat(score.score) * score.credit
```

+ 두 개의 function 모두 return값이 명확히 타입(Float)이 있었지만, 현재 저 상태로 곱하는 과정은 추론 값 * 추론 값 이 됨으로 타입을 명료히 적어주어야 만 

```
(Float)scoreToFloat(score.score) * (FLoat)score.credit
```


#2 swift 3항 연산자
+ 스위프트 3항 연산자는 아래와 같이 사용가능하다

```
{조건} ? {true일 경우} : {false 일경우}
```

+ 이렇게 말이다.

```
creditAverage.isNaN ? "0.0" : String(creditAverage)
```
+ creditAverage가 나눌수없는값으로 나눠지는경우 Nan이 나옴으로 nan인지 여부를 체크해 0.0 아님 string으로 리턴하는 3항 연산자예시이다.


## REF.
