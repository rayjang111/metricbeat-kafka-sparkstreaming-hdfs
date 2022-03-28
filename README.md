# KAFKA 와 Spark Streaming 을 활용한 빅데이터 환경 파이프라인 구축 프로젝트

이 프로젝트는 Kafka 와 Spark Streaming 을 중심으로 Hadoop, MetricBeats를 설치부터 시작해 스크래치 부터 시작할 수 있도록 하는 토이 프로젝트입니다.

Kafka 의 프로듀서 데이터로선 서버의 데이터를 분석하기 위해서 Metricbeat 의 System module을 사용할 계획이고 차후

System Log 분석을 위해 Filebeat 를 연동해 Syslog 분석기능도 추가할 예정입니다.

이 프로젝트의 최종적인 데이터처리 프로세스는
- 각 서버들로 부터 Metricbeat를 통한 데이터 수집후 Kafka Topic 에 전송
- SparkStreaming 을 통해 Kafka Topic 에서 데이터를 pull 해옴
- 실시간 Aggregation 을 통해 평균 사용량, 메시지 수 등을 수집
- 수집된 데이터를 HDFS 에 저장후 Hive 를 통해 조회

이룰 구현하기 위한 환경설정은 다음과 같습니다.
- Ubuntu 18.04 VM with 8 vcpu, 16gb memory, 500gb disk 3대
- multi-node Kafka Cluster
- multi-node Hadoop Cluter
- Spark with multi-node Hadoop Yarn
- Hive
- Metricbeat


--- 
### VM 생성 및 네트워크 설정
먼저 VM 을 생성하고 VM 들끼리 서로 통신할수 있게 서버 정보와 key를 공유합니다.
관련 정보:




