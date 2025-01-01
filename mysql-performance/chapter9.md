# 9장 다른 문제들
## 9-1 스플릿-브레인이 가장 큰 위험이다
* 스플릿-브레인의 조건
  * 둘 이상의 MySQL 인스턴스에서 쓰기가 가능합니다
  * 둘 이상의 MySQL 인스턴스에서 쓰기가 발생합니다
* 둘다 일어나서는 안되고 특히 동시에 발생해서는 안되지만, 버그나 사고를 영원히 피할 수는 없습니다.
  * 이를 스플릿-브레인 이라고 합니다.
* 데이터가 모든 인스턴스에서 더이상 일관되지 않기 때문에 실질적인 분할이다.
* 스플릿-브레인이 발생하면 반드시 감지하고 중지해야 한다.
* 단 몇 초의 스플릿 브레인으로 인해 몇주동안의 데이터 포렌식과 조정 과정이 필요 할 수 있다.
* 복구를 위해 모든 쓰기를 비활성화 해야한다.
  * 데이터 무결성은 데이터 가용성보다 중요하다.
* 일치하지 않는 행을 찾느 방법은 pt-table-sync 를 실행하거나 수동으로 확인해야 한다.
## 9-2 데이터 드리프트는 실제지만 보이지 않는다
* 데이터 드리프트는 일관성 없는 데이터를 의미한다.
* 데이터 드리프트는 pt-table-checksum을 실행하여 쉽게 감지할 수 있다.
  * 데이터를 읽고 비교만 하는 도구이므로 안전하다.
* 아무도 데이터 드리프트의 근본 원인을 발견하거나 입증한 적이 없다.
  * 이론적으로 비결정적 쿼리와 명령문 기반 복제나 복제본에 대한 쓰기로 인해 발생한다.
  * 그럼에도 불구하고 데이터 드리프트는 존재한다.
## 9-3 ORM을 믿지 않도록 주의한다
* ORM은 성능이 목적이 아니므로 생성된 쿼리를 확인해야 한다.
* ORM은 행을 객체로 취급하기 때문에 모든 열을 선택할 수 있다.
* 일부 ORM은 쿼리 전후에 SHOW WARNINGS 를 실행한다.
## 9-4 스키마는 항상 변경된다
* 온라인 스키마 변경을 수행하는 것은 도전적이다.
* MySQL을 위한 3가지 솔루션
  * pt-online-schema-change
  * gh-ost
  * ALTER TABLE
* 스키마 변경도 개발 프로세스의 일부가 되어야 하므로 스키마 변경을 수동으로 수행하지 않는다.
* GitHub ACtions 등을 사용하여 MySQL 스키마 마이그레이션 자동화를 읽어보아라
## 9-5 MySQL 표준 SQL 확장
* MySQL은 표준 SQL에 대한 많은 확장 (커스텀?) 이 있다는 점을 주의하라.
* MySQL은 full outer join 과 같은 일부 표준 SQL 기능을 지원하지 않는다.
* 이러한 독특한 점은 전문가들은 잘 알고 있다.
* MySQL 매뉴얼은 포괄적이고 권위있다.
  * 전문가는 매뉴얼에 많이 의존하고 있으며 여러분도 그래야 한다.
## 9-6 시끄러운 이웃들
* 시끄러운 이웃은 지나치게 많은 시스템 리소스를 사용하여 다른 프로그램의 성능을 떨어뜨리는 프로그램이다.
  * ex) 서버 20개의 개별 MySQL 인스턴스를 실행 중이지만, 그중 하나가 모든 CPU와 I/O를 사용하는 경우
* 클라우드에서는 시끄러운 이웃의 존재를 보거나 증명할 수 없다.
  * 의심될 때는 클라우드 DB를 다시 프로비저닝 하는 것이 일반적
## 9-7 애플리케이션은 우아하게 실패하지 않는다
* 주변의 모든 것이 올바르게 작동할 때 올바르게 작동하는 SW를 만드는건 아무런 소용이 없다.
  * 넷플릭스가 카오스 엔지니어링을 하는 이유이다.
* 카오스 엔지니어링은 MySQL 업계에서 표준 관행이 아니다.
* 12 가지 DB 카오스 시나리오
  * MySQL 오프라인 상태
  * MySQL 응답 속도 느림
  * MySQL 읽기 전용
  * MySQL 이 방금 시작 (콜드 버퍼)
  * 읽기 전용 복제본이 오프라인이거나 매우 느림
  * 같은 지역에서 Failover 수행
  * 다른 지역으로 Failover 수행
  * DB 백업중
  * DNS 주소 해석이 느림
  * 네트워크가 느리거나 꽉참
  * RAID 배열에 있는 하드 하나가 성능 저하
  * SSD 여유 디스크 공간이 5% 미만
## 9-8 고성능 MySQL은 어렵다
* 실제 애플리케이션 쿼리가 책에 있는 간단한 예보다 일반적으로 더 복잡하다.
* 실제 애플리케이션 성능이 워크로드의 한쪽 측면에 거의 의존하지 않는다.
  * 더 많은 성능이 필요할수록 전체 워크로드 (각 쿼리, 모든 데이터와 모든 접근패턴)를 더 많이 최적화 해야한다.