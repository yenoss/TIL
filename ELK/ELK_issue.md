# ELK_ISSUE

## WHAT?
+ 경험했던 ELK의 이슈들을 적습니다.


## 1.Search와 Kibana를 붙이는 도중 Kibana의 접속이 실행을 하여도 되지 않는 것을 확인하였다.

+ Kibana의 default serverhost가 localhost로 되어 있었다. localhost라는 말은 내부에서 쓰이는 루프백 호스트명이다. 즉 외부에서는 접근할 수 없다.  
+ localhost 대신 0.0.0.0을 사용하여 외부접근을 대기하는 상태로 실행하였더니 접근되었다.


