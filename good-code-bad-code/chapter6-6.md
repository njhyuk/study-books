# 6-6 미래를 대비한 열거형 처리

## 6.6.1 미래에 추가될 수 있는 열것값을 암묵적으로 처리하는 것은 문제가 될 수 있다

```java
enum PredictedOutcome {
COMPANY WILL_GO_BUST,
COMPANY_WILL_MAKE_A_PROFIT,
}

Boolean isOutcomeSafe(PredictedOutcome prediction) {
if (prediction == PredictedOutcome. COMPANY_ WILL_GO_BUST) {
  return false;
}
return true; // 새로운 열거형 값은 무조건 true 처리되는 문제!
}

```


## 6.6.2 해결책: 모든 경우를 처리하는 스위치 문을 사용하라

```java
Boolean isOutcomeSafe(PredictedOutcome prediction) {
	switch (prediction) {
		case COMPANY_WILL_GO_BUST:
		return false;
		case COMPANY_WILL_MAKE_A_PROFIT:
		return true;
}

throw new UncheckedException("Unhandled prediction: " + prediction); // 처리되지 못한 열거형 값이 있다면 오류
}
```

## 6.6.3 기본 케이스를 주의하라
* switch case 에서 default 문을 쓰고 싶은 유혹..
* if 문 처리하던때와 같은 문제가 발생함, 오류를 발생시켜라

## 6.6.4 주의 사항 : 다른 프로젝트의 열거형에 의존
* 다른 조직에서 내가 작성한 열거형 의존
* 조직의 출시 주기와 프로젝트와의 관계에 따라 달라진다
* 계속 추가될 가능성이 있고, 이로 인해 코드가 작동하지 않을 수 있음, 주의 필요












