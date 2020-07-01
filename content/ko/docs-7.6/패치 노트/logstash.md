---
title: "Logstash 패치 노트"
linkTitle: "Logstash"
type: docs
weight: 2
date: 2020-07-01
description: >
  Logstash v7.6 패치 노트
---

# Logstash 7.6.0 릴리스 정보

-   기능 : 내부 클래스 및 플러그인에 대한 지원 중단 로거를 소개합니다. [# 11260](https://github.com/elastic/logstash/pull/11260) 과 [# 11486](https://github.com/elastic/logstash/pull/11486)
    
    -   Deprecation 로거는 Logstash 구성 요소가 더 이상 사용되지 않는 알림을 기본 위치 인 별도의 파일에 기록하는 통합 된 방법입니다 `log/logstash-deprecation.log`. 이 파일은 사용자가 주요 업그레이드 후 작동을 멈출 수있는 기능을 사용하고 있는지 확인할 수있는 단일 위치를 제공합니다.
    
-   기능 : Logstash 모니터링 / 관리 [# 11496에](https://github.com/elastic/logstash/pull/11496) 대한 cloud-id / auth 지원 추가[](https://github.com/elastic/logstash/pull/11496)
-   기능 : [Jdbc 통합 플러그인](https://github.com/logstash-plugins/logstash-integration-jdbc) 의 초기 릴리스. 이전에 분리 된 Jdbc 플러그인과 공유 종속성을 단일 코드베이스로 결합
-   고정 : 여러 파이프 라인의 컴파일이 느려지는 회귀 [# 11560](https://github.com/elastic/logstash/issues/11560)
    
    -   [# 11482](https://github.com/elastic/logstash/issues/11482) 의 작업자 수에 비해 Java 실행 파이프 라인 컴파일 속도 저하 문제가 해결되어 여러 파이프 라인을 사용할 때 파이프 라인 컴파일 속도가 [느려졌습니다](https://github.com/elastic/logstash/issues/11482) . 이 수정은 여러 작업자를 사용할 때 회귀 및 원래 문제를 해결합니다.
    
-   퓨마를 4.x [# 11241로](https://github.com/elastic/logstash/pull/11241) 업데이트했습니다[](https://github.com/elastic/logstash/pull/11241)
-   jruby를 9.2.9.0으로 업데이트 [# 11281](https://github.com/elastic/logstash/pull/11281)
-   수정 : 플러그인 [# 11318을](https://github.com/elastic/logstash/pull/11318) 빌드 할 때 versions.yml 파일의 올바른 디렉토리 수정 : `versions.yml`기본 Java 플러그인을 빌드 할 때 불필요하게 필요한 문제가 수정되었습니다.
-   Sinatra 및 랙을 2.x [# 11354로 업데이트](https://github.com/elastic/logstash/pull/11354)
-   변경 : 기본 JRUBY_OPTS를 기본값으로 --dev로 설정 ( _고속_ 스크립트의 경우) [# 11355](https://github.com/elastic/logstash/pull/11355)
-   수정 : 사용되지 않는 Thread.exclusive 메소드 사용이 제거되어 logstash가 시작될 때마다 경고 메시지가 표시되었습니다. [# 11388](https://github.com/elastic/logstash/pull/11388)
-   Enterprise 라이센스 레벨 [구독](https://www.elastic.co/subscriptions) [번호 # 11407](https://github.com/elastic/logstash/pull/11407) 추가[](https://github.com/elastic/logstash/pull/11407)
-   [DOC] 클라우드 ID [# 11469에](https://github.com/elastic/logstash/pull/11469) 대한 모듈 전용 고지 사항 제거[](https://github.com/elastic/logstash/pull/11469)
-   [DOC] pipeline.workers [# 11474에](https://github.com/elastic/logstash/pull/11474) 대한 세부 사항 추가[](https://github.com/elastic/logstash/pull/11474)
-   [DOC] 모니터링 [# 11526](https://github.com/elastic/logstash/pull/11526) 을 위해 내부 수집기에 지원 중단 알림 추가[](https://github.com/elastic/logstash/pull/11526)
-   빌드 : 누락 된 라이센스에 대한 라이센스 보고서 작업 실패 [# 11554](https://github.com/elastic/logstash/pull/11554)
-   고정 : Docker 컨테이너 이미지가 pipeline.id도 기록하는 데 사용하는 log4j2.properties 파일이 업데이트되었습니다. [# 11567](https://github.com/elastic/logstash/pull/11567)

# 플러그인

**Jdbc 통합**

- 이전에 분리 된 Jdbc 플러그인과 공유 종속성을 단일 코드베이스로 결합한 [Jdbc 통합 플러그인](https://github.com/logstash-plugins/logstash-integration-jdbc) 의 초기 릴리스

**Cef 코덱**

- 설명서 [# 75](https://github.com/logstash-plugins/logstash-codec-cef/pull/75) 에 따라 ahost / agentHostName 필드에 대한 CEF 축약 형 이름 변환이 수정되었습니다.

**확장한 코덱**

- 나노초의 정확한 시간을 처리하기 위해 EventTime msgpack 확장 처리 및 매개 변수 [# 18](https://github.com/logstash-plugins/logstash-codec-fluent/pull/18) 추가

**DNS 필터**

-   각 놓친 조회하고 냉혹 메모리 (초래할 수있는 문제 수정 [JRuby를 버그](https://github.com/jruby/jruby/issues/6015) 상승 예외없이 미스를 조회하여 처리)를 [# 61](https://github.com/logstash-plugins/logstash-filter-dns/pull/61)
-   JRuby resolv.rb 패치에 대한 제한이 9.2.9.0 이전 버전에 추가되었습니다. [# 58](https://github.com/logstash-plugins/logstash-filter-dns/pull/58)
-   정렬되지 않은 목록 및 문서 [# 57](https://github.com/logstash-plugins/logstash-filter-dns/pull/57) 의 코드 샘플에 대한 asciidoc 형식을 수정했습니다.[](https://github.com/logstash-plugins/logstash-filter-dns/pull/57)
-   `nameserver`옵션 [# 56에](https://github.com/logstash-plugins/logstash-filter-dns/pull/56) 검색 도메인 추가

**Elasticsearch 필터**

- Feat : cloud_id / cloud_auth 구성 [# 122 지원](https://github.com/logstash-plugins/logstash-filter-elasticsearch/pull/122)

**비트 입력**

- Jackson 종속성 업데이트

**Elasticsearch 입력**

-   Feat : cloud_id / cloud_auth 구성 [# 112](https://github.com/logstash-plugins/logstash-input-elasticsearch/pull/112) 지원 추가[](https://github.com/logstash-plugins/logstash-input-elasticsearch/pull/112)
-   Manticore [# 111](https://github.com/logstash-plugins/logstash-input-elasticsearch/pull/111) 을 사용하도록 Elasticsearch Client 전송을 변경했습니다.

**파일 입력**

- `exclude`처리 중 회귀 문제를 해결하십시오 . 패턴은 전체 경로가 아니라 파일 이름과 일치합니다. [# 237](https://github.com/logstash-plugins/logstash-input-file/issues/237)

**HTTP 입력**

- CBC 암호가 여전히 많은 상황에서 사용되므로 업데이트를 netty 및 tcnative로 되돌리기

**CSV 출력**

-   문서 : 오타 수정 [# 19](https://github.com/logstash-plugins/logstash-output-csv/pull/19)
-   문서 : 코드 샘플 [# 22](https://github.com/logstash-plugins/logstash-output-csv/pull/22) 이후의 수정 형식

**Elasticsearch 출력**

- Feat : cloud_id 및 cloud_auth [# 906에](https://github.com/logstash-plugins/logstash-output-elasticsearch/pull/906) 대한 지원 추가

**S3 출력**

- [ONEZONE_IA](https://aws.amazon.com/s3/storage-classes/#__) 를 storage_class 로 지정하는 기능 추가

**Udp 출력**

-   소켓 쓰기 예외 [# 10에서](https://github.com/logstash-plugins/logstash-output-udp/pull/10) 플러그인 충돌이 해결되었습니다.[](https://github.com/logstash-plugins/logstash-output-udp/pull/10)
-   _retry_count_ 및 _retry_backoff_ms_ 옵션 [# 12에](https://github.com/logstash-plugins/logstash-output-udp/pull/12) 대한 지원 추가


