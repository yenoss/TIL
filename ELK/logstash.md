# ELK_ISSUE

## WHAT?
+ logStash 사용경험을 이야기합니다.

## 1.logstash conf파일에서 특정 field에서 value를 내부에서 사용하려면?

+ index를 설정할때 특정 필드에 있는 value를 넣어서 만들고싶었다(idnex로 카테고리를 분류하기위해)
+ json 파일이 아래와 같을떄

```
{"log_type":"test01","user_id":123}
```

+ 해당 log_type을 가지고 특정 index를 만드려면

```
index => "%{log_type}"
```

+ 이렇게 하면 index가 test01인 상태로 es에 저장된다.
+ 즉, % {field_name}을 통해 해당 필드의 value를 가져올 수 있다는 이야기다.



## 2.logstash conf파일에서 index에 날자를 넣고싶다면?

+ 로그스태시를 읽어 index에 넣는 날의 날자정보를 넣으려면 아래와같이 하면된다.

`index => "%{index}-%{+YYYY.MM.dd}"`

