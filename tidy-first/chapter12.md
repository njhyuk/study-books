# 도우미 추출

* 목적이 분명하고 나머지 코드와는 상호작용이 적은 코드 블록을 만날때가 있다. 
* 도우미의 이름은 목적에 따라 짓자.
* 메서드 추출 리팩터링을 사용하자.


## 큰 루틴 안에서 몇줄을 추출해 도우미 함수로 만들기

```kotlin
fun routine() {
    val a = 10
    val b = 20
    val c = (a + b) / 2
}
```

```kotlin
fun routine() {
    val a = 10
    val b = 20
    average(a, b)
}

fun average(a: Int, b: Int): Int {
    return (a + b) / 2
}
```

## 도우미 함수로 시간적 결합을 표현하는 경우

```
foo.a()
foo.b()
```

이럴땐 다음처럼 바꾸기

```
ab()
    b()
    a()
```
