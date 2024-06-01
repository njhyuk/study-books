# 5.9 프로그래밍 언어의 새로운 기능을 적절하게 사용하라

## 5.9.1 새 기능은 코드를 개선 할 수 있다

```java
List<String> getNonEmptyStrings (List<String> strings) {
    List<String> nonEmptyStrings = new ArrayList<>();
    for (String str : strings) {
        if (!str.isEmpty)) {
            nonEmptyStrings.add(str);
        }
    }
    return nonEmptyStrings;
}
```

```java
List<String> getNonEmptyStrings(List<String> strings)
{
    return strings.stream()
        .filter(str -> !str.isEmpty())
        .collect(tolist ());
}
```

일반적으로 코드의 품질을 개선한다면 언어가 제공하는 기능을 사용하는 것이 좋다.

## 5.9.2 불분명한 기능은 혼동을 일으킬 수 있다

* 궁극적으로 누가 코드를 유지보수할 지가 중요함
* 다른개발자가 익숙하지 않다면, 스트림을 사용하지 않는 것이 좋을 수도 있다.

## 5.9.3 작업에 가낭 적합한 도구를 사용하라

맵에서 어떤 키에 대한 값을 찾는 가장 합리적인 코드는?

```java
String value = map.get(key)
```

스크림을 사용하면? 오히려 복잡함

```java
Optional<String> value = map.entrySet().stream()
    filter(entry -> entry.getKey().equals(key))
    .map(Entry::getValue)
    •findFirst();
```

과장된 예지만 필자는 본적이 있음. 적절히 사용하라





