## GO-setting

#### 1.vscode go 설정이 안됨.

* vscode go github에서 다운.
* extension에서 해당 파일 업로드.
* goPath[설정](http://blog.naver.com/PostView.nhn?blogId=pid011&logNo=220771635153&redirect=Dlog&widgetTypeCall=true)

* Err `cannot find delve debugger`
  * go get github.com/derekparker/delve/cmd/dlv
* `go env` 를 통해 현재 go setting을 확인할 수 있음



#### 2. go get명령어등이 timeout 날경우

* proxy 설정이 필요한경우 go get 명령을 날릴때 아래와 같이 실행하면 된다.
  * `http_proxy=127.0.0.1:8080 go get {패키지 다운로드 주소}`
* 귀찮다면 알리아스!
  * `alias go = 'http_proxy=127.0.0.1:8080 go'`



#### 3.  Dep으로 의존성 관리

* python에 pip가 있다면 go에는 dep이 있다.
* 설치

  * `sudo apt-get install dep`

* 패키지 추가

  * `dep ensure -add github.com/go-sql-driver/mysql`

  * gopkg.lock에 아래와 같이 생성

    * ~~~shell
      [[projects]]
        name = "github.com/go-sql-driver/mysql"
        packages = ["."]
        revision = "72cd26f257d44c1114970e19afddcd812016007e"
        version = "v1.4.1"
      ~~~

* 패키지리스트 전체 설치

  * `dep ensure`	
  * vendor 폴더에 모든 패키지가 설치된다.

## REF

[go-run-err](http://gaiserne.tistory.com/226)

[go-proxy](https://stackoverflow.com/questions/10383299/how-do-i-configure-go-to-use-a-proxy)

[dep](https://golang.github.io/dep/docs/new-project.html)