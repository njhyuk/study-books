# 챕터 9 : 설명하는 상수

리터럴 상수로 사용된 곳은 상징적인 상수로 바꿔라

```java
public static final int PAGE_NOT_FOUND = 404;

public void main(int status) {
    if (status == PAGE_NOT_FOUND) {
        // do something
    }
}
```

도움이 되지 않는 리터럴 상수는 다음과 같다.

```java
public static final int ONE = 1;

public void main(int status) {
    ONE + 10 // 1이 필요할때마다 사용
    ONE + 2
}
```

* 상수 응집하기
  * 한번에 사용되는 상수들은 한곳에 모아두기
* 후속작업
  * 다른 이유로 묶인 변수들을 분리하기
* 결합도와 응집도는 뒤로하고 일단 작업하기
