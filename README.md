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
- multi-node Spark with Hadoop Yarn
- Hive
- Metricbeat


--- 
### 1.VM 생성 및 네트워크 설정

먼저 VM 을 생성하고 VM 들끼리 서로 통신할수 있게 서버 정보와 key를 공유합니다.

관련 링크:
https://rayjang111.notion.site/key-password-a0d901ff12eb4a6497a4004170819846

### 2. Kafka 설치

Kafka 와 Zookeeper을 설치해주고 구성해준다

myid 설정이 핵심

관련 링크:
https://rayjang111.notion.site/Ubuntu-18-04-Kafka-Cluster-7996e32dfbef4c7fb712e7cfa4eac3d4

### 3.하둡 클러스터 구성

하둡 클러스터 구성을 통해서 hdfs, yarn 을 준비해준다

관련링크:
https://rayjang111.notion.site/Ubuntu-18-04-10-22db1220cbc54315984d6bb4094d0a3d

### 4.Spark 클러스터 구성

Spark를 클러스터 구성하고 Yarn 을 Resource Manager 로서 관리할 수 있게 해줌

관련링크:
https://rayjang111.notion.site/Ubuntu-18-04-Spark-Cluster-535aa2d98f0c4c9c96b2114f3b20c3f0


### 5.Metric Beat 설치 및 실행

Metricbeat 를 각 서버마다 설치해주고 Output을 Kafka 로 설정

관련링크: 
https://rayjang111.notion.site/2-241593e946dd4e29954eb3b9597e7291


