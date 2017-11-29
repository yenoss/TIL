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






## REF.
[python doc](https://ko.wikipedia.org/wiki/Localhost)