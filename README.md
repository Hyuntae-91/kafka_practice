# kafka_practice
카프카 공부 관련

## 카프카란
실시간 데이터 스트리밍 플랫폼
데이터 메세지를 빠른 속도로 주고 받을 수 있게 도와주는 시스템
비유하자면 우체국

### 다음과 같은 상황에서 사용
- 로그 데이터 수집
- 금융 서비스에서 실시간 거래 데이터 처리
- IoT 환경에서 센서 데이터 실시간 분석
- 마이크로서비스 간 통신

## 카프카의 핵심 구성 요소
- 생산자 (Producer)
- Broker (Kafka 서버)
  - Topic (주제)
- 소비자 (consumer)

### 생산자
- 데이터를 만들어서 Kafka 서버로 전송하는 역할

### Broker
- 데이터 전송 중개인 역할
- Kafka 서버
- Producer 가 보낸 데이터를 저장, 관리
- Kafka 는 여러개의 Broker 가 함께 동작하면서 대량의 데이터를 처리

### Topic
- 데이터를 분류해서 저장하는 카테고리
- 생산자는 특정 Topic 으로 데이터를 전송
- 소비자는 특정 Topic 에서 데이터를 읽음

### 소비자
- Kafka 에서 데이터를 꺼내서 처리하는 역할


## Pub/Sub 과의 차이점
- Kafka 는 Pub/Sub 의 상위 호환 버전

- Pub/Sub 은 메세지를 짧게 저장하거나 저장하지 않음
  - 반면, Kafka 는 디스크에 지속적으로 저장
- Pub/Sub 은 Subscriber 가 메세지를 받지 못하면 메세지가 사라짐 (손실)
  - Kafka 는 언제든 원하는 시점부터 디스크로부터 다시 읽기 가능
- Pub/Sub 은 메세지 순서를 보장하지 않음
  - Kafka 는 Partition 단위로 순서를 보장 함
- Pub/Sub 은 단순히 모든 Subscriber 에게 Broadcast
  - Kafka 는 Consumer Group 으로 처리 분산
- Pub/Sub 은 가볍고 즉각적인 메세지에 사용
  - Kafka 는 대규모 데이터 스트리밍 처리에 사용


## 시스템 구성
1. Partition
   1. Topic 은 여러개의 Partition 으로 나뉨 (분산 처리 및 데이터 처리 속도 Up)
   2. 메세지 순서는 Partition 안에서 보장
   3. Partition 이 많아지면, Consumer 가 나눠서 처리 가능 -> 병렬성
   4. 데이터가 많아져도 수평 확장
2. Offset
   1. Partition 내에서 메세지의 고유 인덱스
   2. Consumer 가 원하는 Offset 부터 다시 읽을 수 있음
   3. 장애가 발생해도 Offset 만 알면 복구 가능