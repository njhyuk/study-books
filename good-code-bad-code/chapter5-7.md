# 5.7 설명되지 않은 값을 사용하지 말라

하드코딩이 필요한 경우가 많이 있는데 예는 다음과 같다.

* 한 수량을 다른 수량으로 변환할 때 사용하는 계수
* 조정 가능한 파라미터 값 (ex 작업이 실패할 경우 재시도의 최대 횟수)
* 어떤 값이 채워질 수 있는 템플릿을 나타내는 문자열

값은 당연히 존재 하지만, 해당 값이 무엇을 의미하는지는 개발자들이 명확히 이해하도록 해야함

## 5.7.1 설명되지 않은 값은 혼란스러울 수 있다

* (예제 5.21) 운동에너지 방정식에 익숙하지 않은 사람은 이 상수가 무엇을 나타내는지 모를 것이다.
* 즉 유지보수 하기 어렵다.

> 하드코딩된 907.1847 값 - 미국톤/킬로그램 변환 계수에 대한 설명이 없다.

## 5.7.2 해결책: 잘 명명된 상수를 사용하라

```java
const Double 킬로그램_톤 = 907.1847

Double getKineticEnergyJ() {
    return 킬로그램_톤 * ...
}
```

## 5.7.3 해결책: 잘 명명된 함수를 사용하라

값을 제거하는 명명된 함수

```java
private static Double kilogramsPerUsTon () {
    return 907.1847;
}

private static Double metersPerSecondPerMph() {
    return 0.44704;
}
```

변환을 수행하기 위한 헬퍼 함수

```java
private static Double usTonsTokilograms (Double usTons) {
    return usTons * 907.1847;
}
private static Double mphToMetersPerSecond (Double mph) {
    return mph * 0.44704;
}
```