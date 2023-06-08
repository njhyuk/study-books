# 5.8 익명함수를 적절하게 사용하라

## 5.8.1 익명 함수는 간단한 로직에 좋다

익명함수 예시 : 단 하나의 문장, 간단하기에 이해하기 쉽고 단순 명료하여 좋음

```java
List<Feedback> getUsefulFeedback(List<Feedback> allFeedback) {
    return allFeedback.filter (feedback -> !feedback.getComment().isEmpty());
}
```

명명함수 예시 : 가독성이 떨어져 보일 수 있으나, 재사용성이 조금 더 올라감

```java
List<Feedback> getUsefulFeedback(List<Feedback> allFeedback) {
    return allFeedback.filter(hasNonEmptyComment);
}

private Boolean hasNonEmptyComment (Feedback feedback) {
    return !feedback.getComment().isEmpty();
}
```

## 5.8.2 익명 함수는 가독성이 떨어질 수 있다

패리티 비트를 확인하는 논리가 익명함수로 표현, 패리티 비티로 확인한다는 점이 드러나지 않음 (가독성 하락)

```java
List<UInt16> getValidIds (List<UInt16> ids) {
    return ids
        .filter (id -> id != 0)
        .filter (id -> countSetBits (id & 0x7FFF) % 2 ==
        ((id & 0x8000) »> 15));
}
```

## 5.8.3 해결책: 대신 명명 함수를 사용하라

호출자는 유효한 ID 를 얻기 위한 높은 수준에서의 세부사항을 알고 싶을 것이다. - 명명함수를 추천 - 즉시 이해

```java
List<UInt16> getValidIds (List<UInt16> ids) {
    return ids.filter (id -> id != 0).filter (isParityBitCorrect);
}

private Boolean isParityBitCorrect (UInt16 id) { }
```

명명은 더 많은 코드를 작성해야 하는 단점, 익명은 줄이는데 뛰어나지만 이름이 없어짐

간단하고 자명한것 : 익명, 복잡한 논리 : 명명

## 5.8.4 익명 함수가 길면 문제가 될 수 있다

* (예제 5.29) 거대한 인라인 익명함수, 중첩 익명 함수, 빽빽하게 채워진 로직으로 이해하기 어려움
* 더 작은 명명 함수로 나누는 것이 좋을 것이다

## 5.8.5 해결책: 긴 익명 함수를 여러 개의 명명 함수로 나누라

* (예제 5.30) 익명 함수를 각각 명명으로 정의하여 나눔
  * buildTitle, buildCommentText, buildCategories










