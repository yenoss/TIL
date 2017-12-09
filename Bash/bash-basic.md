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

##REF
[rsync](https://stackoverflow.com/questions/2193584/copy-folder-recursively-excluding-some-folders)