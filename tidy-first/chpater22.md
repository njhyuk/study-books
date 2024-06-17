# 요소들을 유익하게 관계 맺는 일

소프트웨어 설계의 의미 : 요소들을 유익하게 관계 맺는 일

## 요소

물질의 구조

* 세포소기관 -> 기관 -> 유기체
* 원자 -> 분자 -> 결정
* 프로그래밍 세계, 토큰 -> 식 -> 문 -> 함수 -> 객체/모듈 -> 시스템

* 요소에는 경계가 있다. 시각과 끝을 알 수 있다.
* 요소는 하위 요소를 포함한다.
  * 프로그래머들은 컴포지트 패턴과 같은 동질적 계층 구조를 선호한다.
  * 자연의 계층 구조는 동질적이지 않다.
    * 하위 요소는 이들을 포함하는 요소와 다르다.

## 관계 맺기

* 요소들은 서로 관계를 맺는다.
* 하나의 함수가 다른 함수를 호출한다.
  * 호출하고/호출받는 관계
  * 자연에서는 먹는다, 그늘을 만들다, 비옥하게 한다
* 소프트웨어 설계에서 관계는 다음의 것들이 있다
  * 호출
  * 발행
  * 대기
  * 참조

## 유익하게

* 하나의 설계 작업은 작은 하위 요소로 만든 거대한 수프를 만드는 일
* 전역 네임스페이스를 사용한 어셈블리 언어 예시
  * 기본적으로 잘 작동
  * 빠르게 변경할 수는 없다, 잘드러내지 않는 관계가 너무 많다
* 설계할 때, 중간 요소를 만들기
  * 그 중간요소들이 서로에게 도움이 되기
  * 함수 A는 함수 B가 계산의 복잡한 부분을 덜어가기

## 요소들을 유익하게 관계맺는 일

* 설계란?
  * 설계를 구성하는 요소들과 그들의 관계, 그 관계에서 파생되는 이점
* 설계자는?
  * 요소들을 유익하게 관계 맺는 일
  * 하는일
    * 요소를 만들고 삭제
    * 관계를 만들고 삭제
    * 관계의 이점을 높이기

한 객체가 하나의 함수에서 다른 객체를 두 번 호출하는 예시

```kotlin
fun caller() {
    box.width() * box.height()
}
```

* caller()는 box 객체와 두가지 관계를 가짐 (두개의 함수 호출)
* 식을 box 객체 안으로 옮기기 

```kotlin
fun caller() {
    box.area()
}

fun Box.area() = width() * height()
```

이제 두 요소는 하나의 함수 호출로 연결됨

시스템의 구조는?

* 요소 계층 구조
* 요소 사이의 관계
* 이러한 관계가 만들어내는 이점
