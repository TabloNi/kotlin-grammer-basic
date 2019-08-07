# kotlin-grammer-basic
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

# kotlin Class 및 object정리

### 기본 클래스

기본 클래스의 형태는 `Java`와 동일하다.


```kotlin
class ClassName {

}
```

별도의 함수 정의가 없다면 다음과 같이 `{}`을 제외할 수 있다.

```kotlin
class ClassName
```

### 생성자

생성자는 항상 `overloading`을 통해서 여러 개의 형태가 만들어지게 된다.

다만 `코틀린으로 클래스를 생성하고, 코틀린에서만 사용하게 되면 default 변수 정의`가 가능하기 때문에 별도의 `overloading`을 정의하지 않아도 된다.

```kotlin
fun setItems(val name: String, val age: Int = 0) {}
```


예를 들면 위와 같이 `default`를 정의해주면 `overloading`을 하지 않아도 무관하다.

다만 Java에서도 같은 함수를 사용하게 만들어야 하고, `default`를 허용하지 않아서 결국 `overloading`을 만들어야 한다.

먼저, Java에서의 생성자는 다음과 같다.

```kotlin
class ClassName {

  public ClassName(String name) {
    // …
  }
}
```

위와 같이 별도의 함수로 생성자를 선언할 수 있다.

코틀린에서는 다음과 같이 클래스 이름 끝에 `()`을 포함하여 생성자를 선언해줄 수 있다.

```kotlin
class ClassName(name: String) {
  // Class 정의
}
```

클래스 생성자의 원형은 다음과 같다.

```
class ClassName constructor(name: String) {
  // Class 정의
}
```

원래는 `constructor`가 생성자를 나타내게 된다.

하지만 `constructor`을 매번 써주는 것은 코드량만 늘어나고 불필요한 사항이라서 생략이 가능하다. 간단하게 `class ClassName(name: String)`의 형태로 선언할 수 있다.


### 생성자 초기화

Java에서 생성자를 초기화 해보면 다음과 같다.

```kotlin
class ClassName {

  private int[] age;

  public ClassName() {
    age = new int[10];
  }
}
```

코틀린의  `constructor`에서는 이러한 코드는 불가능하기 때문에 별도의 `init` 코드를 이용하여 초기화해줄 수 있다.

```kotlin
class ClassName(name: String) {
  init {
    println("Initialized Value ${name}")
  }
}
```

`init` 코드를 사용하지 않고, 다음과 같이 `upperName`이라는 String 변수에 생성자에서 넘겨받은 `name`을 `toUpperCase`하여 바로 대문자로 초기화할 수 있다.

```kotlin
class ClassName(name: String) {
  val upperName = name.toUpperCase()
}
```

별도의 생성자 정의 없이 위와 같이 바로 초기화가 가능한 형태로 사용할 수 있다.

생성자에 `val`로 정의하였다면 읽기만 가능하고, `var`로 정의하였다면 읽기 쓰기가 가능한 형태이다. Java에서는 `final`로 사용할 수 있다. 다음과 같은 형태로 생성자를 정의할 수 있다.

```kotlin
class Person(val name, var age: Int) {
  // ...
}
```

### 1개 이상의 생성자

클래스 이름의 선언과 동시에 생성자를 선언하는 Kotlin에서도 1개 이상의 생성자를 정의할 수 있다.

* JAVA

```java
class Person {
  public Person(String name) {
    // name 정의
  }

  public Person(String name, int age) {
    this(name);
    // age 정의
  }
}
```

Kotlin에서는 `constructor`을 여러 개로 정의할 수 있다.

```kotlin
class Person(val name: String) {
  constructor(name: String, age: Int) : this(name) {
    // ...
  }
}
```

첫 번째 생성자는 `val name: String`만을 초기화할 수 있고, 2번째는 `name: String, age: Int`를 가지는 생성자이다.

`name`은 중복적으로 사용되는 키워드이므로 기존 생성자로 넘겨주기 위해서 `this()` 키워드를 사용하여 정의 할 수 있다.

### 생성자 private으로 사용하기

Java에서는 싱글톤을 사용하는 경우 `private`을 정의하여 생성자를 이용한다.

Kotlin에서도 `private`의 생성자를 이용할 수 있다.

```kotlin
class PrivateConstructor private constructor() {
  // Class 정의
}
```

### 클래스 사용하기

클래스를 생성하기 위해서 Java에서는 `new` 키워드를 사용한다.

`new`를 사용하여 다음과 같이 `ClassName` 클래스에 접근하여 사용할 수 있다.

* JAVA

```java
class ClassName {
  // Class 정의
}

ClassName className = new ClassName();
```

코틀린에서는 `new`라고 쓰지 않고도 `Class` 를 사용할 수 있다.

클래스의 생성자만 정의하면 바로 사용할 수 있다.

```kotlin
class ClassName {
  // Class 정의
}

val className = ClassName()
```

### Kotlin의 상속

Java에서는 `extends`와 `implements`로 상속을 이용한다.

```kotlin
public abstract class Base {
  public Base(int age) {

  }
}

// 추상 클래스의 상속을 다음과 같이 사용
public class UseBase extends Base {
  public UseBase(int age) {
    super(age);
  }
}
```

kotlin에서는 `abstract`와 `interface`에 대한 별도 구분 없이 `:`을 이용하여 상속받을 수 있다.

```kotlin
open class Base(age: Int)

// open으로 생성한 추상 클래스를 다음과 같이 사용
class UseBase(age: Int) : Base(age)
```

간단하게 위와 같이 `:`으로 구분하여 상속을 구현하게 된다.

예를 들어 `Android` 많이 사용하는 `View` 상속은 다음과 같이 처리할 수 있다.

```kotlin
class MyView : View {
    constructor(ctx: Context) : super(ctx) {
      // 정의
    }

    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs) {
      // 정의
    }
}
```

### 함수 Overriding

함수를 Overriding을 하기 위해서 java에서는 `abstract` 또는 `interface`를 사용한다.

`abstract`은 `extends`을 이용하여 상속을 구현하고, `interface`는`implements`를 이용하여 상속을 사용한다.

```java
abstract class AbstractBase {
  abstract void onCreate();
  final void onResume() {} // 상속에서 재 구현 금지
}

interface Base {
  void onStart();
}

public Use extends AbstractBase implements Base {

  // Abstract 상속에 대한 구현
  @Override
  void onCreate() {}

  // interface에 대한 구현
  @Override
  void onStart() {}
}
```

이를 kotlin에서 `:` 와 `open`를 이용하여 구현하면 다음과 같다.

```kotlin
interface BaseItem {
    fun onStart()
}

open class Base {
    open fun v() {}
    fun nv() {}
}

class AbstractBase() : Base(), BaseItem {
    // Base의 open 키워드를 통해 상속을 구현
    override fun v() {}
    // Interface에서 구현한 상속
    override fun onStart() {}
}
```

### kotlin `open`

kotlin에서 사용하게 되는 `open` 키워드는 다음과 같다.

* java에서는 상속의 재 정의를 방지하기 위해 `final`을 사용한다.

* kotlin에서는 반대로 상속의 재 정의를 허용하기 위해서 `open`을 사용한다.

java에서는 `final`을 통해서 상속의 재 정의를 막지만 kotlin에서는 `open`을 이용하여 함수의 재 정의를 할 수 있도록 허용한다.

`open` 클래스의 `open` 함수가 있다면, 이는 상속을 받아 재 정의가 가능한 형태이다.

그래서 다음과 같이 `open` 클래스를 구현하게 되면 `v()`는 재 정의가 가능하고, `nv()`는 재 정의가 불가능한 형태가 만들어 진다.

```kotlin
open class Base {
    open fun v() {
        print("ABC")
    }
    fun nv() {}
}
```

open은 변수에서도 사용이 가능하다.

```kotlin
open class Foo {
  open val x: Int get { ... }
}

class Bar(override val x: Int) : Foo() {

}
```

위의 코드를 예제로 작성하면 다음과 같고 실행하면 12라는 결과를 얻을 수 있다.

```kotlin
fun main(args: Array<String>) {
    print(C(12).x)
}

open class A {
    open val x: Int = 0
}

class C(override val x: Int) : A() {
}
```

### Overriding Rules

다음과 같은 코드에서 다중 상속을 허용하게 된다.

```kotlin
open class A {
  open fun f() { print("A") }
  fun a() { print("a") }
}

interface B {
  fun f() { print("B") } // interface members are 'open' by default
  fun b() { print("b") }
}

class C() : A(), B {
  // The compiler requires f() to be overridden:
  override fun f() {
    super<A>.f() // call to A.f()
    super<B>.f() // call to B.f()
  }
}

//kotlin Formula code

```

해당 `C()`의 `f()` 함수를 실행한 결과는 다음과 같다.

* print(“A”), print(“B”)

class C()에서 보듯 `f()` 함수를 정의한 부분을 살펴보면,

* super<A>.f()는 A.f()를 하는 것과 동일하다.
* super<B>.f()는 B.f()를 하는 것과 동일하다.

함수 `f()`가 `open class A`의 `f()`도 상속받았고, `interface B`의 `f()`도 함께 상속이 된 상태라서 가능한 현상이라 볼 수 있다.


### Abstract class

Java에서 사용하는 추상 클래스 정의는 다음과 같다.

```kotlin
public abstract class Base {

  public Base(String name) {
    updateName(name);
  }

  protected abstract void updateName(String name);
}

// Base를 상속 받는 클래스
public class UseName extends Base {
  public UseName(String name) {
    super(name);
  }

  @Override
  protected void updateName(String name) {
    // 정의
  }
}
```

kotlin에서도 기본 Abstract은 동일하게 구현하게 된다.

```kotlin
abstract class BaseUse(name: String) {

    init {
        updateName(name)
    }

    protected abstract fun updateName(name: String)
}


// Base를 상속 받는 클래스
class UseName(name: String) : BaseUse(name) {

    override fun updateName(name: String) {
        // 정의
    }
}
```

추가로 kotlin의 `open class`를 추가하여 다음과 같이 확장할 수 있다.

```kotlin
open class Base {
  open fun f() {}
}

abstract class AbstractBase : Base() {
  override abstract fun f()
}
```

`open` 클래스의 `f()` 함수는 `override`가 가능한 형태이다.
이를 `AbstractBase`에서 상속받고, `abstract`으로 확장할 수 있다. 

## Java의 static 메소드 와 코틀린

다음은 java에서의 `static`을 이용한 외부접근이다.

```kotlin
public class ClassName {

  // getInstance() 구현을 위하여 private
  private ClassName() {

  }

  public static ClassName getInstance() {
    return new ClassName();
  }
}

// Use...
ClassName className = ClassName.getInstance();
```

위와 같은 `getInstance`의 형태로 사용할 수 있다.

kotlin에서는 `companion` 키워드를 사용하여 구현할 수 있다.

```kotlin
// 생성자 private 처리
class ClassName private constructor() {

  // 외부에서 static 형태로 접근 가능
  companion object {
    fun getInstance() = ClassName()
  }
}

// Use kotlin
val className = ClassName().getInstance()
// Use java
ClassName className = ClassName.Companion.getInstance();
```

### Sealed Classes

열거 형태로 자기 자신을 return이 가능하고, 다음과 같이 `class`와 `object`에 자기 자신을 `return`하는 클래스 형태이다.

다음 예제는 `eval`이라는 함수에 `Expr`을 이용하게 된다. 이 클래스는 `when`으로 동작한다. 이는 `Expr`의 `Sum` 클래스를 초기화하고 초기화시에는 2개의 `Expr`을 사용하며 이를 `+`하는 함수이다. 실제로는 `expr.number`를 가져와서 처리하는 예제이다.

```kotlin
fun main(args: Array<String>) {
	print(eval(Expr.Sum(Expr.Const(12.44), Expr.Const(12.33))))
}

sealed class Expr {
    class Const(val number: Double) : Expr()
    class Sum(val e1: Expr, val e2: Expr) : Expr()
    object NotANumber : Expr()
}

fun eval(expr: Expr): Double = when(expr) {
    is Expr.Const -> expr.number
    is Expr.Sum -> eval(expr.e1) + eval(expr.e2)
    Expr.NotANumber -> Double.NaN
    // the `else` clause is not required because we've covered all the cases
}
```
