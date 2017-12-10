# Swift-basic

## WHAT?
+ Swift 문법에 대한 이야기를 적습니다.

## 1.[err] binary operator '*' cannot be applied to operands of type 'Float' and 'Int'

+ 여러 함수에서 여러타입의 function에서 * 연산을 하려고 했는데 위와 같은 에러가 발생했다.

```
scoreToFloat(score.score) * score.credit
```

+ 두 개의 function 모두 return값이 명확히 타입이 있었지만, 현재 저 상태로 곱하는 과정은 명시적 상태의 값 * 명시적 상태의 값 이 됨으로 타입을 명료히 적어주어야 한다.

```
(Float)scoreToFloat(score.score) * (FLoat)score.credit
```







## REF.
