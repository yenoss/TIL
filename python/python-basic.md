# ELK_ISSUE

## WHAT?
+ python 기본 문법 or 함수등에 대해 이야기합니다.

## 1. json encodeing

+ json을 import한 후 dumps method를 이용한다.

```
import json
dict = {"key":"value","key2":123}
json_dict = json.dumps(dict)
```

+ 여기서 띄어쓰기,공백 없이 출력하려면 separators 옵션을 추가해준다.

```
json_dict = json.dumps(dict,seperators(',',':'))
```

+ compact하게 결과가 리턴된다.


## 2. json decoding

+ json을 import한 후 loads method를 이용한다.

```
import json
json = {"key":"value","key2":123}
dict = json.loads(dict)
```
+ dictionary타입으로 디코딩된다.



## 3. List remove

+ for loop에서 remove연산시 생각과는 다른 결과를 발견했다.

```
somelist = range(10)
for x in somelist:
		somelist.remove(x)
somelist
```

+ 언뜻보면 somelist는 빈배열이 나와야될것 같아보인다. 하지만 결과는 [1,3,5,7,9]의 배열이 나온다.
+ 코드를 자세히 보면 답이나온다.

```
for x in somelist:
print(x)
somelist.remove(x)
print(somelist)

0
[1, 2, 3, 4, 5, 6, 7, 8, 9]
2
[1, 3, 4, 5, 6, 7, 8, 9]
4
[1, 3, 5, 6, 7, 8, 9]
6
[1, 3, 5, 7, 8, 9]
8
[1, 3, 5, 7, 9]

```

+ 프린트 찍힌것처럼 somelist의 원본을 remove하였음으로, 1번째 루프가 돈 다음(x=0) 2번째 루프가 돌경우, 1번째 리스트원소값인 2가 x가 되어, 2를 삭제하게되고, 마찬가지로 다음 루프들도 같이 기존 리스트원소값의 변형된 리스트에서 루프가 동작함으로 위와 같이 의도하지 않은 결과가 나오게된다.
+ 이를 해결하기 위해서 원본 리스트는 그대로 놔두고, 카피된 리스트로 for loop를 돌아주면된다.


```
somelist = range(10)
for x in somelist[:]:
		somelist.remove(x)
somelist
```
+ 위와 같이 slice([:])를 이용하면 새로운 배열을 리턴함으로 기존 somelist와는 다른 배열에서 for loop를 돌게 된다.








## REF.
[python doc](https://ko.wikipedia.org/wiki/Localhost)
[python for](https://stackoverflow.com/questions/1207406/remove-items-from-a-list-while-iterating)