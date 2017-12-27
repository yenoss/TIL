# ELK_ISSUE

## WHAT?
+ logStash 사용경험을 이야기합니다.

## 0. Install(logstash 6.0)
+ log stash의 기본 설치사양은 아래와 같다.
+ aws에서라면 free tire에서는 안돌아가고, t2.medium 사양이 최소사양에 해당한다.

```
RAM 4GB, CPU 2
```

#### java7 설치.

```
sudo add-apt-repository -y ppa:webupd8team/java
sudo apt-get update
sudo apt-get -y install oracle-java8-installer
```

####  로그스태시 설치

```
sudo add-apt-repository -y ppa:webupd8team/java
sudo apt-get update
sudo apt-get -y install oracle-java8-installer
```




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


## 3.logstash 에서 txt파일을 읽어보자.
+ logstash의 conf파일은 크게 input/filter/output으로 되어있다.
+ 이 중 input에서 txt파일을 읽는 예는 아래와 같다.


```
input {
	file {
		path => "{dirctory}/log.txt*"
        start_position => beginning
	}
}
```

+ 위와 같이 설정하면 해당디렉토리에서. log.txt 로시작하는 모든 txt파일을 row별로 읽게된다.
+ 이떄 start_position옵션을 주게되는데 이는 어디서부터 해당 로그를 읽을 것인가를 의미한다.
+ beginning => 처음부터읽는다는 의미이다, 단 최초 접근시만 적용되고, 이후로 읽게되면 live stream방식으로 읽기때문에 읽은 이후의 row에 대해서만 로그를 읽어드린다.

+ 필자는 log를 구분하기 쉽게, 용량이슈등에 있어 daily로 저장함으로 log.txt.2017=12-04 파일에서 최초 로그등을 글기위해 위와 같이 패턴을 설정하였다. (실제로 live 데이터만 긁게된다면, log.txt만 긁으면될 것이다.)


##Ref

[logstash-official](https://www.elastic.co/guide/en/logstash/current/installing-logstash.html)

[logstash-startposition](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-file.html#plugins-inputs-file-start_position)

[logstash-install](https://www.digitalocean.com/community/tutorials/how-to-use-logstash-and-kibana-to-centralize-and-visualize-logs-on-ubuntu-14-04)
