# Deploy-basic

## WHAT?
+ 배포하는 과정에서 겪은 것들을 이야기합니다.

## 1. git으로 배포할때 주의할 점.
+ git으로 서비스 배포할 경우 일반적으로 git의 개인키를 만들어 놓아서 해당 서버에서 바로 새로운 코드를 받아 실행하게된다.

+ 서버로 로그인하여 들어가서 풀을 하면 잘되지만 jenkins + openssh-publisher를 이용해 들어가 풀을 요청하면 권환이 거절되는 것을 볼 수 있다. (아마 open-ssh로 들어가는 유저의 권한 문제일것이다)
`sshkey permission denyied`

+ 위 와같은 이슈가 생길경우 ssh-agent 에  실제 키를 추가해주어야 한다

```
eval ssh-agent -s
ssh-add ~/.ssh/bitbucket_key
```

+ 이렇게 설정을한후 다시 pull을 땡겨보면 키를 이용해 해당 소스를 받아오는 것을 확인 할 수 있다.

+ !! 배포시 위 와 같이 소스의 디펜더시가 키에 달려있는 것은 좋은 배포방법은 아닐것이다. 서버가 독립적으로 실행되는데 걸림돌이 될 수 있기 때문이다. 

## 2. superviosrd not daemonize
+ docker로 서버요청을 받기위해선 docker에서 해당 서버포트를 물고(?:listen하도록) 있어야한다. 
+ 일반적인 아래와 같은 명령어를 쓰게 되면  daemon모드라 도커에 port로 잡히지 않는다. 

```CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/fifl-box-api-live.conf"`
```

+ 이럴땐 -n 옵션을 사용하면 된다.

```
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/fifl-box-api-live.conf","-n"]
```

## REF.
