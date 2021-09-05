# Kotlin Generics
코틀린의 제네릭

# Basic Usage
```kotlin
// in Function
fun <T> log(msg: T) = println("Log : $msg")

// in Interface, Class
interface Wrapper<T> {}
class Something<T> (val item: T) {}

// Super type restriction
fun <T: Number> plusOne(x: T) = x+1
```

# `in`, `out` Keyword
## in (Contravariance, 반변)
```kotlin
interface Super<in T>

fun main() {
    val a: Super<Double> = object: Super<Number> {}
}
```
T 보다 상위 타입인 무언가를 입력으로 받는다. <br>
상위타입은 T로 형변환 될 수 없으므로 **읽기 불가** <br>
T는 상위타입으로 형변환 될 수 있으므로 **쓰기 가능** <br>

## out (Covariance, 공변)
```kotlin
interface Sub<out T>

fun main() {
    val b: Sub<Number> = object: Sub<Double> {}
}
```
T 보다 하위 타입인 무언가를 입력으로 받는다. <br>
하위타입은 T로 형변환 될 수 있으므로 **읽기 가능** <br>
T는 하위타입으로 형변환 될 수 없으므로 **쓰기 불가** <br>

## Star Projection
```kotlin
interface Function<in T, out U>

Function<*, String> -> Function<in Nothing, String>
Function<Int, *> -> Function<Int, out Any?>
Function<*, *> = Function<in Nothing, out Any?>
```

`*` 은 전체 타입이 필요할 때 쓴다. <br>
in 타입에는 in Nothing 가 된다. (Nothing 은 모든 타입의 Subtype) <br>
out 타입에는 out Any? 가 된다. (Any? 는 모든 타입의 Supertype) <br>

타입 계층 구조 : Nothing -> Nothing? -> 사용자 정의 타입, 기본 타입 -> Any?

# Reified Type
## Type Erasure
```kotlin
fun main() {
    val a = listOf("a", "b", "c")
    val b = a as List<Int> // No Error
    println(b.sum()) // java.lang.ClassCastException
}
```
List<Int> 와 List<String> 은 모두 런타임에 Int, String 이라는 타입 정보가 지워진다. <br>
둘다 List 타입이기 때문에 a as List<Int> 는 아무 문제없이 실행된다. <br>
그러나 b.sum() 은 `ClassCastException` 을 일으킨다.

## `reified` Keyword
```kotlin
fun <T> getClassName() = T::class.java.name // Error
```
이 때 T 에 대한 정보는 지워지므로 `T::class` 로 접근할 수 없다. <br>
타입 정보를 삭제하고 싶지 않을 때 `reified` 를 사용한다. <br>
  
```kotlin
inline fun <reified T> getClassName() = T::class.java.name // No Error
```
그러나 코틀린의 한계로 inline 함수에서만 reified 를 사용할 수 있다.
