# Filebeat-basic

## WHAT?
+ filebeat 사용경험을 이야기합니다.

## 0. FileBeat?
+ file beat는 각서버의 로그를 로그 aggreater로  보내주는 전달자 역할을 합니다. 
+ 최초 필자는 logstash를 모든 서버에 붙여 search에 붙이려는 과감(?)한 시도를 하게 됩니다. 하지만 logstash가 실행이 너무 무겁고 느리며, 같은 기능(필터,전달과정등..)을 하는 작업들을 모든 서버에서 책임지게 되는것은 비효율적이라는 생각을 하게됩니다.
+ tdagent의 fluentd 같이 가볍고 로그만 전달해주는 기능을 elk 스택과 아름답게 연동할 수 있는것이 바로 filebeat입니다.

#### 설치
+ 도커로 띄우고, 실행시 host와 log를 공유하여 해당 로그를 가져오도록 합니다. 
+ `sudo docker pull docker.elastic.co/beats/filebeat:6.1.1`

#### filebeat 설정
+ conf파일은 filebeat.xml로 만듭니다. 대략 아래와 같습니다.

```
 filebeat.prospectors:
    - type: log
      paths:
         - /home/ubuntu/log.log*
  output.logstash:
     hosts: [ "{ip주소}:5044" ]
```
+ 여러 옵션들이 있겠지만, 간단하게 위와 같습니다. 
+ 해당 paths에 로그를 line by line 으로 아래의 logstash 서버에게 전송합니다. 


#### logstash 설정
+ filebeat에서 온 데이터를 logstash에서 받기위해선 logstash.conf 파일의 input을 수정해야합니다.

```
input {
    beats {
        port => “5044"
    }
}
```

+  일반적으로 input으로 path를 입력하였다면, 위처럼 포트를 지정해주고 로그스태시를 실행합니다. 그렇담 filebeat에서 데이터를 받아 올것입니다.


##Ref
