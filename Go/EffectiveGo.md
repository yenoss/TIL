#### 

#  Effective Go



   * [Effective Go](#effective-go)
      * [Names](#names)
         * [Package names](#package-names)
         * [Getter](#getter)
         * [Inerface names](#inerface-names)
      * [SemiColons](#semicolons)
      * [Control strcutures](#control-strcutures)
         * [if](#if)
         * [Redeclaration and reassignment](#redeclaration-and-reassignment)
         * [For](#for)
         * [Switch](#switch)
      * [Functions](#functions)
         * [Mutliple return valuse](#mutliple-return-valuse)
         * [Named result parameters](#named-result-parameters)
         * [Defer](#defer)
      * [REF](#ref)


## Names

### Package names

* 좋은패키지 이름은: 짧고, 명확하고, 기억나기 좋도록. 
* 편의성을위해: 소문자로 싱글단어가 괜찮다. underscore, mixedCap 은 지양.
* 모든소스에서 고유할필요는 없다. 로컬에서 바꿀수도 있으니까.
* 예를 보자
  * buffered reader는 bufio 패키지의 Reader를 콜한다. bufReader가아니라.  bufio.Reader가 더 명확하기 때문.
  * once.Do, No once.DoOrWaituntilDone()

### Getter

* 자동제공하진 않지만 적절히 사용하는것은 좋다. 그러나 이름에 get을 넣거나 하는건 너무 관용적임. 
* Owner를 get하려면 getowner 보다 owner를 걍 사용해라.

~~~go
owner := obj.Owner()
if owner != user {
    obj.SetOwner(user)
}
~~~



### Inerface names

* er suffix 를 사용해라. 
  * Reader,Writer,Formatter,CloseNotifier ..
  * 다만 read,write와같은 signature 이름을 피해라





## SemiColons

* go는 인터프린팅될때 규칙에 의해 세미콜론을 자동으로 붙임.

* 개행전에 마지막 토큰이 식별자(int, string)인 경우, 숫자 또는 문자열 상수와 같은 기본 토큰중 하나 일때 붙임.

  * break continue fallthrough return += --

* 토큰뒤에는 항상 세미콜론을 붙이게됨.



  > if new line comes after atoken that could end a statement, insert a semicolon



* brace closing될때도 바로 붙게됨. 
* 여러줄을 나눠줘야할 경우에만 세미콜론을 붙이게됨.
  * if data,err = getData().Error ; err!=nil { 



## Control strcutures



### if

```go
if x >0 {
    return y
}

if err := file.Chmod(0554); err != nil {
    log.Print(err)
    return err
}
```

* 에러처리는 위와 같이 필요에따라 else 없이 하는 것이 좋음.



### Redeclaration and reassignment

```go
	f, err := os.Open("data")
	d, err := f.Stat()
```

* err는 위에서 사용되고 아래에 새로운 값으로 쓰임.



### For

~~~go
sum := 0
for i := 0; i < 10; i++ {
    sum += i
}

for key, value := range oldMap {
    newMap[key] = value
}

a := []int{1, 2, 3}
for i, j := 0, len(a)-1; i < j; i, j = i+1, j-1 {
    a[i], a[j] = a[j], a[i]
}

~~~



* 대부분 일반 스크립트 언어와 비슷한데 마지막 코드는  multiple일 경우 ++ 대신 +1 -1 을 사용해야됨. 
* ++등은 명령문이기 때문에 라는데 잘 모르겠음.



### Switch

* if else 체인 느낌식으로 사용.

~~~
func unhex(c byte) byte {
    switch {
    case '0' <= c && c <= '9':
        return c - '0'
    case 'a' <= c && c <= 'f':
        return c - 'a' + 10
    case 'A' <= c && c <= 'F':
        return c - 'A' + 10
    }
    return 0
}
~~~



## Functions

### Mutliple return valuse

* 많은 리턴을 가질수 있다. 

~~~
func (file *File) Write(b []byte) (n int, err error)
~~~



### Named result parameters

* 함수의 파라미터 결과 리턴은 이름을 줄수있음.
* 이름을 짓는법이 정해져있진않지만 짧고 분명해야됨.

~~~go
func nextInt(b []byte, pos int) (value, nextPos int) {
~~~

~~~go
func ReadFull(r Reader, buf []byte) (n int, err error) {
    for len(buf) > 0 && err == nil {
        var nr int
        nr, err = r.Read(buf)
        n += nr
        buf = buf[nr:]
    }
    return
}

~~~



### Defer

* Defer는 함수의 콜에 상태를 스케쥴 함. 
* 반환되기 직전에 실행해야되는것.

~~~go
// Contents returns the file's contents as a string.
func Contents(filename string) (string, error) {
    f, err := os.Open(filename)
    if err != nil {
        return "", err
    }
    defer f.Close()  // f.Close will run when we're finished.

    var result []byte
    buf := make([]byte, 100)
    for {
        n, err := f.Read(buf[0:])
        result = append(result, buf[0:n]...) // append is discussed later.
        if err != nil {
            if err == io.EOF {
                break
            }
            return "", err  // f will be closed if we return here.
        }
    }
    return string(result), nil // f will be closed if we return here.
}

~~~

* 리소스 반환같은곳이 중요한 쓰임새.
* LIFO와 같은 형태에서 defer가 유용하게 쓰일수 있음

~~~go
func trace(s string)   { fmt.Println("entering:", s) }
func untrace(s string) { fmt.Println("leaving:", s) }

// Use them like this:
func a() {
    trace("a")
    defer untrace("a")
    // do something....
}
~~~



## Data

### Allocation With new

* 고에는 두개의 할당 빌트인  함수들이 있다. new & make임.

* 두 개는 서로 다른 유형임.

* new

  * new(T) 는 zero가 된 저잔소를 할당함.
  * 포인터로 반환되기때문에 0값의 저장소를 가르키는 포인터를 반환함.
  * 메모리를 이니셜라이즈 하지 않는다. 
  * 0으로 초기화되기 때문에 기본값이 0인 값을 사용하는 형태일때 쓰이면 됩니다.

    * byte.Buffer는 기본 0값을 사용할 준비가 된 버퍼.
    * syncMutext에도 init이나 consructure가 없음. 대신 sync Mutex의 0값은 잠기지 않은 상태르 나타냄.

### Constructors and composite literals

* zero value는 완벽하지는 않다. initializing이 필요할 수 있을 때가 있기 때문이다. 

```
func NewFile(fd int, name string) *File {
    if fd < 0 {
        return nil
    }
    f := new(File)
    f.fd = fd
    f.name = name
    f.dirinfo = nil
    f.nepipe = 0
    return f
}
```

* newFile의 initialize를 할때 위와같이 설정 할 수 있을것이다. 당장에 쓰이지 않을(말그대로 초기화할)  부분을 nil과 0으로 채울수 있을것이다.
* 이러한 경우에는 composit literal로  간단히 나타낼 수 있다.

~~~
func NewFile(fd int, name string) *File {
    if fd < 0 {
        return nil
    }
    f := File{fd, name, nil, 0}
    return &f
}
~~~

* 여기서 nil과 0은 zero value로 자동으로 들어가기 때문에 이 마져도 아래와 같이 줄일 수 있다.

~~~
return &File{fd: fd,name: name}
~~~

* 이는 다른 데이터 타입에서도 적용될 수 있다.

~~~
ele := [...]string {1:"hi",3:"nice}
fmt.Printf(“%#v, length=%d\n”, elements, len(elements))
//
[4]string{“”, “hi”, “”, “nice”, “”}, length=4
~~~

* 빈 곳은  "" 로 채워진것을 볼 수 있다.

### Allocation With make

- new 와 애당초 make는 쓰임 목표가 다르다. 
- initialized value가 zero value가 아니라는 점이다. 
- 사용되기전에 일정량의 length, capcity가 보장되어야하는 데이터에 쓰인다. 

~~~
make([]int, 10, 100)
~~~

* 위의 예제는 100까지의 int를 담을 수 있는  array를 준비해두고 10만큼의 길이의 slice structrure를 할당해둔다. (여기는 slice가 make 될때 capcity가 어떻게 할당되는지 참고하면 된다.)

~~~
var p *[]int = new([]int)       // allocates slice structure; *p == nil; rarely useful
var v  []int = make([]int, 100) // the slice v now refers to a new array of 100 ints

// Unnecessarily complex:
var p *[]int = new([]int)
*p = make([]int, 100, 100)

// Idiomatic:
v := make([]int, 100)	
~~~

* 위의 코드를 보면 확실히 new와 make의 차이를 느낄 수 있다.



## Arrays

* Go와  C의 array의 차이는 아래와 같다.
  * Arrays는 values값이다.  copy시 모든 element들이 copy된다.
  * function 에 array를 받았다면 그것은 copy값이다. point값이 아니다.
  * array의 size는 type에 일부분이다. 
* value property는 유용하지만 cost가 비싸다. c style로 필요하다면 당연 point값으로 이용하면 된다.












## REF

[EffetiveGo](https://golang.org/doc/effective_go.html#formatting)

[examples](https://medium.com/golangspec/composite-literals-in-go-10dc62eec06a)

