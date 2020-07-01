  


---
title: "Filebeat 패치 노트"
linkTitle: "Filebeat"
type: docs
weight: 1
date: 2020-07-01
description: >
  Filebeat v7.6 패치 노트
---

# 주요 변경 사항

**모든 비트**

-   사용자 정의 정책에 대한 업그레이드 경험을 향상 시키려면 기본 ILM 정책에서 버전 정보를 제거하십시오. [14745](https://github.com/elastic/beats/pull/14745)
-   `setup`cmd를 실행 `setup.ilm.overwrite`하면 사용자 지정 정책에 대한 향상된 지원을위한 설정이 적용됩니다. [14741](https://github.com/elastic/beats/pull/14741)
-   새 라이센스 엔드 포인트 및 새 형식을 사용하도록 x-pack 라이센스 프로그램 코드를 정리하십시오. URL / _xpack / license를 / _license로 바꿉니다. [15091](https://github.com/elastic/beats/pull/15091)
-   문서 ID 필드의 이름이 @ metadata.id에서 @ metadata._id로 변경되었습니다. [15859](https://github.com/elastic/beats/pull/15859)
-   동일한 데이터 경로를 가진 두 개의 Beat 인스턴스를 동시에 실행할 수 없습니다. [14069](https://github.com/elastic/beats/pull/14069)

**Filebeat**

-  CEF 확장은 이제 CEF 안내서에 정의 된 데이터 유형에 매핑됩니다. [14342](https://github.com/elastic/beats/pull/14342)

**Journalbeat**

-   깨진 대시 보드를 제거하십시오. [15288](https://github.com/elastic/beats/pull/15288)

**Metricbeat**

-  지표와 차원 모두에 대한 Cloudwatch 지표 세트 매핑을 업데이트합니다. [15245](https://github.com/elastic/beats/pull/15245)

**Packetbeat**

-   TLS : ECS에 맞게 필드가 변경되었습니다. [15497](https://github.com/elastic/beats/pull/15497)
-   TLS : send_certificates 및 include_raw_certificates 옵션의 동작이 변경되었습니다. [15497](https://github.com/elastic/beats/pull/15497)

# 버그 수정

**모든 비트**

-   잠금 파일을 확보 할 수없는 경우 스풀링을 디스크 차단으로 무한 수정하십시오. [15338](https://github.com/elastic/beats/pull/15338)
-   `metricbeat test output`output.hosts에서 ipv6 ES 호스트로 수정 하십시오. [15368](https://github.com/elastic/beats/pull/15368)
-   `convert`선행 0으로 문자열을 정수로 변환하는 프로세서를 수정 합니다. [15513](https://github.com/elastic/beats/issues/15513) [15557](https://github.com/elastic/beats/pull/15557)
-   기존 에이전트. *, ecs.version 및 host.name 필드가 원래 이벤트에 이미 존재하는 경우 Beats가 겹쳐 쓰는 문제를 수정하십시오. [14407](https://github.com/elastic/beats/pull/14407)
-   정방향 프록시가 사용 중일 때 TLS 설정이 무시되는 문제를 해결합니다. [$ 15516](https://github.com/elastic/beats/pull/15516)
-   Beats는 더 이상 대시 보드를 사용할 수없는 경우로드를 시도하지 않습니다. [15802](https://github.com/elastic/beats/pull/15802)

**Auditbeat**

-   시스템 / 소켓 : 커널 5.x와의 호환성 문제가 해결되었습니다. [15771](https://github.com/elastic/beats/pull/15771)

**Filebeat**

-   간격이 시간으로 사용되지 않는 Filebeat 입력 httpjson의 문제를 해결하십시오. [14728](https://github.com/elastic/beats/pull/14728)
-   MISP 모듈의 Filebeat httpjson 입력에 대한 input.yml의 SSL 구성을 수정하십시오. [14767](https://github.com/elastic/beats/pull/14767)
-   s3 입력에서 새 리더를 작성할 때 컨텐츠 유형을 확인하십시오. [15252](https://github.com/elastic/beats/pull/15252) [15225](https://github.com/elastic/beats/issues/15225)
-   Netflow 입력에서 세션 재설정 감지 및 충돌이 수정되었습니다. [14904](https://github.com/elastic/beats/pull/14904)
-   handleS3Objects 함수의 오류를 처리하고 s3 입력에 대한 디버그 메시지를 추가하십시오. [15545](https://github.com/elastic/beats/pull/15545)
-   netflow : 범위 필드가없는 옵션 템플릿을 허용합니다. [15449](https://github.com/elastic/beats/pull/15449)
-   netflow : 일부 장치 (NSEL 및 Netstream)에서 바이트 / 패킷 카운터를 수정합니다. [15449](https://github.com/elastic/beats/pull/15449)
-   netflow : 필드 `class_id`를 짧게에서 길게 변경하여 일부 Cisco 장치와의 호환성을 수정하십시오 . [15449](https://github.com/elastic/beats/pull/15449)
-   Cisco ASA Firewall에 대한 고정 대시 보드. [15420](https://github.com/elastic/beats/issues/15420) [15553](https://github.com/elastic/beats/pull/15553)
-   context_timeout 구성을 추가하여 GetObjectRequest API 호출과 함께 s3 입력이 멈추는 문제를 해결하십시오. [15502](https://github.com/elastic/beats/issues/15502) [15590](https://github.com/elastic/beats/pull/15590)
-   cloudtrail 구성에 shared_credential_file을 추가하십시오. [15652](https://github.com/elastic/beats/issues/15652) [15656](https://github.com/elastic/beats/pull/15656)
-   zeek notice fileset 구성 파일에서 오타를 수정하십시오. [15764](https://github.com/elastic/beats/issues/15764) [15765](https://github.com/elastic/beats/pull/15765)
-   `elasticsearch`모듈에 대해 수집 파이프 라인을 설정할 때 Elasticsearch가 중복 와일드 카드에 대한 로그 경고를 표시하지 않도록 합니다. [15840](https://github.com/elastic/beats/issues/15840) [15900](https://github.com/elastic/beats/pull/15900)
-   `elasticsearch/audit`타임 스탬프를 올바르게 처리하도록 파일 세트를 개선하십시오 . [15942](https://github.com/elastic/beats/pull/15942)

**Heartbeat**

-   HTTP 검사를위한 메모리 초과 할당으로 인해 7.5에서 도입 된 과도한 메모리 사용량을 수정하십시오. [15639](https://github.com/elastic/beats/pull/15639)

**Metricbeat**

-   perfmon 메트릭 세트에서 인스턴스 이름을 감지하도록 정규식을 수정하십시오. [14273](https://github.com/elastic/beats/issues/14273) [14666](https://github.com/elastic/beats/pull/14666)
-   `docker.container.size`필드 값 수정 [14979](https://github.com/elastic/beats/issues/14979) [15224](https://github.com/elastic/beats/pull/15224)
-   `kibana`Kibana에서 사용할 수없는 모듈을 더 탄력적으로 만듭니다 . [15258](https://github.com/elastic/beats/issues/15258) [15270](https://github.com/elastic/beats/pull/15270)
-   perfmon 메트릭 세트에서 일부 유니 코드 문자열로 공황 예외를 수정했습니다. [15264](https://github.com/elastic/beats/issues/15264)
-   확인 `logstash`Logstash 비 가용성에 모듈이 더 탄력. [15276](https://github.com/elastic/beats/issues/15276) [15306](https://github.com/elastic/beats/pull/15306)
-   Metricbeat 자동 검색 힌트에 사용자 이름 / 암호를 추가 [15349을](https://github.com/elastic/beats/pull/15349)
-   EC2 지표 집합 및 클라우드 워치 지표 집합에 태그에 대한 도트를 추가합니다. [15843](https://github.com/elastic/beats/issues/15843) [15844](https://github.com/elastic/beats/pull/15844)
-   SQL 모듈을 사용하여 수집 한 타임 스탬프에 RFC3339 형식을 사용하십시오. [15847](https://github.com/elastic/beats/pull/15847)
-   Cloudwatch 지표 이름에 도트를 추가합니다. [15916](https://github.com/elastic/beats/issues/15916) [15917](https://github.com/elastic/beats/pull/15917)
-   `logstash-xpack`Logstash를 모니터링하기 위해 문제 모듈이 갑자기 중단되는 문제를 해결 했습니다. [15974](https://github.com/elastic/beats/issues/15974) [16044](https://github.com/elastic/beats/pull/16044)

# 추가

**모든 비트**

-   도커 요청이 마감 시간을 초과 한 경우 친숙한 로그 메시지를 추가합니다. [15336](https://github.com/elastic/beats/pull/15336)
-   GA `script`프로세서. [14325](https://github.com/elastic/beats/pull/14325)
-   `fingerprint`프로세서를 추가하십시오 . [11173](https://github.com/elastic/beats/issues/11173) [14205](https://github.com/elastic/beats/pull/14205)
-   Elasticsearch 출력에 API 키에 대한 지원을 추가하십시오. [14324](https://github.com/elastic/beats/pull/14324)
-   Kafka consumergroup metricset [14822](https://github.com/elastic/beats/pull/14822) 에서 consumer_lag 추가[](https://github.com/elastic/beats/pull/14822)
-   Kafka 대시 보드 [14863](https://github.com/elastic/beats/pull/14863) 에서 consumer_lag 사용[](https://github.com/elastic/beats/pull/14863)
-   다양한 리소스 기반 검색을 활성화하기 위해 kubernetes 자동 검색 [리팩터링 14738](https://github.com/elastic/beats/pull/14738)
-   `add_id`프로세서를 추가하십시오 . [14524](https://github.com/elastic/beats/pull/14524)
-   모든 비트에서 TLS 1.3을 활성화합니다. [12973](https://github.com/elastic/beats/pull/12973)
-   디스크 스풀링은 각 플랫폼에 잠금 파일을 작성합니다. [15338](https://github.com/elastic/beats/pull/15338)
-   Windows 패키지에 대해 DEP (Data Execution Protection)를 사용하십시오. [15149](https://github.com/elastic/beats/pull/15149)
-   사용자는 이제 설정 `monitoring.cloud.*`을 무시하도록 지정할 수 있습니다 `monitoring.elasticsearch.*`. [14,399](https://github.com/elastic/beats/issues/14399) [15,254](https://github.com/elastic/beats/pull/15254)
-   kubernetes 자동 검색에 대한 지원을 추가하여 다른 소스에서 이벤트로 추가 메타 데이터를 추가하십시오. [14875](https://github.com/elastic/beats/pull/14875)
-   ECS 1.4.0으로 업데이트하십시오. [14844](https://github.com/elastic/beats/pull/14844)
-   decode_json_fields 프로세서에 document_id 설정을 추가하십시오. [15859](https://github.com/elastic/beats/pull/15859)

**Filebeat**

-   Google Cloud Audit 로그 수집을 위해 새 파일 세트 googlecloud / audit를 추가하십시오. [15200](https://github.com/elastic/beats/pull/15200)
-   CEF 모듈에 대시 보드를 추가하십시오 (Logstash ArcSight 모듈에서 포트 됨). [14342](https://github.com/elastic/beats/pull/14342)
-   json 형식 AWS 로그를 읽기 위해 s3 입력에 expand_event_list_from_field 지원을 추가하십시오. [15,357](https://github.com/elastic/beats/issues/15357) [15,370](https://github.com/elastic/beats/pull/15370)
-   azure eventhub go SDK를 사용할 azure-eventhub 입력을 추가하십시오. [14092](https://github.com/elastic/beats/issues/14092) [14882](https://github.com/elastic/beats/pull/14882)
-   수확기 (예를 들어, 더 많은 통계를 노출 `read_offset`, `start_time`). [13395](https://github.com/elastic/beats/pull/13395)
-   구문 분석 할 수없는 syslog 메시지에 대해 log.source.address를 포함하십시오. [13268](https://github.com/elastic/beats/issues/13268) [15453](https://github.com/elastic/beats/pull/15453)
-   aws elb 파일 세트를 GA로 해제하십시오. [15426](https://github.com/elastic/beats/pull/15426) [15380](https://github.com/elastic/beats/issues/15380)
-   azure-eventhub를 파일 비트 azure 모듈과 통합하십시오 (kafka 입력 대체). [15480](https://github.com/elastic/beats/pull/15480)
-   aws s3access 파일 세트를 GA에 릴리스하십시오. [15431](https://github.com/elastic/beats/pull/15431) [15430](https://github.com/elastic/beats/issues/15430)
-   cloudtrail 파일 세트를 AWS 모듈에 추가하십시오. [14657](https://github.com/elastic/beats/issues/14657) [15227](https://github.com/elastic/beats/pull/15227)
-   Google Cloud Firewall 로그를 수집하기위한 새로운 파일 세트 googlecloud / firewall [14553](https://github.com/elastic/beats/pull/14553)
-   google-pubsub 입력 : 게시자가 승인 한 경우 ACK pub / sub 메시지 [13346](https://github.com/elastic/beats/issues/13346) [14715](https://github.com/elastic/beats/pull/14715)
-   google-pubsub 입력에서 베타 레이블을 제거하십시오. [13346](https://github.com/elastic/beats/issues/13346) [14715](https://github.com/elastic/beats/pull/14715)
-   AWS ELB 파일 세트에 대한 대시 보드를 추가하십시오. [15804](https://github.com/elastic/beats/pull/15804)
-   googlecloud 감사 로그 출력을 기반으로 event.outcome 필드를 설정하십시오. [15731](https://github.com/elastic/beats/pull/15731)
-   AWS vpcflow 파일 세트에 대한 대시 보드를 추가하십시오. [16007](https://github.com/elastic/beats/pull/16007)

**Metricbeat**

-   `system/memory`메트릭 [집합에](https://github.com/elastic/beats/pull/15492) 대한 데이터 확장[](https://github.com/elastic/beats/pull/15492)
-   `storage`스토리지 계정의 지표 값을 검색하려면 푸른 지표 세트를 추가하십시오 . [14548](https://github.com/elastic/beats/issues/14548) [15342](https://github.com/elastic/beats/pull/15342)
-   Azure 모듈에 대한 비용 경고를 추가하십시오. [15356](https://github.com/elastic/beats/pull/15356)
-   elb 모듈을 GA로 해제하십시오. [15485](https://github.com/elastic/beats/pull/15485)
-   추가 `system/network_summary`metricset을 [15,196](https://github.com/elastic/beats/pull/15196)
-   Metricbeat의 비트 모듈이 명명 된 파이프 또는 유닉스 도메인 소켓을 통해 모니터링 정보를 읽을 수 있도록합니다. [14558](https://github.com/elastic/beats/pull/14558)
-   스크립트 프로세서를 활성화하십시오. [14711](https://github.com/elastic/beats/pull/14711)
-   STAN 대시 보드 추가 [15654](https://github.com/elastic/beats/pull/15654)

**Functionbeat**

-   트리거 된 기능에 대한 모니터링 정보를 추가하십시오. [14876](https://github.com/elastic/beats/pull/14876)
-   Google Cloud Platform 지원을 추가하십시오. [13598](https://github.com/elastic/beats/pull/13598)


