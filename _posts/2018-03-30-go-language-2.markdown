---
layout: post
Title: "[GO] golang"
Author: bosco lyu
Meta: "golang"
published: false
---


## 함수 function
* 일급 함수로 사용 가능함.

## closure
* closure : 함수 바깥에 있는 변수를 참조하는 함수값
```
package main
 
// func에서 func 외부에 있는 i값에 접근해서 값을 업데이트할 수 있다.
func nextValue() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}
 
func main() {
    next := nextValue()
 
    println(next())  // 1
    println(next())  // 2
    println(next())  // 3
 
    anotherNext := nextValue()
    println(anotherNext()) // 1 다시 시작
    println(anotherNext()) // 2
}
```
## goroutine
* 동시 실행
* 기본적으로 1개의 cpu만 사용함.
```
Thread m = new Thread();
``` 
* goroutine as anonymous function
```
```

* 여러개의 cpu를 사용하고 싶다면 

```
package main
 
import (
    "runtime"  
)
 
func main() {
    // 4개의 CPU 사용
    runtime.GOMAXPROCS(4)
 
    //...
}

```

## sync
* 

## select

## defer

## chan

## fallthrough

## 