# Git-basic

## WHAT?
+ python web framework Django에 대해 이야기합니다.

## 1. Django 프로젝트 Gunicorn으로 구동시키기.

+ env환경에서 pip3로 gunicorn을 설치합니다.

```
. env/bin/activate
pip3 install gunicron
```

+ gunicorn으로 django 서비스를 실행시킵니다.

```
. env/bin/gunicorn --env DJANGO_SETTINGS_MODULE={dir}.settings.dev -w $(( `cat /proc/cpuinfo | grep 'core id' | wc -l` + 1 )) -b 0.0.0.0:3000 {projectname}.wsgi:application 
```

+ 위와 같이  gunicorn을 가상환경에서 실행시키고, 
+ django를 실행시킬 setting 파일과 
+ -w옵션으로 몇개의 프로세스를 돌릴지, 
+ -b옵션으로 몇번포트에서 어떤 프로젝트를 실행할지를 정해준다.

+ 보통 gunicorn을 돌릴땐 코어수*2 +1을 추천한다. 위의 코드는 기본 코어수 + 1로 돌리는 것인데. 이유는 보통 하이퍼스래드로 돌아가서 코어수가 원래갯수에 * 2배로 출력된다는점이 있기 때문에 기존것에 +1을 해두었다 .



## REF.
[git-emptyfolder](https://blog.asamaru.net/2015/09/25/git-tracking-empty-directories/)