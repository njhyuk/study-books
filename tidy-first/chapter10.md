# 챕터10 : 명시적인 매개 변수

Map 으로 매개변수가 전달되면 어떤 데이터가 필요한지 알기 어려움 

```java
void drawCircle(Map<String, Object> circleOptions) {
    circleOptions.get("center").getX() ...
}
```

drawCircle 을 나누면 명시적 매개변를 정리할 수 있다.

```java
void drawCircle(Map<String, Object> circleOptions) {
    paintCircle(
    circleOptions.get("center"),
    circleOptions.get("radius"),
    circleOptions.get("fillColor")
    );
}

void paintCircle(Point center, int radius, Color fillColor) {
    // draw circle
}
```

> 그냥 맵을 쓰는게 잘못된거 아닐까?
