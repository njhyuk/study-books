# 8.4 클래스는 자신의 기능에만 집중해야 한다 
## 8.4.1 다른 클래스와 지나치게 연관되어 있으면 문제가 될 수 있다
* 예제 8.18 Book 클래스에서 Chapter 객체 리스트의 합계를 구하는 코드
* Chapter 에 대한 많은 세부사항이 Book 에 하드코딩됨

## 8.4.2 해결책: 자신의 기능에만 충실한 클래스를 만들라
* chapter 의 로직을 chapter 클래스로 옮김
* Book 에서는 옮겨진 chapter의 함수를 호출하여 Book 클래스를 위한 코드만 남겨짐
