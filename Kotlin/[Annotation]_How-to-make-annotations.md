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
```kotlin
@AutoService(Processor::class)
class SansProcessor: AbstractProcessor() {

  /* 어노테이션 클래스의 이름들을 넣는다. */
  override fun getSupportedAnnotationTypes(): MutableSet<String> {
    return mutableSetOf(
      Wa::class.java.name
    )
  }
  
  /* 얘는 잘 모르겠다. */
  override fun getSupportedSourceVersion(): SourceVersion {
      return SourceVersion.latestSupported()
  }
  
  /* 프로세서를 구현한다. (상속 필수) */
  override fun process(annotations: MutableSet<out TypeElement>?, roundEnv: RoundEnvironment): Boolean {
    roundEnv.getElementsAnnotatedWith(Wa::class.java) // Wa 어노테이션이 붙은 것들을 가져온다.
    if (!checkElementType(ElementKind.CLASS, classElements)) return false // 클래스에 붙어있는건지 확인
    
    classElements.forEach {
      // Process something!!!
    }
  }
  
  
  
  /* 타입 체크 하는 함수이다. */
  private fun checkElementType(kind: ElementKind, elements: Set<Element>): Boolean {
    if (elements.isEmpty()) return false

    elements.forEach {
      if (it.kind != kind) {
        printMessage(
          Diagnostic.Kind.ERROR, "Only ${kind.name} Are Supported", it
        )
        return false
      }
    }
    return true
  }

  private fun printMessage(kind: Diagnostic.Kind, message: String, element: Element) {
    processingEnv.messager.printMessage(kind, message, element)
  }
}
```

## KotlinPoet
코틀린 파일을 동적으로 작성하는 모듈이다. <br>
이를 통해 빌드 시 새로운 클래스, 함수등을 만들 수 있다. <br>

프로세서에서 KotlinPoet 을 사용해 Extension 등을 만든다.
