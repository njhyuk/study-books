# 9.5 제네릭의 사용을 고려하라
## 9.5.1 특정 유형에 의존하면 일반화를 제한한다
* 단어 맞히기 게임을 위해, 리스트의 무작위 item 을 삭제하고 반환하는 요건
* 예제 19 에서 String 으로 구현했지만, 단어 맞히기 게임 이아닌 사진 맞추기 게임으로 변경한다면 중복 코드를 생성해야함

## 9.5.2 해결책: 제네릭을 사용하라
예제9.21 에서 제네릭으로 변경하여 사진 맞추기 클래스 유형도 코드를 재사용하여 대응이 가능해짐