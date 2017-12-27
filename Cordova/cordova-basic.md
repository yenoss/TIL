# Cordova-basic

## WHAT?
+ cordova 이슈들에 대해 적습니다.




## 1. Cordova 특정 플러그인이 설치되지 않는다.
+ 코르도바의 특정 플러그인을 설치할경우 아래와 같은 에러를 뱉었다.

```
21367 error code ENOENT
21368 error errno -2
21369 error syscall rename
```

+ 원인은 버전이 맞지않아서 발생하였다. 코르도바를 라이브러리가 워킹하는 버전에 맞도록 맞춰주었다.

```
sudo npm install cordova@6.5.0
```

## 2. Cordova fcm ios 에서 googleService를 찾지 못함.

+ GoogleService-info.plist를 찾을 수 없다는 에러가 발생하였다
+ 해당 파일을 resource파일 아래 복붙하고, 타겟을 꼭 fiflbox 로 설정해줘야한다.


## REF.
[cordova-versioning](https://stackoverflow.com/questions/35190434/cordova-installation-error-path-issue-error-code-enoent)
