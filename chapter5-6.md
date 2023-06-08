# 5.6 함수 호출도 가독성이 있어야 한다

* 함수 호출은 인수 개수가 늘어나면 이해하기 힘들어짐
* 충분히 모듈화 되지 않았음을 의미 할 수 있다

## 5.6.1 매개변수는 이해하기 어려울 수 있다

```
sendMessage("hello", 1, true)
```

hello 는 메세지 같다. 1 이랑 true 는 뭘까? 세부 구현 봐야함.

## 5.6.2 해결책: 명명된 매개변수 사용

```kotlin
sendMessage(
    message: "hello",
    priority: 1,
    allowRetry: true
)
```

타입스크립트 에서는 위 문법이 불가능, DTO 를 객체 구조 분해해서 많이 쓴다.

```
function sendMessage (
    {message, priority, allowRetry}: SendMessageDto
)
```

## 5.6.3 해결책: 서술적 유형 사용

* 예제 5.18 priority 는 클래스, retryPolicy 는 enum 으로 서술적 정의
* 의미를 알기 어려운 int와 boolean 값에서 이해하기 쉬워짐

## 5.6.4 때로는 훌륭한 해결책이 없다

이 클래스의 생성자는 상자의 모서리 위치를 나타내는 4개의 정숫값을 매개변수로 받는다.

```java
class BoundingBox {
    BoundingBox(Int top, Int right, Int bottom, Int left) {
        // ...
    }
}
```

* 명명된 매개변수를 지원하지 않는다면, 이해하기 쉽지 않다.
* 이 경우는 특별히 만족스러운 해결책이 없으며, 인라인 주석문을 사용하는 방법이 있다.
* 한편으로는 주석을 유지보수해야 해서 쓰지 말라는 주장도 있다.

```java
new BoundingBox(
    /* top= */ 10,
    /* right= */ 50,
    /* bottom= */ 20,
    /* left= */ 5,
)
```

> 💬 이정도는 IDE 에서 보이는 힌트로도 명확하지 않나? 오히려 지저분한 것 같다..

* 세터 함수를 추가하거나 빌더 패턴과 같은 것을 사용하는 것이 대안이 될 수 있음
  * 단점 : 값이 누락된 채 인스턴스가 만들어질 가능성

## 5.6.5 IDE는 어떤가?

* 이 방법이 대단이 유용하지만 의존하지 않는 것이 좋다.
* 코드베이스 탐색 도구, 병합 도구, 코드 검토 도구에서는 지원하지 않기 떄문


