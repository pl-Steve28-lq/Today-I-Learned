# Component and Inject
Component (컴퍼넌트) 와 Inject (주입) 어노테이션


## Component
Dagger 가 주입할 때 쓰는 클래스이다. Dagger 는 컴파일 타임에 **Dagger클래스이름** 이라는 새로운 클래스를 만들어 낸다.

## Inject
Dagger 가 Component 를 통해서 주입 해 줄 것들이다. 함수, 변수 등에 사용 할 수 있다.

## Examples
### Constructor Injection
```java
// Car.kt
class Car {
    @Inject
    constructor(engine: Engine, wheels: Wheels) {}
}

// CarComponent.kt
@Component
interface CarComponent {
    fun getCar(): Car
}

// 컴파일 타임에 DaggerCarComponent 클래스를 생성

// MainActivity.kt
val comp = DaggerCarComponent.create()
val car = comp.getCar() // Car 을 가져옴

```

### Field Injection
```java
// Car.kt
class Car {
    constructor(engine: Engine, wheels: Wheels) {}
}

// CarComponent.kt
@Component
interface CarComponent {
    fun getCar(): Car
    fun inject(activity: MainActivity) // 액티비티, 필드를 주입 받음
}

// 컴파일 타임에 DaggerCarComponent 클래스를 생성

// MainActivity.kt
@Inject lateinit var car: Car // 필드 주입

val comp = DaggerCarComponent.create()
comp.inject(this) // 메인 액티비티를 주입함
```
