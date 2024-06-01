# 8.3 클래스 상속을 주의하라
* 객체 언어의 특징 : 클래스 계층
	* Vehicle 클래스를 정의한 다음, Vehicle 클래스를 상속받는 Car 및 Truck 클래스
	* 특정 승용차는 Car 클래스 상속 성의

> 상속이 일으킬 수 있는 문제점과 대안 설명

## 8.3.1 클래스 상속은 문제가 될 수 있다.
* FilValueReader, FilValueWriter 인터페이스
* FilValueReader, FilValueWriter 를 상속받은 CsvFileHandler 구체
* CSV 를 정수로 읽으려고 IntFileReader 를 CsvFileHandler 의 서브클래스로 생성함
	* IntFileReader 가 CsvFileHandler 의 모든 기능 사용 가능
	* Write 기능도 사용 가능해져버림
* 구분자가 쉼표에서 세미콜론으로 변경된다면?
	* 다른 개발자가 SemicolonFileHandler 를 구현 해 둔 상태
	* SemicolonFileReader 를로 SemicolonIntFileReader 서브클래스를 만들어서 구현
		* IntFileReader 의 대부분 로직 복붙, 중복이 발생됨

## 8.3.2 해결책: 구성을 사용하라
* IntFileReader 에서 FileValueReader 를 상속받는게 아니라!
	* FileValueReader 를 생성자로 전달받기
	* IntFileReaderFactory 클래스 생성
		* FileValueReader 를 세미콜론으로 구현하여 주입
		* FileValueReader 를 쉼표로 구현하여 주입

> 간결하고 적응성이 높아졌다.

## 8.3.3 진정한 is-a 관계는 어떤가?
* 포스머스탱은 승용차 (is-a) 관계로 볼 수 있다.
* IntFileReader 는 CsvFileHandler (is-a) 로 보기 어렵다.
	* 상속보다 구성이 낫다.
* is-a 관계라고 해도 상속은 여전히 문제가 있다.
* 문제
	* 취약한 베이스 클래스 문제
		* 슈퍼 클래스 수정되면 서브 클래스 작동 안됨
	* 다이아몬드 문제
		* 다중상속을 지원하는 언어, 문제 발생, 어떤 슈퍼클래스의 메서드인지?
	* 문제가 있는 계층 구조
		* Car, Aircarft 구체 (슈퍼) 가 있는 상태
			* 단일 상속 구조에서 FlyingCar 클래스는 누구를 상속 받아야?
		* 인터페이스와 구성으로 해결
			* Car, Aircarft 를 인터페이스로 변경
			* Car 가 DrivingAction 구성 사용
			* Aircraft 가 FlyAction 구성 사용
			* FllyingCar 구체는 Car, Aircraft 인터페이스 두개 다 구현



