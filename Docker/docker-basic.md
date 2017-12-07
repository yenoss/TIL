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
sudo docker build  --tag test:0.1 .
```

+ --tag : 이미지의 태그를 설정, 이름만설정하면 latest로 자동설정.

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





## REF.
