# 3장 - 시스템 설계 면접 공략법
* 수백명, 수천명의 엔지니어가 참여한 제품 설계를 기대하지 않음
* 두명의 동료가 문제의 해결책을 찾아내는 과정에 대한 시뮬레이션
  * 설계 기술 시연, 설계 결정에 의한 방어 능력 검증
* 기술적 측면만 보지 않는다.
  * 협력에 적합한 사람, 압박에 헤처 나갈 수 있는 사람
  * 모호한 문제를 해결할 능력
  * 부정적 신호 검증
    * tradeoff 로 타협을 고려하지 않고 오버 엔지니어링을 하는지
    * 과도한 엔지니어링으로 시스템 비용이 올라감
    * 완고함, 편협함

## 효과적 면접을 위한 4단계 접근법

### 1단계 문제 이해 및 설계 범위 확정
* 문제에 대해 바로 답은 내면 안된다.
* 면접은 퀴즈 쇼가 아니다.
  * 속도를 늦춰라.
  * 깊이 생각하고 질문하여 요구와 가정을 분명히 하라.
* 올바른 질문하는게 중요하다.
* 질문 예시
  * 구체적으로 어떤 기능을 만들어야 하는지
  * 제품 사용자 수
  * 회사의 규모가 얼마나 빨리 커질지 예상하는지
  * 회사의 기술 스택이 뭔지, 활용할 기존 서비스가 있는지
* 예제 - 뉴스피드 시스템
  * 플랫폼 지원 사양 (ios/web/android)
  * 중요한 기능 질문
  * 정렬 방법 질문 (시간역순, 포스트 가중치, 가까운 친구 우선)
  * 최대 몇명의 친구 가능
  * 트래픽 규모 질문
  * 이미지나 비디오 스펙 여부
* 질문으로 모호함을 없애는 것이 중요하다.

### 2단계 개력적인 설계안 제시 및 동의 구하기
* 설계안의 최초 청사진 제시 -> 의견 구하기 (면접관을 팀원처럼)
* 화이트보드로 핵심 컴포넌트 다이어그램 (클라, API, 웹, DB, 캐시)
* 최초 설계안이 제약사항들을 만족하는지 계산 (과정을 소리내서)
  * 개략적 추정이 필요한지는 면접관에게 물어보기
* 구체적 사용 사례 살펴보기, 엣지케이스 발견하기
* API 엔드포인트와 스키마도 보여야 하나?
  * 질문에 따라 다르다.
  * 구글 검색 엔진 설계같은 큰문제면 생략
  * 의견 물어보기

#### 예제 - 뉴스 피드 시스템

![](chapter3/image%202.png)

두가지 플로우로 나눠서 설계 해 볼 수 있음

* 피드 발행 : 사용자 포스팅 -> DB/캐시 기록 -> 친구의 뉴스피드
* 피드 생성 : 사용자 친구들의 포스트 -> 시간 역순으로 정렬


### 3단계 상세 설계
* 특정 시스템 컴포넌트의 세부 사항을 깊게 보기를 원할 것
  * 예시
    * 단축 URl 생성기 : URL 해시 함수 구체적 질문
    * 채팅 시스템 : 지연시간과 온/오프라인 상태 질문
* 시간관리 
  * 페이스북 뉴스피드 순위 알고리즘 - EdgeRank 알고리즘에 너무 깊게 설명
  * 시간을 너무 많이씀, 규모 확장 가능한 설계 능력 검증 X

#### 예제

피드 발행, 뉴스 피드 가져오기

![](chapter3/image.png)

### 4단계 마무리
* 면접관의 시스템 병목구간, 개선 가능 지점 주문
  * 완벽하다고 하거나 개선할 부분이 없다고 하면 안됨
  * 개선할 점은 항상 있다
  * 비판적 사고 능력과 좋은 인상 기회
* 설계를 면접관에게 요약해서 설명하기 - 면접관 기억 환기
* 오류가 발생하면 생기는 일 설명 (서버 오류, 네트워크 장애)
* 운영 이슈 (매트릭, 모니터링, 로그, 배포 방법)
* 미래에 닥칠 확장 요구사항에 대처할 방법
  * 백만사용자 설계 -> 천만 사용자 설계

#### 해야 할 것
* 질문을 통해 모호한 부분 확인
  * 가정이 옳다고 믿지 않기
* 문제의 요구사항 이해
* 최선이 없다고 명심하기
* 면접관에게 사고 흐름을 이해할 수 있게 하기
* 가능하면 여러 해법 제시
* 면접관이 동의하면? 각 컴포넌트의 세부사항 설명 시작
* 면접관의 아이디어 이끌어 내기
* 포기하지 말기
  #### 
#### 하지 말아야 할 것
* 전형적인 면접질문도 대비하지 않기
* 요구사항과 가정이 모호한 상태로 설계하기
* 특정 컴포넌트에 너무 깊게 설명하기 (개략적 first)
* 막히면 힌트를 청하기
* 소통을 주저하지 말기 (침묵 X)
* 설계안을 내놓은게 끝난게 아님 - 소통하고 의견을 구하기

#### 시간 배분
45분이라면 추정
* 1단계 - 문제이해/설계범위 정하기 - 3분~10분
* 2단계 - 설계안 제시하고 동의받기 - 10분~15분
* 3단계 - 상세 설계 - 10분~25분
* 4단계 마무리 - 3분~5분

#대규모시스템설계기초