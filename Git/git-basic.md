# Git-basic

## WHAT?
+ git 사용법에 대해 이야기합니다.

## 1. git에 빈폴더 올리기

+ 깃에 폴더만 올리고싶을때가 있다. 예를 들면 로그 파일을 저장하기위한 폴더가 그러하다.
+ 로그는 올리고 싶지않지만 이로저로 여기저기서 해당경로를 설정해줘야하기 때문이다.
+ 물론 배포과정 전에 해당 폴더를 생성해줘도되지만, 간단히 빈폴더를 올린다.

```
touch .emptys
```

+ 위와 같이 빈폴더 내부에 숨김파일을 하나 만들게 되면 트래킹에 잡히게된다.

## 2. git 특정 브랜치 clone하기

+ `git clone -b {branchname} {repositoryUrl}`








## REF.
[git-emptyfolder](https://blog.asamaru.net/2015/09/25/git-tracking-empty-directories/)