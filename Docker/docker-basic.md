# Docker-basic

## WHAT?
+ docker의 사용법에 대해 이야기 합니다.




## 1. Docker 기본.

#### docker ubuntu image 받기.

```
sudo docker pull ubuntu:16.04 
```

#### docker image 찾기.

```
sudo docker images 
```

#### docker image로 컨테이너 만들어 실행시키기.

```
sudo docker run -i -t --name ubu ubuntu /bin/bash
```
+ -i : interactive 컨테이너와 주고받겠다.
+ -t : pseudo-tty tty를 사용하겠다.(teletypeWriter 콘솔..)
+ --name : 실행 컨테이너 이름
+ 뒤에 이미지이름. 
+ 뒤에 배쉬 실행.

+ -d : daemon 모드, 백그라운드모드로.
+ -p : 포트설정 host와의 포트관계를 결정. ( -p 3000:3000 host 3000에 컨테이너 포트 3000 연결)
+ -v : {hostdirectory}:{contianerdirectory} 설정을주면 두개의 폴더가 sharing된다

+ 위와 같은 옵션으로 아래와 같이 도커에서 간단히 실행 해볼 수 있다.

```
sudo docker run -d -p 3000:3000 fifl
```

+ background 서버 돌려놓기.

#### docker container 보기

```
sudo docker ps
```
+ 현재 실행된 컨테이너 리스트.

```
sudo docker ps -a
```
+ stop된 컨테이너 리스트까지 모두 보여짐.

#### docker image 만들기

+ dockerFile로 image 생성하기.

```
sudo docker build --no-cache  --tag test:0.1 .
```

+ --tag : 이미지의 태그를 설정, 이름만설정하면 latest로 자동설정.
+ --no-cache : 기존에 있는 cache를 사용하지 않고 새롭게 빌드한다.

#### docker repository push

+ docker build할때 이미지파일에 tag를 붙여서 두개를 만든다.

```
sudo docker build  --tag test:latest  {repository}/test:latest
```

+ docker images 를 보 tag된 새로운 이미지가 생기고(이름만다름)
+ 이 상태에서 푸시를 하면

```
sudo docker push {repository}/test:latest
```

+ 실제 도커이미지가 올라갑니다.

#### docker diff
```
docker run -i -t --name test_app {repository}/test:latest /bin/bash
```

+ 실제 도커에 들어가서 이미지를 변경한다.
+ exit 명령어를 통해 나오게되면 다음 변경된 내용을 확인할 수 있다.

```
docker diff {container 이름} or {container hash값} 
```

+ 필자는 test.log라는 파일을 추가해봤다.

```
C /root
A /root/.bash_history
C /user
C /user/src
C /user/src/app
A /user/src/app/test.log
```
+ 위와 같이 변경 내용을 확인할 수 있다.
+ A : 추가된파일
+ C : 변경된파일
+ D : 삭제된파일
+ test.log만 만들었지만 디렉토리가 변경되었므으로 다른것도 영향을 받는다.

#### docker commit
+ 바뀐레파짓토리로 새로운 이미지를 만든다.
```
docker commit {container 이름} {repository}/test:1.0
```
+ 새로운  이미지가 해당 tag에 맞게 만들어질것이다. 이를 푸시한다.

```
docker push {repository}/test:1.0
```


#### docker pull
+ docker를 repository에서 받아보자. 필자는 aws ecs(elastic container service)을 사용하고있다.

```
 aws ecr describe-repositories
 docker pull aws_account_id.dkr.ecr.us-west-2.amazonaws.com/amazonlinux:latest
```

+ 레파짓토리를 확인하고, 해당 레파짓토리에서 image파일을 땡겨오는 코드이다.
+ 간단하지만, 필자는 권한 에러로 매우 느리게 진행되었다.
+ 위의 코드를 실행하기전에 ecs에서 레파짓토리 읽기,쓰기등의 설정을 꼭!! 해줘야하고, 사용자관리 솔루션인 iam에서도 해당 유저의 ecs Acess에 해당하는 권한을 꼭 설정해주어야한다.



## 2. docekr codec Error (Readme read err)

+ 도커 환경에서 python 관련 라이브러리를 건드리다 아래와같은 에러를 만났다.

```
Collecting pyfcm==1.4.3 (from -r requirements.txt (line 24))
  Downloading pyfcm-1.4.3.tar.gz
    Complete output from command python setup.py egg_info:
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-build-2y23iekp/pyfcm/setup.py", line 41, in <module>
        long_description=read('README.rst'),
      File "/tmp/pip-build-2y23iekp/pyfcm/setup.py", line 17, in read
        return open(os.path.join(os.path.dirname(__file__), fname)).read()
      File "/usr/lib/python3.5/encodings/ascii.py", line 26, in decode
        return codecs.ascii_decode(input, self.errors)[0]
    UnicodeDecodeError: 'ascii' codec can't decode byte 0xc2 in position 4157: ordinal not in range(128)

```

+ 보아하니 pyfcm 라이버리에서 README.rst파일을 읽다 ascii값을 디코드 하지 못한다는 에러였다.
+ 도커에서 실행할경우, ubuntu의 기본 locale이 utf8으로 잡혀 있지 않아서 발생하였다.
	+ locale이란  세계각 나라에서 가지고 특징들을(언어,날짜..) 있는 os별 설정에 따라 어떻게 보여줄지를 정해지는 설정이다.
	+ 예로 한국 2017년 1월 1일  출력을, 미국 local로 바꾸면 01/01/2017 로 보여지게된다.


+ 도커의 기본 locale은 아래와 같다.

```
root@269f0ac2522f:/# locale
LANG=
LANGUAGE=
LC_CTYPE="POSIX"
LC_NUMERIC="POSIX"
LC_TIME="POSIX"
LC_COLLATE="POSIX"
LC_MONETARY="POSIX"
LC_MESSAGES="POSIX"
LC_PAPER="POSIX"
LC_NAME="POSIX"
LC_ADDRESS="POSIX"
LC_TELEPHONE="POSIX"
LC_MEASUREMENT="POSIX"
LC_IDENTIFICATION="POSIX"
LC_ALL=

```
+ 즉, 아무것도 설정되어있지 않는 상태


​	
+ 위 라이브러리 설치하기전 아래와같이 ubuntu locale을 아래와 같이 utf8기반으로 바꿔주면된다.

```
RUN apt-get install -y locales
RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  
```


+ 잘 실행되면 아래와 같이 나온다.
```
root@9b65b8fe46f6:# locale
LANG=en_US.UTF-8
LANGUAGE=en_US:en
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=en_US.UTF-8
```



## 3 Docker Proxy Setting

* Version : 18.06

~~~shell

sudo vim /ete/systemd/system/docker.service.d/http-proxy.comf

//아래와같이 설정
[Service]
Environment="HTTP-PROXY={proxyip}/"
Environment="HTTPS-PROXY={proxyip}"
Environment="NO_PROXY=localhost,127.0.0.1"

//아래와 같이 리로드& 확인			
systemctl daemon-reload
systemctl restart docker
systemctl show --property=Environment docker

~~~





## REF.

[aws-ecs](http://docs.aws.amazon.com/ko_kr/AmazonECR/latest/userguide/docker-pull-ecr-image.html)
[locale set](https://github.com/mozilla/unicode-slugify/issues/16)
[locale set2](http://jaredmarkell.com/docker-and-locales/)
[local ?](https://beomi.github.io/2017/07/10/Ubuntu-Locale-to-ko_KR/)

[dockerProxy](https://blog.itanoss.kr/ko/%EC%9A%B0%EB%B6%84%ED%88%AC-16-04%EC%97%90%EC%84%9C-docker-%ED%94%84%EB%A1%9D%EC%8B%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/)