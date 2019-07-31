# kotlin-grammer-basic
kotlin-grammer-basic


# 코틀린 문법 정리

### 1. 코틀린 기본 파일 정의

* 기본적으로 코틀린 프로그램은 확장자가 kt인 파일이다.

* 파일(File)과 클래스 파일(Class)는 편의상 구분한다.
  
  ex)MyClass.kt, MyFile.kt
 
 
### 2. 패키지

* 패키지란 관련된 클래스(Class)들을 묶기 위한 물리적 개념이다.

* 이용하려는 클래스가 다른 패키지에 있다면 import 구문을 이용한다.

```kotlin
package com.example.tabloni.one

import com.example.tabloni.one.sub.two
```

* 임포트할 때 이름을 바꾸어 다른 이름으로 사용가능하다.

```kotlin
package com.example.tabloni.one

import com.example.tabloni.one.sub.two as MySimplePackage
```

### 3. 변수와 함수

#### 3.1 변수 선언법

* **val**,**var**로 변수를 선언할 수 있다.
* **var**은 읽기,쓰기가 가능한 일반 변수 이다.
* **val**은 읽기만 가능한 final 변수 이다.
* 선언하는 법은 **val(or var) 변수명 : 타입 = 값** or **val 변수명 = 값** 으로 선언한다.
* 타입 추론을 지원한다.

```kotlin
val data1:Int = 10
val data2 = 20
var data3 = 30

fun main(args: Arrya<String>){
  //data2 = 50 //error: 변경이 불가능함.
  var data3 = 50 //OK!

}
```

#### 3.2 변수 초기화

* 변수 선언은 최상위(클래스 외부),클래스 내부,함수 내부에 선언할 수 있다.
* 최상위 레벨이나 클래스의 멤버 변수는 선언과 동시에 초기화 해주어야 한다.
* 함수 내부의 지역 변수는 선언과 동시에 초기화하지 않더라도 된다. 초기화한후 사용할 수 있다.

```kotlin
val topData1: Int//err
var topData2: Int//err

class Test {
  val objData1: String//err
  var objData2: String//err

    fun some(){
    val localData1: String//ok!
    var localData2: Int//ok!
    
    println(localData1)//err : 변수가 초기화 되지않음
    
    localData1 = "TabloNi" //ok!
    println(localData1)//ok!
    
    }
}
```

#### 3.3 함수 선언

* 선언 방법 **fun 함수명(매개변수명:타입):리턴타입{}**

```kotlin
fun sum(a:Int,b:Int):Int{
  return a+b
}
```

* 매개변수 에는 var,val을 선언할 수 없다. 매개변수는 기본으로 val이 적용되어있다.
* 의미있는 반환값이 없을 때는 Unit으로 명시한다.
* Unit은 생략할 수 있으며 함수의 타입이 선언되지 않았다면 기본적으로 Unit이 적용된다.

```kotlin
fun sum(a:Int,b:Int):Unit{
  //some code
}
```

```kotlin
fun sum(a:Int,b:Int) {
  //some code
}
```
