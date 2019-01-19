---
layout: post
Title: "[GO] golang"
Author: bosco lyu
Meta: "golang"
published: false
---

# introduction
## keyword

```
break           default         func            interface       select
case            defer           go              map             struct
chan            else            goto            package         switch
const           fallthrough     if              range           type
continue        for             import          return          var
```
## function
* 내장된 함수는 기능을 편하게 쓸 수 있도록 제공되는 함수임
* 키워드가 아니므로 해당 명칭을 다른 용도로 사용할 수 있다. 물론 그럴 경우 내장함수 new를 사용할 수 없다.
```
make    	len     	cap     
new     	append		copy       
close   	delete		complex         
real		imag		panic           
recover
```

## declaration
* `var, const, type, func` 4가지 종류가 있음
* `함수안에서는` 타입을 선언하지 않고 간략하게 선언할 수 있다.
```
var t int = 0
```
```
t := 0
i, j := 0, 1
```
* 일부 변수가 이미 선언을 했더라고 같이 쓸 수 있다.
```
// 두번째 문장에서 에러 발생하지 않음
in, err := os.Open(infile)
out, err := os.Create(outfile)
```
* 모든 변수가 이미 선언된 경우에는 에러가 발생한다.
```
// 두번째 문장에서 컴파일 에러 발생함.
f, err := os.Open(infile)
f, err := os.Create(outfile)
```
## 엄밀한 관리
### package -> import -> definition으로 작성되어야 한다.
순서가 어긋나면 컴파일 에러를 뱉는다. 

```go
import (
	"fmt"
	"os"
	"bufio"
)

package main

func main() {
	fmt.Println("Hello, 訝??")
}
```
```
$ go build HelloWorld.go
can't load package: package main:
Statement.go:1:1: expected 'package', found 'import'
```



### gofmt 툴을 제공해서 올바른 서식으로 고쳐준다.
gofmt를 이용한 코드 포맷팅도 컴파일 에러가 발생하면 수정하지 않는다. 

```go
package main

import (
        "fmt"
//      "os"
//      "bufio"
)

func main()
{
        fmt.       Println("Hello, 訝??")
}
```

```
$ gofmt Statement.go
Statement.go:10:1: expected declaration, found '{'
```

### 불필요한 변수나 패키지가 포함되어 있으면 에러를 뱉는다. 
실제로 필요할 것 같아서 import를 했는 데 사용하지 않으면 go라는 언어는 그냥 지나치지 않고 컴파일 에러를 출력한다. 어쩌면 짜증날 수도 있겠지만, 향후 코드 유지 보수를 위해서 에러를 출력하는 것이 더 좋다고 생각한 것 같다.

```go
package main

import (
        "fmt"
        "os"
        "bufio"
)

func main() {
        fmt.Println("Hello, 訝??")
}
```

```
# command-line-arguments
./Statement.go:7:2: imported and not used: "os"
./Statement.go:8:2: imported and not used: "bufio"
```

## 문법
### ; 세미콜론
문장이 한 줄에 두 개 이상 나오는 경우외에는 세미콜론을 붙여도 되고, 붙이지 않아도 된다. 세미콜론이 없으면 컴파일러는 개행문자로 판단한다. 주의할 점은 함수의 시작하는 중괄호 {는 함수 선언 아래가 아닌 같은 줄에 위치해야 한다.

### 변수
* 수명
  * 생명 주기
    * 패키지 수준의 변수의 수명은 프로그램의 전체 실행 기간과 같다.
    * 지역 변수의 수명은 동적이다.
### 상수
`const`라는 키워드를 이용해서 선언한다. 아래와 같이 묶어서 선언할 수도 있다. const를 감싸고 있는 것이 중괄호`{}`가 아니라 괄호`()`임을 유념하자. `itoa` 를 사용하면 그 아래에 있는 상수들도 자동 1씩 증가하는 값을 가지게 된다.


```go
package main
import (
	"fmt"
)

const (
        SUCCESS = iota
        FAIL
        FAIL_INVALID_PARAMETER
        FAIL_DB_CONNECTION
)

func main() {
	fmt.Println(SUCCESS)
	fmt.Println(FAIL)
	fmt.Println(FAIL_DB_CONNECTION)
}
```

```
$ go run Const.go
0
1
3
```
### 포인터
* C의 포인터와 동일하게 사용할 수 있다.
* 지역 변수의 포인터에 할당된 값이 사라지진 않는다.
* **포인터를 함수 파라미터로 넘기는 것은 지원하지 않는다.

```
package main

import "fmt"

func main() {
	var fun = func () *int {
		// int x = 0 <- invalid expression
		var x = 0
		fmt.Println(x)
		fmt.Println(&x)
		x = 1
		return &x
	}
	ret := fun()
	fmt.Println(ret)
	fmt.Println(*ret)
	fmt.Println(&ret)
	ret = call(ret)
	fmt.Println("after call function")
	fmt.Println(ret)
	fmt.Println(*ret)
	fmt.Println(&ret)

	// ret = call(&ret) compile error


}


func call(par *int) *int {
	fmt.Println("call function")
	fmt.Println(par)
	fmt.Println(&par)
	var x = par
	fmt.Println(x)
	fmt.Println(&x)
	fmt.Println(*x)
	*x = *x + 1
	return x
}
```

```
./pointer.go:24:13: cannot use &ret (type **int) as type *int in argument to call
```

### 연산자
#### 비교 연산자
비교 연산자의 경우 java와 다르게 `==` string은 기본 자료형이어서(?) 변수의 값을 비교한다. 

```go
package main
import (
        "fmt"
)

const (
        EQUAL = iota
        NOT_EQUAL
)

func main() {
        var a = "string a"
        var b = "string b"
        var c = "string a"

        if a == b {
                fmt.Println(EQUAL)
        } else {
                fmt.Println(NOT_EQUAL)
        }

        if a == c {
                fmt.Println(EQUAL)
        } else {
                fmt.Println(NOT_EQUAL)
        }
}
```
```
$ go run Operator.go
1
0
```
그렇지만 map의 경우에는 비교가 되지 않는다.
```go
package main
import (
	"fmt"
)

const (
        EQUAL = iota
        NOT_EQUAL
)

func main() {
	var a = "string a"
	var b = "string b"
	var c = "string a"

	var map1 = make(map[string]int)
	var map2 = make(map[string]int)

	map1[a] = 1
	map2[a] = 1


	if map1 == map1 {
		fmt.Println(EQUAL)
	} else {
		fmt.Println(NOT_EQUAL)
        }
        
	if map1 == map2 {
		fmt.Println(EQUAL)
	} else {
		fmt.Println(NOT_EQUAL)
	}
}
```
```
# command-line-arguments
./CollectionOperator.go:22:10: invalid operation: map1 == map1 (map can only be compared to nil)
./CollectionOperator.go:28:10: invalid operation: map1 == map2 (map can only be compared to nil)
```
### 조건문
여는 중괄호`{`가 `if`와 같이 있어야 한다. 규칙은 `else if`, `else`에도 동일하게 적용된다. 

### 반복문
다른 언어가 제공하는 do, while는 제공하지 않고 for 문 하나를 이용한다.

```go
for 초기화; 조건; 후처리 {

}

for 조건 {
    
}

for {

}
```
collection을 처리하는 경우에는 `range`를 이용해서 작성도 가능하다.
배열의 경우 첫번째 값은 인덱스이고, 두번째 값이 실제 값이다. 인덱스 값을 `a` 이렇게 선언하고 할당하면 변수를 실제로 사용하지 않았기 때문에 컴파일 에러가 발생한다. 이럴 때는 `_`를 사용하면 된다.
```go
for _, arg := range os.Args[1:] {
    fmt.Println(arg)
}

```

### 문자열
문자열을 계속 더하면 Java처럼 매번 새로운 문자열을 생성한다. 기존의 문자열은 garbage collection 처리 된다.

```go
var full string = ""
for _, arg := range os.Args[1:] {
    full += arg
}
```
성능 저하를 피하고 싶으면 Join 함수를 사용하면 된다.
```
func main() {
        fmt.Println(strings.Join(os.Args[0:], " "))
}
```

### 메모리 주소의 출력
실제 변수의 메모리 주소가 궁금할 때는 그냥 C처럼 `&`를 사용하면 된다. 위처럼 매번 새로운 문자열을 만들어도 변수는 full 하나이기 때문에 주소는 모두 동일하다.

```go
func main() {
        var full string = ""
        fmt.Println(&full)
        full += "test"
        fmt.Println(&full)
        full += " test11"
        fmt.Println(&full)
        fmt.Println("Hello, 訝??")
}
```
```
$ ./Statement1
0xc42000e1d0
0xc42000e1d0
0xc42000e1d0
Hello, 訝??
```


# reference
* golang site : [https://golang.org/](https://golang.org/)
* golang official blog : [https://blog.golang.org/](https://blog.golang.org/)
* golang Documentation : [https://golang.org/doc/](https://golang.org/doc/)
* Go Language specification Doc : [https://golang.org/ref/spec](https://golang.org/ref/spec)
* Go Command Documentation : [https://golang.org/doc/cmd](https://golang.org/doc/cmd)
* Go Memory Model : [https://golang.org/ref/mem](https://golang.org/ref/mem)
* package Documentation : [https://golang.org/pkg/](https://golang.org/pkg/)
* Effective Go : [https://golang.org/doc/effective_go.html](https://golang.org/doc/effective_go.html)
* golang tutorial : 
    * [https://go-tour-kr.appspot.com/](https://go-tour-kr.appspot.com/#1)
    * [https://1ambda.github.io/golang/golang-tutorial/](https://1ambda.github.io/golang/golang-tutorial/)
* golang Korean Community : [https://golangkorea.github.io/](https://golangkorea.github.io/)
* Go와 객체 지향 : [https://golangkorea.github.io/post/go-start/object-oriented/](https://golangkorea.github.io/post/go-start/object-oriented/)
