# Kotlin Contract
코틀린 Contract 문법

# `contract` and `implies`
컴파일러에게 변수의 조건을 당부하는 문법이다.
```kotlin
import kotlin.contracts.contract

fun main() {
    val a: Int? = 5
    
    // Error
    if (a.isNotNull()) printSquare(a) // inferred type is Int? but Int was expected
    
    // Works
    if (a.isNotNullContracted()) printSquare(a)
}

fun printSquare(s: Int) = println(s*s)

fun Any?.isNotNull() = this != null

fun Any?.isNotNullContracted(): Boolean {
    contract {
        returns(true) implies (this@isNotNullContracted != null) // contracts that this is not null
    }
    return this != null
}
```

`Any?.isNotNull` 함수는 true 를 반환해도 null 이 아님을 컴파일러가 알지 못하기 때문에 `printSquare(a)` 는 Type mismatch 가 된다. <br>
그러나 `Any?.isNotNullContracted` 함수는 **true 가 반환되면 null 이 아님을 당부하여** `printSquare(a)` 가 정상적으로 실행되도록 만든다.

# `callsInPlace` and `InvocationKind`
```kotlin
import kotlin.contracts.*

fun main() {
    val a: String
    invoke { a = "Hello, World!" }
    // Captured values initialization is forbidden due to possible reassignment
    println(a) // Error
    
    val b: String
    invokeOnce { b = "Hello, World!" }
    println(b)
}

fun invoke(lambda: () -> Unit) = lambda()
fun invokeOnce(lambda: () -> Unit) {
    contract {
        callsInPlace(lambda, InvocationKind.EXACTLY_ONCE) // contracts that lambda will be invoked exactly once
    }
    lambda()
}
```

일반 람다 안에서 캡쳐된 변수를 initialize 하는 것은 재할당에 의해 불가능하다. <br>
`callsInPlace` 로 딱 한번만 실행됨을 컴파일러에게 당부하면 가능하다.

## InvocationKind 의 종류
> `InvocationKind.EXACTLY_ONCE` : 정확히 한번만 실행 <br>
> `Invocationkind.AT_LEAST_ONCE` : 한번 이상 실행 <br>
> `InvocationKind.AT_MOST_ONCE` : 실행되지 않거나 한번 실행 <br>
> `InvocationKind.UNKNOWN` : 알 수 없음
