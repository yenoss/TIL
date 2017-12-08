# Bash-basic

## WHAT?
+ Bash shell 팁들에 대해 정리합니다.

## 1. 특정 프로세스 삭제했다 다시 실행시키기
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
