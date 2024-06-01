# 8-2 인터페이스에 의존하라
## 8.2.1 구체적인 구현에 의존하면 적응성이 제한된다
RoutePlanner 가 NorthAmericalRoadMap 구체에 의존하는 모습

## 8.2.2 해결책: 가능한 경우 인터페이스에 의존하라
RoutePlanner 가 RoadMap 인터페이스를 의존하여 교체 가능해진 모습
