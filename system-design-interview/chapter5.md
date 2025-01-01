# 5장 - 안정 해시 설계
## 해시키 재배치 문제
N개의 캐시 서버에 부하를 균등하게 나누는 보편적인 방법
serverIndex = hash(key) % N (N은 서비스 개수)
![](chapter5/image.png)<!-- {"width":349} -->
* 연산을 key % 4 로 적용하여 특정한 키가 보관된 서버로 적용한 모습
* hash(key0) % 4 == 1 : 클라이언트는 캐시에 보관된 데이터를 가져오기 위해 서버 1에 접속
* 서버 풀의 크기가 고정되어 있을 때, 데이터 분포가 균등할때 잘 작동함
* 서버가 추가되거나 기존 서버가 삭제되면 (4->3) 문제가 생김
  * 해시 재연산 -> 키 재분배 : 아래와 같이 1번서버 장애시 대규모 캐시 미스가 발생하게 됨
    * 안정 해시는 이를 해결하는 기술
      ![](chapter5/image%2027.png)<!-- {"width":451} -->

## 안정 해시
* 해시테이블의 크기가 조정될때 오직 k/n 키만 재배치하는 해시 기술
* k는 키의 개수 n은 슬롯의 개수
  * 전통적인 해시 테이블은 대부분 키를 재배치함.

### 해시 공간과 해시 링
* 해시함수 `f` 로 SHA-1 을 사용
  * 함수의 출력 값 범위는 x0, x1, x2... 과 같다고 하자.
* SHA-1 의 해시공간은 0~2^160-1
  * **x0** : 0
  * **xn**은 2^160-1
  * **x1**부터 **xn-1**까지 : 그 사이의 값

![](chapter5/image%204.png)
위 해시 공간을 구부려 접으면 아래와 같은 해시링이 됨!
![](chapter5/image%2025.png)<!-- {"width":253} -->

### 해시 서버
이 해시 함수 `f` 를 사용하면 서버를 링 위의 어떤 위치에도 대응 시킬 수 있다.
(아래는 s0, s1, s2, s3 4개의 서버를 배치해봄)
![](chapter5/image%205.png)<!-- {"width":488} -->

### 해시 키
여기서 사용된 함수는 "해시 키 재배치 문제" 에 언급된 함수와 다르고 나머지 연산을 쓰지 않는다.
캐시할 키 key0, key1, key2, key3 또한 해시링 위의 어느 지점에 배치할 수 있다.
![](chapter5/image%2028.png)<!-- {"width":488} -->

### 서버 조회
키가 저장되는 서버는? 해당 키의 위치로부터 시계방향 탐색 -> 첫번째 서버!
key0 -> 서버0, key1 -> 서버1, key2 -> 서버2, key3 -> 서버3
![](chapter5/image%2020.png)<!-- {"width":474} -->

### 서버 추가
새로운 서버 4가 추가되면? key0만 재배치되었다.
key0의 시계방향 -> 첫번째 서버가 서버 4, 다른키들은 재배치 되지 않음
![](chapter5/image%208.png)<!-- {"width":401} -->

### 서버 제거
서버 1이 삭제되면? key1만 서버2로 재배치되었다. (같은원리!)
![](chapter5/image%2010.png)<!-- {"width":401} -->

### 기본 구현법의 두 가지 문제
* 파티션의 크기가 균등하게 유지하는게 불가능하다.
  * 어떤 서버는 큰 공간, 어떤 서버는 작은 공간
  * 아래는 s1이 삭제되어서 s2만 두배나 커진 상황
    ![](chapter5/image%2021.png)<!-- {"width":429} -->
* 키의 균등 분포를 달성하기가 어렵다.
  * 서버가 다음과 같이 배치 된다면?
  * 서버1과 서버3은 아무 데이터도 없는데 대부분의 키는 서버2에 보관된다.
* 이걸 해결하기 위한 기법이 가상노드 기법
  ![](chapter5/image%2011.png)<!-- {"width":451} -->

### 가상 노드
* 하나의 서버는 N개의 가상노드를 가질 수 있다.
* 아래 예시로 서버 0과 서버 1은 3개의 가상노드를 갖는다.
  * 서버0 -> s0 -> s0_0, s0_1, s0_2
  * 서버1 -> s1 -> s1_0, s1_1, s1_2
* 따라서 각 서버는 하나가 아닌 여러 개 파티션을 관리해야 한다.
* 아래 예시는 s0 로 표시된 파티션은 서버0이 관리, s1 로 표시된 파티션은 서버1이 관리
  ![](chapter5/image%2012.png)<!-- {"width":470} -->

k0 의 시계방향 -> s1_1 가상노드 -> s1에 저장! -> 즉 서버 1
![](chapter5/image%2015.png)<!-- {"width":514} -->

* 가상노드의 개수를 늘리면 키의 분포는 점점 더 균등해진다.
* 표준편차가 작아져서 데이터가 고르게 분포되기 때문이다.
* 표준편차 : 데이터가 어떻게 퍼져 나갔는지 보이는 척도!
* 100~200개 가상 노드 : 표준 편차는 평균의 5%(200개)\~10%(100개)
* 가상노드의 개수를 늘리면? 표준 편차의 값은 더 떨어진다.
  * 가상노드 데이터를 저장할 공간이 더 많이 필요함. (trade off)
  * 시스템 요구사항에 맞게 조정해야 한다.

### 재배치할 키 결정
서버 4 추가되면? s4 부터 s3 사이 키 재배치가 필요하다.
![](chapter5/image%2017.png)<!-- {"width":451} -->
서버s1이 삭제되면? s1부터 반시계 s0 사이의 키 재배치가 필요하다.
![](chapter5/image%2022.png)<!-- {"width":451} -->

#### 안정해시의 이점
* 서버가 추가되거나 삭제될때 재배치되는 키의 수가 최소화됨
* 데이터가 보다 균등하게 분포, 수평적 규모 확장
* 핫스팟키 문제를 줄임

#대규모시스템설계기초
