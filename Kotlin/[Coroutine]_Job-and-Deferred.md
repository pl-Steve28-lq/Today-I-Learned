# Job and Deferred
코루틴 Job 타입과 Deferred 타입

## Job
값을 Return 하지 않는 코루틴. <br>
실행 할 때는 코루틴스코프의 메서드인 launch 를 이용하고, <br>
종료를 기다리기 위해서 join() 메서드를 사용한다.

## Deferred
값을 Return 하는 코루틴.<br>
실행 할 때는 코루틴스코프의 메서드인 async 를 이용하고, <br>
종료를 기다리고 값을 받기 위해 await() 메서드를 사용한다.

## runBlocking
안의 모든 명령이 끝날 때 까지 블로킹 한다. 

## 코루틴의 취소
cancel() 메서드로 코루틴을 취소 할 수 있다.
