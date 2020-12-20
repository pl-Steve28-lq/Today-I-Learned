# How to make annotations
어노테이션 만드는 법

## Annotation Class
어노테이션 클래스를 만든다. <br>
@Target 어노테이션으로 어디에 달 수 있는지 설정한다. <br>
@Repeatable 어노테이션으로 여러개 달 수 있는지 설정한다. <br>
```kotlin
@Target(AnnotationTarget.CLASS) // 클래스에 달 수 있음
@Repeatable // 계속 달 수 있음
annotation class Wa( val sans: String )


@Wa("샌즈")
@Wa("Sans")
class Undertale {}
```

## Annotation Processor
어노테이션을 처리하는 프로세서를 만든다. <br>
javax.annotation.processing.AbstractProcessor 를 상속한다. <br>
구글의 AutoService 를 통해 자동으로 컴파일러에 등록 되게 할 수 있다.

코드 참조 : [UselessProcessor.kt](https://github.com/pl-Steve28-lq/UselessThings/blob/master/UselessThings/src/main/java/com/steve28/uselessthings/annotations/UselessProcessor.kt)

## KotlinPoet
코틀린 파일을 동적으로 작성하는 모듈이다. <br>
이를 통해 빌드 시 새로운 클래스, 함수등을 만들 수 있다. <br>

프로세서에서 KotlinPoet 을 사용해 Extension 등을 만든다.
