# Bash-basic

## WHAT?
+ Bash shell 팁들에 대해 정리합니다.

## 1. 특정 프로세스 삭제했다 다시 실행시키기.
+ 단순 프로세스로 서버를 백그라운드에서 돌릴 경우. 기존에 돌아가던 서버를 죽이고 새로운 서버를 띄워야 할 때가 있다.
+ run_server.sh란 서버 실행 스크립트가 있을떄. 아래와 같이 shell script를 작성해준다.

```
. env/bin/activate 
SERVER=$(ps -ef | grep ' 0.0.0.0:22051'| wc -l) 
#만약 위와 같은 프로세르르 가진 서버가 2개이상존재한다면
#삭제하고 런.
if [ $SERVER -ge 2 ]
then
    echo [remove] server 22051
    pkill -9 -ef ' 0.0.0.0:22051'
fi
echo [start] server 22051
nohup bash run_server.sh &> /dev/null &
```

## 2. 파일 카피에서 특정 폴더를 제외하기.
+ gitignore하듯 특정 파일을 제외하고 카피해야할 경우가 있다.
+ 이럴경우 `rsync`를 사용하면 된다.

```
rsync -av --exclude='/home/ubuntu/fiflbox/playground/test' /home/ubuntu/fiflbox/playground/ /home/ubuntu/fiflbox/test
```

+ 위와같이 av옵션을 주고 제외할 파일 옵션에 제외할 파일 그리고 source destination 순으로 입력하면 제외되는 파일을 빼고 카피가 가능하다.

+ -v: verbose(상세내용 출력)
+ -a: archiv(심볼릭, 그룹권한등 모든것을 복사)


## 3. java8설치할경우  script로 license 승인하기
+ java8 뿐아니라, mysql등 다양한 경우에 스크립트로 키보드의 역할을 대신해야할 경우가있다.
+ 이번경우는 java8의 라이센스를 승인을 스크립트로 yes하는 코드이다.
+ apt 설치전 아래와같이 echo로 명령어를 설정해두면된다.

```
echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | sudo debconf-set-selections
```

+  | : 왼쪽 출력을 오른쪽으로 파이핑해라.( 복수의 명령어를 결합)
+  debconf-set-selections : 미리설정파일. 사용자가 debconf응답(여기선 라이센스)에대 사전에 응답을 정하는것
##REF
[rsync](https://stackoverflow.com/questions/2193584/copy-folder-recursively-excluding-some-folders)

[piping](http://mwultong.blogspot.com/2006/07/redirection-piping.html)

[devconf](http://manpages.ubuntu.com/manpages/trusty/man1/debconf-set-selections.1.html)
[devconf2](https://docs.openstack.org/liberty/ko_KR/install-guide-rdo/debconf/debconf-concepts.html)