# What is Hilt
Hilt 는 무엇인가?

## Dagger
JVM 에서의 Dependency Injection (의존성 주입)을 위한 모듈이다.<br>
컴파일 타임에 의존성 주입을 시작한다.

## Hilt
Android 에서 쉽게 쓸 수 있도록 제작된 Dagger 기반 의존성 주입 모듈이다.<br>

## Dagger 와 Hilt 의 차이점
`Dagger`
```kotlin
/* Car.kt */
class Car {
}

/* CarComponent.kt */
@Component
interface CarComponent {
    fun getCar(): Car
    fun inject(activity: MainActivity) // 액티비티, 필드를 주입 받음
}

// 컴파일 타임에 DaggerCarComponent 클래스를 생성

/* MainActivity.kt */
@Inject lateinit var car: Car // 필드 주입

val comp = DaggerCarComponent.create()
comp.inject(this) // 메인 액티비티를 주입함
```

<br><br><br>


`Hilt`
```kotlin
/* Car.kt */
class Car {
}

/* CarModule.kt */
@Module
@InstallIn(ApplicationComponent::class)
class CarModule {
    @Provides
    fun provideCar() = Car()
}

/* MainActivity.kt */
@AndroidEntryPoint
class MainActivity {
    @Inject lateinit var goodCar: Car
}

/* MyApplication.kt */
@HiltAndroidApp
class MyApplication : Application()
```
