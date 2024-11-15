# 회복 탄력성
`
마이크로 서비스 환경에서 회복 탄련성과 견고성을 향상키는 방법을 알아보자
`

## 회복 탄력성이란?
- 회복탄력성을 네 가지 개념으로 분류

### 견고성
- 예상되는 문제를 수용하기 위해 소프트웨어와 프로세스에 메커니즘을 구축하는 개념
- 호스트의 문제를 자동으로 탐지하고 재시도를 수행하여 견고성을 개선할 수 있음
- 견고성은 예상치 못한 일이 발생한 후에 개선 될 수 있음
- 견고성을 높일수록 시스템에 더 많은 복잡성이 추기 됨

### 회복성
- 사전 준비를 철저히 하여 장애로 부터 회복하는 능령을 향상해야 함
- 장애가 발생했을 때 구성원들은 자기역할을 이해하고 빨리 수행할 수 있어야함 함

### 원만한 확장성
- 견고성과, 회복성과 달리 에측하지 못한 상황을 예방해야 할 필요성이 있음
- 시스템이 분산 되어 있는 수평 구조일 경우 예기치 못한 상황에 좀 더 잘 대처 할 수 있음

### 지속적인 적응력
- 회복 탄력성을 보장하는 조직을 만들기 위해 구성원 들이 하는 일을 지속적으로 적응시켜야 함 
- 시스팀에 대한 보다 전체적인 관점이 필요하고 모르는 것을 발견하려고 노력해야 함

### 그리고 마이크로서비스 아키텍쳐
- 회복 탄력성을 제공하는 능력은 시스템을 구축하고 운영하는 사람들의 속성

## 장애는 어디에서나 발생한다
- 일정 규모 이상이 되면 장애를 피할 수 없음
- 장애가 발생하지 않도록 프로세스를 통제하는 것 만큼 쉽게 복구 하는 환경을 만드는 것도 중요

## 얼마나 많아야 너무 많은 건가?
- 얼마나 많은 실패를 허용할 수 있는지 또는 시스템이 얼마나 빨라야 하는지는 시스템의 사용자에 의해 결정됨
- 사용자의 요구사항을 파악하기 위하여 올바른 정보를 수집하고 사용자가 이해하는 데 도움이 되는 질문을 지속적으로 해야 함

### 응답 시간/지연시간
- 부하 증가가 응답 시간에 어떤 영향을 주는지 
- 
### 가용성
- 서비스가 허용 가능 다운 타임기간을 측정 
- 
### 데이터 내구성
- 데이터 손실 허용 범위와, 보존 기관

## 기능 저하
- 각 장애의 영향도를 파악하고 기능을 적절하게 분산시키는 방법을 찾아야 함
- 비즈니스의 맥락을 이해하여 특정 서비스가 다운되더라도 부분적인 서비스가 가능하게 해야함

## 안정성 패턴

### 타임아웃
- 다른 서비스를 호출 할 때에는 항상 타임아웃을 설정하고 모든 곳에 기본 타임아웃 값을 지정해야 함
- 타임아웃이 발생하면 기록하고 살펴보고 정상 상태의 응답 시간을 확인해야 함
- 단일 서비스 호출에 대한 타임아웃만을 고려하지 말고 시스템 체인 전체를 고려 해야함

### 재시도 
- 다운스트림 호출의 문제는 일시적일 수 있기 때문에 재시도가 도움이 될 수 있음
- 오류의 코드를 확인하여 재시도를 해야할 지 판단해야 함

### 벌크 헤드
- 벌크 헤드(격벽)을 구현하여 한 영역에서 발생한 장애의 영향을 최소화 할 수 있음
- 자원이 포화되지 않도록 특정 조건에서 요청을 거부하는 로드셰딩 구현도 좋은 방법

### 회로 차단기
- 서비스에서 일정 이상의 에러 감지시 회로를 차단하여 호출을 하지 못하게 막음
- 서비스가 복구 됐는지 확인하면 회로 차단기를 재설정 하여 호출을 열어줌
- 회로차단기는 애플리케이션이 빠르게 실패하는 데 도움이 되며 느리게 실패하는 것보다 좋은 결과를 가져다 줄 수 있음

### 격리
- 서비스가 다른 서비스의 가용성에 많이 의존 할수록 수행 능력에 더 많은 영향을 미침
- 격리를 강화하여 서비스를 더 자유롭게 운영하고 발전시킬 수 있는 자율성을 향상 키워야 함

### 이중화
- 인스턴스를 여러개 두어 장애가 발생해도 서비스를 유지할 수 있도록 환경을 구성
- 장애 대응 뿐만 아니라 애플리케이션을 확장해 증가하는 부하를 처리하는데 도움을 줌

### 미들웨어
- 메세지 브로커를 사용하여 시스템에서 발생하는 자원 경합을 줄일 수 있음
- 일부 견고성 문제를 해소할 때 유용할 수 있지만, 모든 상황에 적용하기에는 어려움

### 멱등성
- 여러번 호출하여도 결과가 변경되지 않도록 설계 해야 함
- 처리됐는지 확실하지 않은 메세지를 재연하고자 할 때 유용하며, 에러를 복구하는 일반적인 방법

## 위험 분산
- 서비스를 논리적, 물리적으로 분리 시켜 장애 영향을 최소화 시킴

## CAP 정리
- 분산 시스템 실패 모드는 모든 것을 갖출 수 없음 일부 희생 필요
- 데이터를 동기화 하고 있는 여러 서비스에서 장애가 났다면 희생해야 할 것을 판단해야 함

### 일관성 희생
- 데이터 일관성을 포기한 채로 서비스를 가용할 수 있음
- 다중 노드의 일관성을 제대로 구현하는 것은 매우 어려음으로 직접 개발하지 않기를 권고
- 일관성을 희생한 시스템을 AP(availability, partition tolerance) 시스템이라고 함

### 가용성 희생
- 일관성을 지키기 위해, 호출을 실패 처리하여 가용성을 포기
- 가용성을 포기한 시스템을 CP(consistency, partition tolerance) 시스템이라고 함

### 단절내성 희생
- 시스템에 단절내성이 없다면 시스템은 네트워크를 통해 실행할 수 없음, 즉 로컬에서 실행하는 단일 프로세스
- CA(consistency, availability)는 분산 시스템에 존재 하지 않음

### AP 아니면 CP?
- 일관성 가용성의 중요도에 따라 상황에 맞게 설계 해야 함

### 양자택일이 아니다
- 시스템 전체가 AP나 CP일 필요는 없음 CAP의 절충안을 개별 마이크로서비스에 적용하는 것이 중요

### 그리고 현실에서는
- 시스템 안에서 일관성을 유지한다고 해도 현실 세게에서 발생하는 모든 상황을 적용 할 수 없으므로 일관성은 완벽할 수 없음
- 때문에 AP 시스템이 주로 선택 되기도 함

## 카오스 엔지니어링
- 시스템을 견고하게 유지하고 지속적인 적응성을 위한 접근 방법으로 복원력을 개선하는데 유용
- 실환경에서 격동적인 조건을 견뎌내는 시스템의 능력에 대한 신뢰를 구축하기 위해 시스템을 실험하는 분야

### 게임데이
- 카오스 엔지니어링이라는 용어가 생기기 훨씬 전부터 특정 이벤트에 대한 사람들의 준비 상태를 테스트하기 위함
- 장애 복구 의존도가 가장 높은 직원을 제외하고 모의 정전을 발생하여 장애 복구 연습

### 운영 환경의 실험
- 시스템이 실제로 견고한지를 테스트 하기 위해 운영 환경의 인프라에 장애를 발생 시킴
- 특정 머신 혹은, 가용영역 전체를 제거하는 방식으로 진행
- 
### 견고성을 넘어
- 카오스 엔지니어링을 적용하면 애플리케이션의 견고성을 개선하는 데 유용
- 카오스 엔지니어링 도구를 사용하여 시스템의 회복 탄력성에 대해 지속적으로 의문을 제기하는 접근 방식으로 활용하면 좋음

## 비난
- 장애가 발생한 후 누군가를 비난하면, 조직 문화가 경직되며, 실패로부터 배울 기회를 잃어버림
- 사람들이 실수를 했을 때 안전하게 인정할 수 있는 조직을 만드는 것은 필수적
- 회복 탄력성을 확보하려면 호기심, 즉 시스템의 약점을 끈임없이 탐구하려는 노력이 필요
- 이를 위해서는 배움의 문화가 필요하며 종종 사고를 겪은 후에 큰 깨달음을 얻을 수 있음
