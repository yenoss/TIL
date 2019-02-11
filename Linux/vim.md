## Vim

## 1. vim 사용

~~~
sudo vi ~/.vimrc
~~~

* vim 관련 설정파일. 
* 없으면 만들면 됨.

~~~
//자동인텐트
set autoindent
    set cindent
//라인 넘버링
set nu
//탭 사이즈
set ts=4
//자동시프트사이즈
set shiftwidth=4
//파일 수정시 자동 업데이트
set autoread

~~~

* vsplit
  * 창 세로분할
* ctr + w  + arrow 
  * 원하는 방향으로 커서 이동
* ctr + w  and o
  * 해당 창을 전체화면으로 (스플릿 없앰)
* :qa!
  * 여러개떠있는 창 모두제거.

* /{word}
  * 검색. 다음 n  전 N
* u
  * redo