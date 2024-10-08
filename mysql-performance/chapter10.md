# 10장 클라우드 MySQL
* 클라우드에서 성능은 곧 돈이다.
* 결국 클라우드는 특별한 것이 아니다.
* 커튼 뒤에는 MySQL과 같은 프로그램을 실행하는 데이터 센터의 물리적인 서버가 있다.
## 10-1 호환성
* 클라우드의 MySQL은 MySQL이 아닐 수 있고 고도로 수정된 MySQL 버전일 수 있다.
* 코드 호환성
  * 기존 오픈소스 코드인지 여부임
  * 변화가 클수록 위험도가 커진다
  * 코드가 호환되지 않은 클라우드에서 MySQL을 사용할 때는 변경범위를 이해햐아 한다
* 기능 호환성
  * MySQL이 클라우드 공급자나 MySQL 배포판 외부에서 사용할 수 없는 기능을 포함하는지 여부
  * 고유한 기능이 있으면 좋지만 다른 클라우드 공급자로 마이그레이션 하기 어려워짐
## 10-2 관리
* MySQL 프로비저닝은 클라우드가 제공해야 하는 것으로, 컴퓨터에서 MySQL을 실행하는 가장 낮은 수준의 작업
* 클라우드 공급자는 root 사용자 외에 MySQL 사용자를 관리하지 않음
* 일부 클라우드는 기본 서버 메트릭을 공개하지만, 전체 스펙트라에 근접한 클라우드는 없다
* ALTER의 책임은 여러분의 책임
* 클라우드는 Failover 조치를 처리함, 그러나 전체 지역에 장애가 발생하고 다른 지리적 위치에서 MySQL을 실행하여 가용성을 복원해야 할 때 재해복구를 처리하지 않음
* 클라우드는 백업, 장기 백업 보존 및 복원 방법을 제공함
* 보안은 여러분의 책임
## 10-3 네트워크와 스토리지 지연 시간
* 클라우드는 전 세계적이며 광역 네트워크는 지연 시간이 길고 안정성이 낮음
* 샌프란시스코에서 MySQL을 실행하고 애플리케이션이 뉴욕에 있다면 최소 쿼리 응답시간은 60ms, 로컬 네트워크보다 60배 느리다
* 클라우드는 네트워크 연결 스톨지를 사용한다, 로컬 스토리지보다 느리고 덜 안정적
* 그러나 이미 크라우드에 있거나, 클라우드에서 새 애플리케이션을 시작하는 경우, 클라우드의 스토리지 대기 시간에대해 걱정할 필요 없다
  * 2~장에서 다른 고도화된 쿼리, 데이터와 접근패턴이 더욱 중요
## 10-4 성능은 곧 돈이다
* 클라우드에서는 매 바이트와 밀리초 단위의 성능이 시간당 청구되므로 중요하다
* 기본 컴퓨팅의 각 레벨에 대해 가격이 2배가 된다
  * ex) 최소 레벨이 vCPU 2, RAM 8GB -> 다음레벨은 vCPU 4 RAM 16GB
* 클라우드의 모든 것은 비용이 든다
  * 스토리지 유형
  * 데이터 스토리지 크기
  * 백업 크기와 보존 기간
  * 로그 크기와 보존 기간
  * 고가용성
  * 리전간 데이터 전송
  * 암호화 키
  * 비밀
* 클라우드 공급자가 할인을 제공한다
  * 1년이나 3년 약정 비용
