---
title: "Elasticsearch 패치 노트"
linkTitle: "Elasticsearch"
type: docs
weight: 1
date: 2020-04-19
description: >
  Elasticsearch v7.6 패치 노트
---

# 알려진 문제

- Index를 축소하고 document를 삭제하거나 변경하면 index가 손상될 수 있습니다. Index의 손상을 방지하려면 index들을 축소하지 않는 것을 권장합니다. 축소한 index가 읽기 전용이라면 축소 후 강제 병합하는 것을 권장합니다. 이 문제는 Elasticsearch 7.7 버전 이상에서 해결됐습니다. 자세한 내용은 [여기](https://issues.apache.org/jira/browse/LUCENE-9300)에서 확인할 수 있습니다.

- 6.x 버전에서 만들어진 index들 중 data와 date_nanos 포맷을 사용하는 필드들은 java.time 패턴들과 호환되지 않습니다. 이 문제로 인해 분석 오류와 부정확한 날짜 계산이나 정확하지 않은 검색 결과가 발생할 수 있습니다. 이 문제는 7.7 버전 이상에서 해결됐습니다. 자세한 내용은 [여기](https://github.com/elastic/elasticsearch/pull/52555)에서 확인할 수 있습니다.

- [느린 로그](https://www.elastic.co/guide/en/elasticsearch/reference/current/index-modules-slowlog.html)는 시간이 지남에 따라 Log4j 로거에 메모리 누수가 발생하게 할 수 있습니다. 새로운 index가 생성되었을 때 새로운 Log4j 로거가 연결됩니다. Index를 삭제하더라도 Log4j가 로거들에 대한 내부 참조를 유지해서 메모리 누수를 발생시킵니다 (issue: [#56171](https://github.com/elastic/elasticsearch/issues/56171)). 이 문제는 6.8.10과 7.7.1 버전에서 해결됐습니다.

- 주 기준 날짜 패턴이 Y와 함께 제대로 작동하지 않습니다. Y를 w와 함께 사용하면 요청에 실패해서 예외가 로그에 기록됩니다 (issue: [#57128](https://github.com/elastic/elasticsearch/issues/57128)). y와 w를 같이 사용하면 부정확한 날짜 계산이 발생합니다. jvm.options 파일에 다음 행을 추가해서 이 문제를 해결할 수 있습니다.

  ```
  9-:-Djava.locale.providers=SPI,COMPAT
  ```

  이 문제는 Elasticsearch 7.7.0 버전 이상해서 해결됐습니다 (issue: [#50916](https://github.com/elastic/elasticsearch/issues/50916)).

# 주요 변경사항

**매핑**

- Cluster 설정에 _id 필드의 필드 데이터 로딩 비활성화 설정 추가 [#49166](https://github.com/elastic/elasticsearch/pull/49166) (issues: [#26472](https://github.com/elastic/elasticsearch/issues/26472), [#43599](https://github.com/elastic/elasticsearch/issues/43599))

# 자바 주요 변경사항

**보안**

- 사용자 정의 영역에서 클라이언트와 역할 매핑(RoleMapping) 지원(issues: [# 48369](https://github.com/elastic/elasticsearch/issues/48369) )

# 지원 중단

**분석**

- 낙타 사례 nGram 및 edgeNGram 토큰 화기 사용 중단 및 제거 [# 50862](https://github.com/elastic/elasticsearch/pull/50862) (문제 : [# 50561](https://github.com/elastic/elasticsearch/issues/50561) )

**권한 부여**

- kibana_user 및 kibana_dashboard_only_user 역할 지원 중단 [# 46456](https://github.com/elastic/elasticsearch/pull/46456)

**분산**

-   동기화 된 플러시 [# 50835](https://github.com/elastic/elasticsearch/pull/50835) 사용 중단 (문제 : [# 50776](https://github.com/elastic/elasticsearch/issues/50776) )
-   소프트 삭제없이 인덱스 사용 중단 [# 50502](https://github.com/elastic/elasticsearch/pull/50502)

**특징 / 지표 API**

-   인덱스 템플릿에 여러 개의 매핑이있는 경우 경고를 방출합니다. [# 50982](https://github.com/elastic/elasticsearch/pull/50982)
-   더 이상 사용되지 않는 _템플릿_ 필드를 사용할 때 경고가 발생하는지 확인하십시오 . [# 50831](https://github.com/elastic/elasticsearch/pull/50831) (문제 : [# 49460](https://github.com/elastic/elasticsearch/issues/49460) )

**인프라 / 코어**

- / _cat / nodes [# 50499](https://github.com/elastic/elasticsearch/pull/50499) 의 _로컬_ 매개 변수를 더 이상 사용하지 [마십시오](https://github.com/elastic/elasticsearch/pull/50499) (문제 : [# 50088](https://github.com/elastic/elasticsearch/issues/50088) )

**재색 인**

- [재색 인 # 49458](https://github.com/elastic/elasticsearch/pull/49458) 에서 정렬 사용 중단 (문제 : [# 47567](https://github.com/elastic/elasticsearch/issues/47567) )

**검색**

-   벡터 스크립트 함수의 서명을 업데이트하십시오. [# 48604](https://github.com/elastic/elasticsearch/pull/48604)
-   sparse_vector 필드 유형을 사용하지 않습니다. [# 48315](https://github.com/elastic/elasticsearch/pull/48315)
-   검색 요청 [# 48351](https://github.com/elastic/elasticsearch/pull/48351) 에서 할당 인식에 대한 지원 중단 경고 추가 (문제 : [# 43453](https://github.com/elastic/elasticsearch/issues/43453) )

# 새로운 기능

**집계**

-   백분위 수 집계를 지원하는 새로운 히스토그램 필드 매퍼. [# 48580](https://github.com/elastic/elasticsearch/pull/48580) (문제 : [# 48578](https://github.com/elastic/elasticsearch/issues/48578) )
-   문자열 용어에 대한 통계 집계 구현 [# 47468](https://github.com/elastic/elasticsearch/pull/47468)

**분석**

- 구현 루씬 EstonianAnalyzer, 형태소 분석기의 [# 49149](https://github.com/elastic/elasticsearch/pull/49149) (문제 : [# 48895](https://github.com/elastic/elasticsearch/issues/48895) )

**입증**

- 비밀번호로 보호 된 키 저장소 (기능 지점) [# 49210](https://github.com/elastic/elasticsearch/pull/49210)

**특징 / ILM + SLM**

-   SLM 정책 실행 [# 50454](https://github.com/elastic/elasticsearch/pull/50454) 를 기다리는 ILM 조치 (문제 : [# 45067](https://github.com/elastic/elasticsearch/issues/45067) )
-   ILM histore 상점 색인 [# 50287](https://github.com/elastic/elasticsearch/pull/50287) 추가 (문제 : [# 49180](https://github.com/elastic/elasticsearch/issues/49180) )

**특징 / 섭취**

- CSV 프로세서 [# 49509](https://github.com/elastic/elasticsearch/pull/49509) (문제 : [# 49113](https://github.com/elastic/elasticsearch/issues/49113) )

**기계 학습**

-   분류 평가 [# 49671의](https://github.com/elastic/elasticsearch/pull/49671) 구현 `precision`및 `recall`메트릭 (문제 : [# 48759](https://github.com/elastic/elasticsearch/issues/48759) )[](https://github.com/elastic/elasticsearch/pull/49671)[](https://github.com/elastic/elasticsearch/issues/48759)
-   데이터 프레임 분석 API 설명 [# 49455](https://github.com/elastic/elasticsearch/pull/49455)
-   기계 학습 모델 추론 수집 프로세서 [# 49052](https://github.com/elastic/elasticsearch/pull/49052)
-   멀티 클래스 분류 [# 47772에](https://github.com/elastic/elasticsearch/pull/47772) 대한 정확도 메트릭 구현 (문제 : [# 48759](https://github.com/elastic/elasticsearch/issues/48759) )
-   분류 및 회귀 결과에 기능 중요도 값 추가 (Tree SHapley Additive ExPlanation 또는 SHAP 사용) [# 857](https://github.com/elastic/ml-cpp/pull/857)

**매핑**

- 필드 별 메타 데이터를 추가하십시오. [# 49419](https://github.com/elastic/elasticsearch/pull/49419) (문제 : [# 33267](https://github.com/elastic/elasticsearch/issues/33267) )

**검색**

-   퍼지 간격 소스 [# 49762](https://github.com/elastic/elasticsearch/pull/49762) 추가 (문제 : [# 49595](https://github.com/elastic/elasticsearch/issues/49595) )
-   로컬로 검색 요청의 진행 상황을 추적하기 위해 리스너 추가 [# 49471](https://github.com/elastic/elasticsearch/pull/49471) (문제 : [# 49091](https://github.com/elastic/elasticsearch/issues/49091) )

# 향상

**집계**

-   재사용 가능한 HistogramValue 객체 [# 49799](https://github.com/elastic/elasticsearch/pull/49799) 추가 (문제 : [# 49683](https://github.com/elastic/elasticsearch/issues/49683) )
-   인덱스 정렬 [# 48399](https://github.com/elastic/elasticsearch/pull/48399) (문제 : [# 48130](https://github.com/elastic/elasticsearch/issues/48130) )를 기반으로 복합 집계 최적화

**배당**

-   할당 필터링 규칙에 따라 자동 확장 인덱스 [# 48974](https://github.com/elastic/elasticsearch/pull/48974)
-   손상된 노드 [# 48265](https://github.com/elastic/elasticsearch/pull/48265) 에서 noop 복사에 대한 진행중인 복구를 취소하지 마십시오 (문제 : [# 47974](https://github.com/elastic/elasticsearch/issues/47974) )
-   DiskThresholdMonitor [# 48115](https://github.com/elastic/elasticsearch/pull/48115) 에서 자동 로깅 (문제 : [# 48038](https://github.com/elastic/elasticsearch/issues/48038) )
-   INITIALIZING / RELOCATING 샤드 [# 47817에](https://github.com/elastic/elasticsearch/pull/47817) 대한 빠른 액세스 (문제 : [# 46941](https://github.com/elastic/elasticsearch/issues/46941) , [# 48579](https://github.com/elastic/elasticsearch/issues/48579) )

**분석**

-   분석기가 [# 50908에](https://github.com/elastic/elasticsearch/pull/50908) 빌드 될 때 지원 중단을 확인하십시오 (문제 : [# 42349](https://github.com/elastic/elasticsearch/issues/42349) )
-   멀티플렉서가 필터 체인 분석 모드 [# 50662를](https://github.com/elastic/elasticsearch/pull/50662) 상속하게 [하십시오](https://github.com/elastic/elasticsearch/pull/50662) (문제 : [# 50554](https://github.com/elastic/elasticsearch/issues/50554) )
-   ngram 토크 나이저 [# 49250의](https://github.com/elastic/elasticsearch/pull/49250) token_chars에서 사용자 지정 문자 허용 (문제 : [# 25894](https://github.com/elastic/elasticsearch/issues/25894) )

**입증**

-   인증 [# 49575에](https://github.com/elastic/elasticsearch/pull/49575) 디버그 / 추적 로깅 추가 (문제 : [# 49473](https://github.com/elastic/elasticsearch/issues/49473) )

**권한 부여**

-   DLS BitSet Cache [# 50535](https://github.com/elastic/elasticsearch/pull/50535) 에서 크기 증가 및 TTL [감소](https://github.com/elastic/elasticsearch/pull/50535) (문제 : [# 43669](https://github.com/elastic/elasticsearch/issues/43669) , [# 49260](https://github.com/elastic/elasticsearch/issues/49260) )
-   _monitor_snapshot_ 클러스터 권한 [# 50489](https://github.com/elastic/elasticsearch/pull/50489) 추가 (문제 : [# 50210](https://github.com/elastic/elasticsearch/issues/50210) )
-   코드 검색 [# 50068에](https://github.com/elastic/elasticsearch/pull/50068) 대한 예약 된 역할 제거 (문제 : [# 49842](https://github.com/elastic/elasticsearch/issues/49842) )
-   [코드] code_admin / code_user 역할 제거 [# 48164](https://github.com/elastic/elasticsearch/pull/48164)
-   역할 쿼리와 지연 문서 수를 해결 [# 48036](https://github.com/elastic/elasticsearch/pull/48036)

**CCR**

-   -   인덱스 [# 48915를](https://github.com/elastic/elasticsearch/pull/48915) 일시 중지 할 때 오류 메시지 개선[](https://github.com/elastic/elasticsearch/pull/48915)
-   CCR 원격 복구 [# 44514](https://github.com/elastic/elasticsearch/pull/44514) 에서 MultiFileTransfer 사용 (문제 : [# 44468](https://github.com/elastic/elasticsearch/issues/44468) )

**CRUD**

-   ID가 너무 길면 ID 세부 정보를 인쇄하십시오. [# 49433](https://github.com/elastic/elasticsearch/pull/49433)
-   동적 매핑 업데이트 [# 48817에](https://github.com/elastic/elasticsearch/pull/48817) 프리 플라이트 검사 추가 (문제 : [# 35564](https://github.com/elastic/elasticsearch/issues/35564) )

**클러스터 조정**

-  -   메타 데이터 저장소를 Lucene [# 50907](https://github.com/elastic/elasticsearch/pull/50907) 로 이동 (문제 : [# 48701](https://github.com/elastic/elasticsearch/issues/48701) )
-   맞춤 메타 데이터 도구 [# 50813](https://github.com/elastic/elasticsearch/pull/50813) 제거 (문제 : [# 48701](https://github.com/elastic/elasticsearch/issues/48701) )

**분산**

-   비공개 지수 [# 48430](https://github.com/elastic/elasticsearch/pull/48430) 의 피어 복구시 보유 임대 사용 (문제 : [# 45136](https://github.com/elastic/elasticsearch/issues/45136) )

**엔진**

-   쓰기 인덱싱 버퍼 [# 50769를](https://github.com/elastic/elasticsearch/pull/50769) 강제로 새로 고치지 마십시오[](https://github.com/elastic/elasticsearch/pull/50769)
-   if_seq_no check [# 50526에](https://github.com/elastic/elasticsearch/pull/50526) 대해 삭제 된 문서 무시[](https://github.com/elastic/elasticsearch/pull/50526)
-   [트랜스 로그 # 48843](https://github.com/elastic/elasticsearch/pull/48843) 에서 실시간으로 읽기 허용[](https://github.com/elastic/elasticsearch/pull/48843)
-   엔진 생성자 [# 48605](https://github.com/elastic/elasticsearch/pull/48605) 에서 검색 [자를](https://github.com/elastic/elasticsearch/pull/48605) 워밍업하지 마십시오 (문제 : [# 47186](https://github.com/elastic/elasticsearch/issues/47186) )
-   강제 병합 [# 48533](https://github.com/elastic/elasticsearch/pull/48533) 에서 이전 및 새 세그먼트를 인터리브하는 새 병합 정책 추가 (문제 : [# 37043](https://github.com/elastic/elasticsearch/issues/37043) )
-   새로 고침은 readLock [# 48414를](https://github.com/elastic/elasticsearch/pull/48414) 얻지 않아야합니다 (문제 : [# 47186](https://github.com/elastic/elasticsearch/issues/47186) )

**특징 / ILM + SLM**

-   새 정책에서 가능한 경우 캐시 된 단계 정책 정의 새로 고침… [# 50820](https://github.com/elastic/elasticsearch/pull/50820) (문제 : [# 48431](https://github.com/elastic/elasticsearch/issues/48431) )
-   UpdateRolloverLifecycleDateStep 재시도 가능 [# 50702](https://github.com/elastic/elasticsearch/pull/50702) (문제 : [# 48183](https://github.com/elastic/elasticsearch/issues/48183) )
-   InitializePolicyContextStep을 재 시도 할 수 있도록 [# 50685](https://github.com/elastic/elasticsearch/pull/50685) (문제 : [# 48183](https://github.com/elastic/elasticsearch/issues/48183) )
-   ILM 재시도 가능한 비동기 조치 단계 [# 50522](https://github.com/elastic/elasticsearch/pull/50522) (문제 : [# 44135](https://github.com/elastic/elasticsearch/issues/44135) , [# 48183](https://github.com/elastic/elasticsearch/issues/48183) )
-   TransportRolloverAction이 하나의 클러스터 상태 업데이트에서 실행되도록 [# 50388](https://github.com/elastic/elasticsearch/pull/50388)
-   idx가 열리고 [닫히면](https://github.com/elastic/elasticsearch/pull/48614) ILM 열기 / 닫기 단계는 noop입니다. [# 48614](https://github.com/elastic/elasticsearch/pull/48614)
-   ILM `check-rollover-ready`단계 재시도 가능 [# 48256](https://github.com/elastic/elasticsearch/pull/48256) (문제 : [# 44135](https://github.com/elastic/elasticsearch/issues/44135) )

**특징 / 섭취**

-   Foreach 프로세서-포크 재귀 호출 [# 50514](https://github.com/elastic/elasticsearch/pull/50514)
-   로그 타시 패턴으로 grok 패턴 동기화 [# 50381](https://github.com/elastic/elasticsearch/pull/50381)
-   필요한 파이프 라인을 최종 파이프 라인 [# 49470으로](https://github.com/elastic/elasticsearch/pull/49470) 교체하십시오 (문제 : [# 49247](https://github.com/elastic/elasticsearch/issues/49247) ).
-   프로세서 강화를위한 템플릿 지원 추가 [# 49093](https://github.com/elastic/elasticsearch/pull/49093)
-   on_failure 블록 [# 49076](https://github.com/elastic/elasticsearch/pull/49076) 내에 on_failure_pipeline 수집 메타 데이터 소개 (문제 : [# 44920](https://github.com/elastic/elasticsearch/issues/44920) )
-   파이프 라인 프로세서에 템플릿 지원을 추가하십시오. [# 49030](https://github.com/elastic/elasticsearch/pull/49030) (문제 : [# 39955](https://github.com/elastic/elasticsearch/issues/39955) )
-   후행 빈 필드 [# 48664](https://github.com/elastic/elasticsearch/pull/48664) 를 유지하기 위해 프로세서를 분할하는 옵션 추가 (문제 : [# 48498](https://github.com/elastic/elasticsearch/issues/48498) )
-   grok watch dog를 스레드 기반이 아닌 Matcher 기반으로 변경하십시오. [# 48346](https://github.com/elastic/elasticsearch/pull/48346) (문제 : [# 43673](https://github.com/elastic/elasticsearch/issues/43673) , [# 47374](https://github.com/elastic/elasticsearch/issues/47374) )
-   수집 사용자 에이전트 regexes.yml [# 47807](https://github.com/elastic/elasticsearch/pull/47807) 업데이트

**기능 / 자바 고급 REST 클라이언트**

-   -   HLRC [# 49657에](https://github.com/elastic/elasticsearch/pull/49657) 원격 정보 추가 (문제 : [# 47678](https://github.com/elastic/elasticsearch/issues/47678) )
-   HLRC [# 48819에](https://github.com/elastic/elasticsearch/pull/48819) 별명 삭제 (문제 : [# 47678](https://github.com/elastic/elasticsearch/issues/47678) )

**기능 / 모니터링**

-   -   상당히 낮은 모니터링 HttpExport 메모리 풋 프린트 [# 48854](https://github.com/elastic/elasticsearch/pull/48854)
-   구문 분석 시간 [# 47912](https://github.com/elastic/elasticsearch/pull/47912) 에서 프록시 기본 경로의 유효성을 검사 [하십시오](https://github.com/elastic/elasticsearch/pull/47912) (문제 : [# 47711](https://github.com/elastic/elasticsearch/issues/47711) )
-   구문 분석 시간 [# 47911](https://github.com/elastic/elasticsearch/pull/47911) 에서 색인 이름 시간 형식 설정의 유효성을 검사하십시오 (문제 : [# 47711](https://github.com/elastic/elasticsearch/issues/47711) )
-   구문 분석 시간 [# 47848](https://github.com/elastic/elasticsearch/pull/47848) 에서 모니터링 헤더 재정의 유효성 검사 (문제 : [# 47711](https://github.com/elastic/elasticsearch/issues/47711) )
-   구문 분석 시간 [# 47821](https://github.com/elastic/elasticsearch/pull/47821) 에서 모니터링 사용자 이름의 유효성을 검사 [하십시오](https://github.com/elastic/elasticsearch/pull/47821) (문제 : [# 47711](https://github.com/elastic/elasticsearch/issues/47711) )
-   구문 분석 시간 [# 47740](https://github.com/elastic/elasticsearch/pull/47740) 에서 모니터링 암호 유효성 검사 (문제 : [# 47711](https://github.com/elastic/elasticsearch/issues/47711) )

**특징 / 통계**

-   클러스터 통계 [# 48485에](https://github.com/elastic/elasticsearch/pull/48485) 수집 정보 추가 (문제 : [# 46146](https://github.com/elastic/elasticsearch/issues/46146) )

**특징 / 관찰자**

-   -   첨부 파일 생성 실패 [# 50080](https://github.com/elastic/elasticsearch/pull/50080)
-   elasticse를 실행할 때 유효하지 않은 패턴에 대해 스택 [추적을](https://github.com/elastic/elasticsearch/pull/49744) 덤프하지 마십시오… [# 49744](https://github.com/elastic/elasticsearch/pull/49744) (문제 : [# 49642](https://github.com/elastic/elasticsearch/issues/49642) )

**지리**

-   -   BKD 지원 geo_shape 및 shape 필드 [# 50141에](https://github.com/elastic/elasticsearch/pull/50141) 대한 "컨테이너"지원 (문제 : [#](https://github.com/elastic/elasticsearch/issues/41204) [41204](https://github.com/elastic/elasticsearch/pull/50141) )
-   지오그리드 집계 [# 50002](https://github.com/elastic/elasticsearch/pull/50002) 에서 지오 바운드 필터링 지원 추가[](https://github.com/elastic/elasticsearch/pull/50002)
-   더 빠른 근사 sinh / atan 수학 함수 소개 [# 49009](https://github.com/elastic/elasticsearch/pull/49009) (문제 : [# 41166](https://github.com/elastic/elasticsearch/issues/41166) )
-   GeoPolygonQueryBuilder [#](https://github.com/elastic/elasticsearch/pull/48449) 48449에 IndexOrDocValuesQuery 추가

**인프라 / 코어**

-   -   ObjectParser [# 50938에](https://github.com/elastic/elasticsearch/pull/50938) "의미 있습니까?"추가[](https://github.com/elastic/elasticsearch/pull/50938)
-   CLI 옵션 설명의 일관된 사례 [# 49635](https://github.com/elastic/elasticsearch/pull/49635)
-   서버 [# 48553](https://github.com/elastic/elasticsearch/pull/48553) 에서 JSON 형식 지정에 대한 복원력 향상 (문제 : [# 48450](https://github.com/elastic/elasticsearch/issues/48450) )
-   `--quiet`  [# 47208](https://github.com/elastic/elasticsearch/pull/47208) (문제 : [# 46900](https://github.com/elastic/elasticsearch/issues/46900) )에서 stderr를 닫지 마십시오

**인프라 / 포장**

-   -   패키지 설치 [# 50158](https://github.com/elastic/elasticsearch/pull/50158) 에서 ES_PATH_CONF를 존중하십시오.[](https://github.com/elastic/elasticsearch/pull/50158)
-   CMS에 대한 지원을 JDK 14 [# 49123](https://github.com/elastic/elasticsearch/pull/49123) 이전으로 제한 (문제 : [# 46973](https://github.com/elastic/elasticsearch/issues/46973) )
-   Windows 서비스 디먼 관리자 [# 49061의](https://github.com/elastic/elasticsearch/pull/49061) 일반 설정에서 구문 분석 된 JVM 설정 제거 (문제 : [# 48796](https://github.com/elastic/elasticsearch/issues/48796) )
-   macOS [# 48765](https://github.com/elastic/elasticsearch/pull/48765) 에서 JDK를 jdk.app에 패키지[](https://github.com/elastic/elasticsearch/pull/48765)
-   UBI 기반 Docker 이미지 [# 48710 추가](https://github.com/elastic/elasticsearch/pull/48710) (문제 : [# 48429](https://github.com/elastic/elasticsearch/issues/48429) )

**인프라 / 플러그인**

-   -   여러 플러그인 설치 진행률보고 [# 51001](https://github.com/elastic/elasticsearch/pull/51001) (문제 : [# 50924](https://github.com/elastic/elasticsearch/issues/50924) )
-   트랜잭션 [# 50924](https://github.com/elastic/elasticsearch/pull/50924) 로 여러 플러그인 설치 허용 (문제 : [# 50443](https://github.com/elastic/elasticsearch/issues/50443) )

**인프라 / 스크립팅**

-   -   스크립팅 : 컴파일 [#](https://github.com/elastic/elasticsearch/pull/50344) 50344에 ​​ScriptFactory가 필요하지 않음 (문제 : [# 49466](https://github.com/elastic/elasticsearch/issues/49466) )
-   스크립팅 : 결정적 [# 50106 인](https://github.com/elastic/elasticsearch/pull/50106) 경우 스크립트 결과 캐시 (문제 : [# 49466](https://github.com/elastic/elasticsearch/issues/49466) )
-   스크립팅 : 스크립트 결과 캐싱을위한 기초 [# 49895](https://github.com/elastic/elasticsearch/pull/49895) (문제 : [# 49466](https://github.com/elastic/elasticsearch/issues/49466) )
-   스크립팅 : 사용 가능한 언어 및 컨텍스트 추가 API [# 49652](https://github.com/elastic/elasticsearch/pull/49652) (문제 : [# 49463](https://github.com/elastic/elasticsearch/issues/49463) )
-   스크립팅 : 컨텍스트 가져 오기 REST API [# 48319 작성](https://github.com/elastic/elasticsearch/pull/48319) (문제 : [# 47411](https://github.com/elastic/elasticsearch/issues/47411) )
-   스크립팅 : 컨텍스트 이름 가져 오기 REST API [# 48026](https://github.com/elastic/elasticsearch/pull/48026) (문제 : [# 47411](https://github.com/elastic/elasticsearch/issues/47411) )

**인프라 / 설정**

-   -   IndexSetting 업데이트 로그가 더 자세한 [# 49969](https://github.com/elastic/elasticsearch/pull/49969) 가되도록 매개 변수를 추가하십시오 (문제 : [# 49818](https://github.com/elastic/elasticsearch/issues/49818) )
-   종속 설정 값의 유효성을 검사합니다. [# 49942](https://github.com/elastic/elasticsearch/pull/49942)
-   필터링 된 설정에 대한 값을 참조하지 마십시오 [# 48066](https://github.com/elastic/elasticsearch/pull/48066)

**특허**

-   -   엔터프라이즈 라이센스 [# 50735에 max_resource_units](https://github.com/elastic/elasticsearch/pull/50735) 추가[](https://github.com/elastic/elasticsearch/pull/50735)
-   라이센스 유형 [# 49418](https://github.com/elastic/elasticsearch/pull/49418) 을 제한하는 설정 추가 (문제 : [# 48508](https://github.com/elastic/elasticsearch/issues/48508) )
-   "기업"라이센스 유형 [# 49223 지원](https://github.com/elastic/elasticsearch/pull/49223) (문제 : [# 48510](https://github.com/elastic/elasticsearch/issues/48510) )

**기계 학습**

-   작업 [# 51146](https://github.com/elastic/elasticsearch/pull/51146) 에서 일찍 발견 된 1000 개 범주에 대한 감사 경고 추가 (문제 : [# 50749](https://github.com/elastic/elasticsearch/issues/50749) )
-   `num_top_feature_importance_values`회귀 및 분류에 매개 변수 추가 [# 50914](https://github.com/elastic/elasticsearch/pull/50914)
-   데이터 프레임 분석 작업 [# 50553을](https://github.com/elastic/elasticsearch/pull/50553) 강제로 삭제 구현 (문제 : [# 48124](https://github.com/elastic/elasticsearch/issues/48124) )
-   사용하지 않는 데이터 프레임 분석 상태 삭제 [# 50243](https://github.com/elastic/elasticsearch/pull/50243)
-   각 분석 보고서를 원하는 필드 매핑으로 복사하도록하십시오 [# 50219](https://github.com/elastic/elasticsearch/pull/50219) (문제 : [# 50119](https://github.com/elastic/elasticsearch/issues/50119) )
-   상태 문서 [# 50149](https://github.com/elastic/elasticsearch/pull/50149) 의 대량 인덱싱 재시도 (문제 : [# 50143](https://github.com/elastic/elasticsearch/issues/50143) )
-   데이터 프레임 분석 분류 [# 50040의](https://github.com/elastic/elasticsearch/pull/50040) 지속 / 복원 상태[](https://github.com/elastic/elasticsearch/pull/50040)
-   `randomize_seed`회귀 및 분류 설정 소개 [# 49990](https://github.com/elastic/elasticsearch/pull/49990)
-   패스 `prediction_field_type`C ++ 분석에 처리 [# 49861](https://github.com/elastic/elasticsearch/pull/49861) (문제 : [# 49796](https://github.com/elastic/elasticsearch/issues/49796) )
-   데이터 프레임 [재색 인화 # 49690](https://github.com/elastic/elasticsearch/pull/49690) 중 선택적 소스 필터링 추가 (문제 : [# 49531](https://github.com/elastic/elasticsearch/issues/49531) )
-   ML 정보 [# 49545에](https://github.com/elastic/elasticsearch/pull/49545) 기본 분류 분석기 정의 추가[](https://github.com/elastic/elasticsearch/pull/49545)
-   이상 탐지기 결과 인덱싱 실패 [# 49508에](https://github.com/elastic/elasticsearch/pull/49508) 대한 재시도 추가 (문제 : [# 45711](https://github.com/elastic/elasticsearch/issues/45711) )
-   1MB에서 1kB [# 49227](https://github.com/elastic/elasticsearch/pull/49227) 까지 데이터 프레임 분석 작업에 대한 최소 모델 메모리 제한 값 [낮추기](https://github.com/elastic/elasticsearch/pull/49227) (문제 : [# 49168](https://github.com/elastic/elasticsearch/issues/49168) )
-   `model_memory_limit`데이터 프레임 분석 작업에 대 한 사용자 경험 향상 [# 44699](https://github.com/elastic/elasticsearch/pull/44699)
-   분류 및 회귀 [# 775에](https://github.com/elastic/ml-cpp/pull/775) 대한 강화 트리 훈련 성능 향상[](https://github.com/elastic/ml-cpp/pull/775)
-   강화 된 트리 트레이닝에서 사용되는 최대 메모리를 줄이고 최대 메모리 사용량을 추정하는 과도한 버그 수정 [# 781](https://github.com/elastic/ml-cpp/pull/781)
-   회귀 [# 784에](https://github.com/elastic/ml-cpp/pull/784) 대한 층화 된 소수 교차 검증[](https://github.com/elastic/ml-cpp/pull/784)
-   기능 레코드 [# 809](https://github.com/elastic/ml-cpp/pull/809) , [# 47050에](https://github.com/elastic/elasticsearch/pull/47050)`geo_point` 대해 지원되는 출력이 추가되었습니다.`lat_long`[](https://github.com/elastic/ml-cpp/pull/809)[](https://github.com/elastic/elasticsearch/pull/47050)
-   모두 회귀 및 분류를 위해 훈련 때마다 새로운 나무의 손실 함수 유도체 계산하기 위해 데이터의 임의의 가방을 사용 [# 811](https://github.com/elastic/ml-cpp/pull/811)
-   `prediction_probability`ml 결과에서 예측 필드와 함께 필드를 방출 [# 818](https://github.com/elastic/ml-cpp/pull/818)
-   Windows에서 기계 학습 기본 프로세스의 메모리 사용량 감소 [# 844](https://github.com/elastic/ml-cpp/pull/844)
-   분류 및 회귀 런타임 감소 [# 863](https://github.com/elastic/ml-cpp/pull/863)
-   유효성 검사 오류가 더 이상 감소하지 않으면 분류 및 회귀 포리스트 조기 교육 중지 [# 875](https://github.com/elastic/ml-cpp/pull/875)
-   매개 변수 [# 877](https://github.com/elastic/ml-cpp/pull/877)`prediction_field_name` 로 제공된 유형을 사용하여 데이터 프레임 분석 결과에서 방출`prediction_field_type`[](https://github.com/elastic/ml-cpp/pull/877)
-   Quantile 추정치 업데이트 성능 개선 [# 881](https://github.com/elastic/ml-cpp/pull/881)
-   초기 하이퍼 파라미터 값 라인 검색에 베이지안 최적화를 사용하도록 마이그레이션하고 예상 개선이 너무 작은 경우 일찍 중지하십시오 [# 903](https://github.com/elastic/ml-cpp/pull/903)
-   예측 테스트 손실이 지금까지 발견 된 최적의 매개 변수 값보다 작은되는 작은 기회가 초기의 경우 교차 검증 중지 [# 915](https://github.com/elastic/ml-cpp/pull/915)
-   최소 클래스 리콜 [# 926](https://github.com/elastic/ml-cpp/pull/926) 을 최대화하기 위해 분류에 대한 결정 임계 값 최적화[](https://github.com/elastic/ml-cpp/pull/926)
-   노드 할당 결정 [# 927](https://github.com/elastic/ml-cpp/pull/927) (문제 : [# 724](https://github.com/elastic/ml-cpp/issues/724) ) 에서 고려되도록 `model_bytes`필드에 분류 메모리 사용량을 포함 `model_size_stats`시키십시오 .

**매핑**

-   평평한 필드에 원격 측정을 추가합니다. [# 48972](https://github.com/elastic/elasticsearch/pull/48972)

**회로망**

-   -   certutil http 명령 [# 49827](https://github.com/elastic/elasticsearch/pull/49827) 추가[](https://github.com/elastic/elasticsearch/pull/49827)
-   플러그인 생성자 [# 49667](https://github.com/elastic/elasticsearch/pull/49667) 에서 SSLService를로드하지 마십시오 (문제 : [# 44536](https://github.com/elastic/elasticsearch/issues/44536) )
-   Netty4 : 복합 누적 기 [# 49478로 전환](https://github.com/elastic/elasticsearch/pull/49478)
-   클러스터 설정 [# 49414에](https://github.com/elastic/elasticsearch/pull/49414) 간단한 전략 추가 (문제 : [# 49067](https://github.com/elastic/elasticsearch/issues/49067) )
-   잘못 구성된 SSL 서버 구성 [# 49280 더 이상](https://github.com/elastic/elasticsearch/pull/49280) 사용되지 않음 (문제 : [# 45892](https://github.com/elastic/elasticsearch/issues/45892) )
-   TLS 트러스트 실패에 대한 향상된 진단 기능 [# 48911](https://github.com/elastic/elasticsearch/pull/48911)

**여과기**

-   QueryVisitors [#](https://github.com/elastic/elasticsearch/pull/49238) 49238을 사용하기 위해 여과기의 QueryAnalyzer 리팩터링 (문제 : [# 45639](https://github.com/elastic/elasticsearch/issues/45639) )

**순위**

-  `search_type`순위 평가 API [# 48542](https://github.com/elastic/elasticsearch/pull/48542) 지원 (문제 : [# 48503](https://github.com/elastic/elasticsearch/issues/48503) )

**회복**

-   -   소프트 삭제 [# 50351이](https://github.com/elastic/elasticsearch/pull/50351) 없는 인덱스에 대해 피어 복구 보존 임대를 사용하십시오 (문제 : [# 45136](https://github.com/elastic/elasticsearch/issues/45136) , [# 46959](https://github.com/elastic/elasticsearch/issues/46959) )
-   복구 버퍼 크기 16B 더 작은 [# 50100](https://github.com/elastic/elasticsearch/pull/50100)

**재색 인**

-   [재색 인](https://github.com/elastic/elasticsearch/pull/49855) 정렬 사용 중단 경고에 2 [# 49855 소요](https://github.com/elastic/elasticsearch/pull/49855) (문제 : [# 49458](https://github.com/elastic/elasticsearch/issues/49458) )

**SQL**

-   SQL : ES jdbc 드라이버 파일이 다른 jar [# 51856에](https://github.com/elastic/elasticsearch/pull/51856) 번들로 제공되는 uberjar 시나리오 처리 (문제 : [# 50201](https://github.com/elastic/elasticsearch/issues/50201) )
-   SQL : 서버 [# 50530](https://github.com/elastic/elasticsearch/pull/50530) 에서 오는 검색 응답에 대한 추적 로깅 추가[](https://github.com/elastic/elasticsearch/pull/50530)
-   SQL : TRUNCATE [# 49571에](https://github.com/elastic/elasticsearch/pull/49571) TRUNC 별명 추가 (문제 : [# 41195](https://github.com/elastic/elasticsearch/issues/41195) )
-   SQL : 드라이버 및 CLI [# 48261에](https://github.com/elastic/elasticsearch/pull/48261) 대한 이진 통신 구현 (문제 : [# 47785](https://github.com/elastic/elasticsearch/issues/47785) )
-   SQL : SELECT [# 51568](https://github.com/elastic/elasticsearch/pull/51568) 에서 전체 텍스트 검색 기능이 허용되지 [않는지 확인](https://github.com/elastic/elasticsearch/pull/51568) (문제 : [# 47446](https://github.com/elastic/elasticsearch/issues/47446) )

**검색**

-   MoreLikeThisQuery [# 49966에](https://github.com/elastic/elasticsearch/pull/49966) 대해 maxQueryTerms에 대한 유효성 검증을 0보다 크게 추가하십시오 (문제 : [# 49927](https://github.com/elastic/elasticsearch/issues/49927) )
-   match_all 쿼리 [# 49717](https://github.com/elastic/elasticsearch/pull/49717) 에서 숫자 정렬 최적화 (문제 : [# 48804](https://github.com/elastic/elasticsearch/issues/48804) )
-   기본 정렬 필드 [# 49092](https://github.com/elastic/elasticsearch/pull/49092) 의 최대 / 최소값을 기반으로 사전 정렬 샤드 (문제 : [# 49091](https://github.com/elastic/elasticsearch/issues/49091) )
-   긴 필드 [# 48804](https://github.com/elastic/elasticsearch/pull/48804) 에서 정렬 최적화[](https://github.com/elastic/elasticsearch/pull/48804)
-   검색 최적화- "_index"필드 [# 48681](https://github.com/elastic/elasticsearch/pull/48681) 에서 쿼리에 대한 canMatch 조기 중단 추가 (문제 : [# 48473](https://github.com/elastic/elasticsearch/issues/48473) )
-   # 48475 순수 disjunctions는 MatchNoneQueryBuilder에 다시 작성해야 [# 48557](https://github.com/elastic/elasticsearch/pull/48557)
-   쿼리가 [# 48195](https://github.com/elastic/elasticsearch/pull/48195) 프로파일 링 될 때 캐싱 비활성화 (문제 : [# 33298](https://github.com/elastic/elasticsearch/issues/33298) )
-   BlendedTermQuery의 equals 메소드는 [# 48193](https://github.com/elastic/elasticsearch/pull/48193) 부스트를 고려해야합니다 (문제 : [# 48184](https://github.com/elastic/elasticsearch/issues/48184) )
-   2048로 벡터 [딤](https://github.com/elastic/elasticsearch/pull/46895) 의 수를 증가시킵니다 [# 46895](https://github.com/elastic/elasticsearch/pull/46895)

**보안**

-   .async-search- *를 제한된 네임 스페이스로 만들기 [# 50294](https://github.com/elastic/elasticsearch/pull/50294)
-   보안은 [# 50207을](https://github.com/elastic/elasticsearch/pull/50207) 변경하지 않은 파일을 다시로드하지 [않아야합니다](https://github.com/elastic/elasticsearch/pull/50207) (문제 : [# 50063](https://github.com/elastic/elasticsearch/issues/50063) )

**스냅 샷 / 복원**

-   클러스터 상태를 사용하여 리포지토리 생성 [# 49729](https://github.com/elastic/elasticsearch/pull/49729) 추적 (문제 : [# 49060](https://github.com/elastic/elasticsearch/issues/49060) )
-   BlobStoreRepository [# 48944의](https://github.com/elastic/elasticsearch/pull/48944) 저장소 리포지토리 [생성](https://github.com/elastic/elasticsearch/pull/48944) (문제 : [# 38941](https://github.com/elastic/elasticsearch/issues/38941) , [# 47520](https://github.com/elastic/elasticsearch/issues/47520) , [# 47834](https://github.com/elastic/elasticsearch/issues/47834) , [# 49048](https://github.com/elastic/elasticsearch/issues/49048) )
-   병렬 [# 48110의](https://github.com/elastic/elasticsearch/pull/48110) 개별 샤드 스냅 샷 파일에서 복원 (문제 : [# 42791](https://github.com/elastic/elasticsearch/issues/42791) )
-   리포지토리 루트 [# 46250](https://github.com/elastic/elasticsearch/pull/46250) 에서 샤드 스냅 샷 인덱스 생성 추적 (문제 : [# 38941](https://github.com/elastic/elasticsearch/issues/38941) , [# 45736](https://github.com/elastic/elasticsearch/issues/45736) )

**저장**

-   HybridDirectory [# 49272의](https://github.com/elastic/elasticsearch/pull/49272) mmap dim 파일 (문제 : [# 48509](https://github.com/elastic/elasticsearch/issues/48509) )

**변환**

-   오류 발생시 강제 정지 견고성 향상 [# 51072](https://github.com/elastic/elasticsearch/pull/51072)
-   메시지 [# 50140](https://github.com/elastic/elasticsearch/pull/50140) 에 실제 시간 초과 추가[](https://github.com/elastic/elasticsearch/pull/50140)
-   이전 체크 포인트 자동 삭제 [# 49496](https://github.com/elastic/elasticsearch/pull/49496)
-   스크립트 오류 [# 48887](https://github.com/elastic/elasticsearch/pull/48887) 의 오류 처리 개선 (문제 : [# 48467](https://github.com/elastic/elasticsearch/issues/48467) )
-   [# 47935](https://github.com/elastic/elasticsearch/pull/47935)`wait_for_checkpoint` 를 중지시키는 플래그 추가 (문제 : [# 45293](https://github.com/elastic/elasticsearch/issues/45293) )

# 버그 수정

**집계**

-   문서 값 [# 51920을](https://github.com/elastic/elasticsearch/pull/51920) 생성 할 때 #simpleName () 대신 #name ()을 사용하십시오 (문제 : [# 50307](https://github.com/elastic/elasticsearch/issues/50307) , [# 51847](https://github.com/elastic/elasticsearch/issues/51847) )
-   rare_terms [# 51868](https://github.com/elastic/elasticsearch/pull/51868) 에서 부적절한 버그 수정 (문제 : [# 51020](https://github.com/elastic/elasticsearch/issues/51020) )
-   합성 날짜 _ 히스토그램 [# 51172](https://github.com/elastic/elasticsearch/pull/51172) 의 시간대 지원 (문제 : [# 45199](https://github.com/elastic/elasticsearch/issues/45199) , [# 45200](https://github.com/elastic/elasticsearch/issues/45200) )
-   매핑되지 않은 [# 50869의](https://github.com/elastic/elasticsearch/pull/50869) 합성 형식 문제 해결 (문제 : [# 50600](https://github.com/elastic/elasticsearch/issues/50600) )
-   SingleBucket aggs는 먼저 버킷 파이프 라인을 [# 50103으로 줄여야합니다](https://github.com/elastic/elasticsearch/pull/50103) (문제 : [# 50054](https://github.com/elastic/elasticsearch/issues/50054) )
-   DocValueFormat.RAW # parseLong [# 49063](https://github.com/elastic/elasticsearch/pull/49063) 에서 정밀도 손실을 피하십시오 (문제 : [# 38692](https://github.com/elastic/elasticsearch/issues/38692) )
-   최소 / 최대 집계 [# 48970](https://github.com/elastic/elasticsearch/pull/48970) 에서 누락 된 값을 무시하도록 수정 (문제 : [# 48905](https://github.com/elastic/elasticsearch/issues/48905) )

**배당**

-   비공개 지수 [# 50645에](https://github.com/elastic/elasticsearch/pull/50645) 대한 샤드 크기 수집 (문제 : [# 33888](https://github.com/elastic/elasticsearch/issues/33888) )
-   자동 확장 복제 된 닫힌 인덱스 [# 48973](https://github.com/elastic/elasticsearch/pull/48973)
-   최신 버전 [# 48652](https://github.com/elastic/elasticsearch/pull/48652) 에서 생성 된 매달린 인덱스 무시 (문제 : [# 34264](https://github.com/elastic/elasticsearch/issues/34264) )
-   결정자 [# 48392](https://github.com/elastic/elasticsearch/pull/48392) 에서 음의 여유 디스크 공간 처리 (문제 : [# 48380](https://github.com/elastic/elasticsearch/issues/48380) )

**분석**

-   PreConfiguredTokenFilter [# 50912의](https://github.com/elastic/elasticsearch/pull/50912) 캐싱 수정 (문제 : [# 50734](https://github.com/elastic/elasticsearch/issues/50734) )
-   더 이상 사용되지 않는 nGram 및 edgeNGram 사용자 정의 필터 [# 50376](https://github.com/elastic/elasticsearch/pull/50376) 에서 오류 [발생](https://github.com/elastic/elasticsearch/pull/50376) (문제 : [# 50360](https://github.com/elastic/elasticsearch/issues/50360) )
-   _analyze api는 [# 48866을](https://github.com/elastic/elasticsearch/pull/48866) 지정할 때 노멀 라이저를 올바르게 사용하지 않습니다 (문제 : [# 48650](https://github.com/elastic/elasticsearch/issues/48650) )

**심사**

-   감사 로그 필터 및 마커 [# 45456](https://github.com/elastic/elasticsearch/pull/45456) (문제 : [# 47251](https://github.com/elastic/elasticsearch/issues/47251) )

**입증**

-   비동기 검증을 위해 ApiKey 자격 증명 유지 [# 51244](https://github.com/elastic/elasticsearch/pull/51244)
-   토큰 / apikeys [# 51042에](https://github.com/elastic/elasticsearch/pull/51042) 대해 익명으로 대체하지 마십시오 (문제 : [# 50171](https://github.com/elastic/elasticsearch/issues/50171) )
-   OpenIDConnect 컬렉션 [# 50521로](https://github.com/elastic/elasticsearch/pull/50521) 사용자 메타 데이터를 채 웁니다 (문제 : [# 50250](https://github.com/elastic/elasticsearch/issues/50250) )
-   유효하지 않은 토큰 [# 49736에](https://github.com/elastic/elasticsearch/pull/49736) 대해 항상 401을 반환합니다 (문제 : [# 38866](https://github.com/elastic/elasticsearch/issues/38866) ).
-   스마트 영역 순서에서 1부터 반복 버그 수정 [# 49473](https://github.com/elastic/elasticsearch/pull/49473)
-   OIDC [# 48746에](https://github.com/elastic/elasticsearch/pull/48746) 대해 기록 된 불필요한 세부 사항 제거[](https://github.com/elastic/elasticsearch/pull/48746)
-   나머지 스펙 [# 48500에](https://github.com/elastic/elasticsearch/pull/48500) 소유자 플래그 매개 변수 추가 (문제 : [# 48499](https://github.com/elastic/elasticsearch/issues/48499) )

**권한 부여**

-   DLS [비트](https://github.com/elastic/elasticsearch/pull/50635) 캐시 [350635](https://github.com/elastic/elasticsearch/pull/50635) 에서 메모리 누수 수정 (문제 : [# 49261](https://github.com/elastic/elasticsearch/issues/49261) )
-   유효성 검사 필드 권한은 역할을 만들 때 [# 50212](https://github.com/elastic/elasticsearch/pull/50212) (: 문제 [# 46275](https://github.com/elastic/elasticsearch/issues/46275) , [# 48108를](https://github.com/elastic/elasticsearch/issues/48108) )
-   역할 [# 48108을](https://github.com/elastic/elasticsearch/pull/48108) 작성할 때 필드 권한의 유효성을 검증 [하십시오](https://github.com/elastic/elasticsearch/pull/48108) (문제 : [#](https://github.com/elastic/elasticsearch/issues/46275) [46275](https://github.com/elastic/elasticsearch/pull/48108) )

**CCR**

-   CCR은 거부 된 실행 예외를 자동 재 시도해야합니다. [# 49213](https://github.com/elastic/elasticsearch/pull/49213)

**CRUD**

-   너무 많은 동시 매핑 업데이트 [# 51038 차단](https://github.com/elastic/elasticsearch/pull/51038) (문제 : [# 50670](https://github.com/elastic/elasticsearch/issues/50670) )
-   GetResult [# 50112](https://github.com/elastic/elasticsearch/pull/50112) 에서 메타 및 문서 필드 맵이 널이 [아닌지 확인하십시오](https://github.com/elastic/elasticsearch/pull/50112) (문제 : [# 48215](https://github.com/elastic/elasticsearch/issues/48215) )
-   그들을 [fsyncing](https://github.com/elastic/elasticsearch/pull/49746) 전에 쓰기 동작을 복제 [# 49746](https://github.com/elastic/elasticsearch/pull/49746)
-   스크립팅 된 upsert [# 49578](https://github.com/elastic/elasticsearch/pull/49578) 에서 요청을 변경하지 마십시오 (문제 : [# 48670](https://github.com/elastic/elasticsearch/issues/48670) )
-   전송 중지 예외 [# 48930](https://github.com/elastic/elasticsearch/pull/48930) 수정 (문제 : [# 42612](https://github.com/elastic/elasticsearch/issues/42612) )
-   업데이트 [# 48707](https://github.com/elastic/elasticsearch/pull/48707) 에서 일관된 소스 반환[](https://github.com/elastic/elasticsearch/pull/48707)
-   인덱스 서비스 생성 실패 [# 48230](https://github.com/elastic/elasticsearch/pull/48230) 에서 쿼리 캐시 닫기 (문제 : [# 48186](https://github.com/elastic/elasticsearch/issues/48186) )

**클러스터 조정**

-   복제 된 닫힌 매달린 인덱스 가져 오기 [# 50649](https://github.com/elastic/elasticsearch/pull/50649)
-   시작시 삭제 된 인덱스의 메타 데이터 무시 [# 48918](https://github.com/elastic/elasticsearch/pull/48918)
-   elasticsearch-node 도구 사용자 정의 메타 데이터 인식 [# 48390 만들기](https://github.com/elastic/elasticsearch/pull/48390)

**디스커버리 플러그인**

-   EC2 Discovery Cache를 빈 시드 호스트 목록 [# 50607로 설정](https://github.com/elastic/elasticsearch/pull/50607) (문제 : [# 50550](https://github.com/elastic/elasticsearch/issues/50550) )
-   EC2 [감지](https://github.com/elastic/elasticsearch/issues/50462) 플러그인 재시도 요청 [# 50550](https://github.com/elastic/elasticsearch/pull/50550) (문제 : [# 50462](https://github.com/elastic/elasticsearch/issues/50462) )

**분산**

-   LuceneChangesSnapshot에 중첩 된 문서를 제외 [# 51279](https://github.com/elastic/elasticsearch/pull/51279)
-   닫힌 파편은 새 엔진 [# 47186을](https://github.com/elastic/elasticsearch/pull/47186) 열면 안됩니다 (문제 : [# 45263](https://github.com/elastic/elasticsearch/issues/45263) , [# 47060](https://github.com/elastic/elasticsearch/issues/47060) )
-   작업 인덱스 매핑 [# 50363](https://github.com/elastic/elasticsearch/pull/50363) 의 메타 버전 수정 (문제 : [# 48393](https://github.com/elastic/elasticsearch/issues/48393) )

**엔진**

-   세그먼트 통계 [# 51331의](https://github.com/elastic/elasticsearch/pull/51331) 소프트 삭제 리더를 래핑하지 마십시오 (문제 : [# 51192](https://github.com/elastic/elasticsearch/issues/51192) , [# 51303](https://github.com/elastic/elasticsearch/issues/51303) )
-   FrozenEngine [# 51192의](https://github.com/elastic/elasticsearch/pull/51192) 계정 소프트 삭제 (문제 : [# 50775](https://github.com/elastic/elasticsearch/issues/50775) )
-   커밋 된 트랜스 로그 생성 [# 50205의](https://github.com/elastic/elasticsearch/pull/50205) 계정 트림 [AboveSeqNo](https://github.com/elastic/elasticsearch/pull/50205) (문제 : [# 49970](https://github.com/elastic/elasticsearch/issues/49970) )
-   새로운 글로벌 체크 포인트 [# 48559에](https://github.com/elastic/elasticsearch/pull/48559) 대해 [탐욕적으로](https://github.com/elastic/elasticsearch/pull/48559) 안전한 커밋을 진행 [하십시오](https://github.com/elastic/elasticsearch/pull/48559) (문제 : [# 48532](https://github.com/elastic/elasticsearch/issues/48532) )
-   참조되지 않은 독자를 다듬을 때 예외를 무시하지 마십시오 [# 48470](https://github.com/elastic/elasticsearch/pull/48470)

**특징 / 특징**

-   X-Pack 스케줄러 [엔진](https://github.com/elastic/elasticsearch/pull/48951) 종료 [# 48951 수정](https://github.com/elastic/elasticsearch/pull/48951)

**특징 / ILM + SLM**

-   복원 진행중인 SLM 검사 수정 [# 50868](https://github.com/elastic/elasticsearch/pull/50868)
-   ILM 정책 단계 검색 실패 처리 [# 49193](https://github.com/elastic/elasticsearch/pull/49193) (문제 : [#](https://github.com/elastic/elasticsearch/issues/49128) [49128](https://github.com/elastic/elasticsearch/pull/49193) )
-   정책 트리거 예외 [# 49128](https://github.com/elastic/elasticsearch/pull/49128) 에서 정책 실행을 중단하지 마십시오[](https://github.com/elastic/elasticsearch/pull/49128)
-   ILM의 단계별 API [# 48827](https://github.com/elastic/elasticsearch/pull/48827) 을 사용할 때 정책 단계 JSON을 다시 읽으 [십시오.](https://github.com/elastic/elasticsearch/pull/48827)
-   서비스가 [# 48658](https://github.com/elastic/elasticsearch/pull/48658) 중지 된 경우 SLM 작업을 예약하지 마십시오 (문제 : [# 47749](https://github.com/elastic/elasticsearch/issues/47749) )
-   SLM 통계가 7.4 [# 48367](https://github.com/elastic/elasticsearch/pull/48367) 에서 전체 업그레이드를 차단하지 않는지 확인[](https://github.com/elastic/elasticsearch/pull/48367)
-   SLM 통계가 7.4 [# 48361](https://github.com/elastic/elasticsearch/pull/48361) 에서 전체 업그레이드를 차단하지 않도록하십시오[](https://github.com/elastic/elasticsearch/pull/48361)
-   xpack 사용법 및 정보 API [# 48096에](https://github.com/elastic/elasticsearch/pull/48096) SLM 지원 추가 (문제 : [# 43663](https://github.com/elastic/elasticsearch/issues/43663) )
-   slm.get_lifecycle [# 47766의](https://github.com/elastic/elasticsearch/pull/47766) 목록 유형으로 policy_id를 변경하십시오 (문제 : [# 47765](https://github.com/elastic/elasticsearch/issues/47765) )

**특징 / 섭취**

-   CsvProcessor [# 51600](https://github.com/elastic/elasticsearch/pull/51600) 에서 ignore_missing 수정[](https://github.com/elastic/elasticsearch/pull/51600)
-   SetSecurityUserProcessor [# 51454로](https://github.com/elastic/elasticsearch/pull/51454) 대상 필드를 덮어 쓰지 마십시오 (문제 : [# 51428](https://github.com/elastic/elasticsearch/issues/51428) )
-   프로세서가 비동기를 실행하는 경우 수집 시뮬레이션 응답 문서 순서 수정 [# 50244](https://github.com/elastic/elasticsearch/pull/50244)
-   geoip 수집 프로세서 [# 49573](https://github.com/elastic/elasticsearch/pull/49573) 에서 IP 목록 허용 (문제 : [# 46193](https://github.com/elastic/elasticsearch/issues/46193) )
-   IAE [# 48816을 사용](https://github.com/elastic/elasticsearch/pull/48816) 하여 수집 프로세서 예외를 래핑하지 마십시오 (문제 : [# 48810](https://github.com/elastic/elasticsearch/issues/48810) )
-   전용 수집 프로세서 예외 [# 48810](https://github.com/elastic/elasticsearch/pull/48810) 소개 (문제 : [# 48803](https://github.com/elastic/elasticsearch/issues/48803) )

**기능 / 자바 고급 REST 클라이언트**

-   es7 노드 http publish_address 형식 [# 49279 지원](https://github.com/elastic/elasticsearch/pull/49279) (문제 : [# 48950](https://github.com/elastic/elasticsearch/issues/48950) )
-   HLRC [# 48420](https://github.com/elastic/elasticsearch/pull/48420) 에서 쿼리로 삭제 및 업데이트 할 슬라이스 추가[](https://github.com/elastic/elasticsearch/pull/48420)
-   잘못된 비교 수정 [# 48208](https://github.com/elastic/elasticsearch/pull/48208)
-   CancelTasks 응답 [# 47017](https://github.com/elastic/elasticsearch/pull/47017) 의 HLRC 구문 분석 수정[](https://github.com/elastic/elasticsearch/pull/47017)
-   별도의 스케줄러를 사용하여 교착 상태 방지 [# 48697](https://github.com/elastic/elasticsearch/pull/48697) (문제 : [# 41451](https://github.com/elastic/elasticsearch/issues/41451) , [# 47599](https://github.com/elastic/elasticsearch/issues/47599) )

**기능 / 자바 저수준 REST 클라이언트**

-  응답에 경고 값 추출 성능 향상 [# 50208](https://github.com/elastic/elasticsearch/pull/50208) (문제 : [# 24114](https://github.com/elastic/elasticsearch/issues/24114) )

**기능 / 모니터링**

-   내보내기 유형이 HTTP 내보내기 [# 49992에](https://github.com/elastic/elasticsearch/pull/49992) 대해 HTTP [인지 확인](https://github.com/elastic/elasticsearch/pull/49992) (문제 : [# 47246](https://github.com/elastic/elasticsearch/issues/47246) , [# 47711](https://github.com/elastic/elasticsearch/issues/47711) , [# 49942](https://github.com/elastic/elasticsearch/issues/49942) )
-   APM system_user [# 47668](https://github.com/elastic/elasticsearch/pull/47668) (문제 : [# 2708](https://github.com/elastic/elasticsearch/issues/2708) , [# 40876](https://github.com/elastic/elasticsearch/issues/40876) )

**지리**

-   null geoBoundingBox [# 50506 방지](https://github.com/elastic/elasticsearch/pull/50506) (문제 : [# 50505](https://github.com/elastic/elasticsearch/issues/50505) )
-   Geo : 생성 된 GeoJson 유형 이름을 낙타 케이스로 전환합니다 (# 50285) [# 50400](https://github.com/elastic/elasticsearch/pull/50400) (문제 : [# 49568](https://github.com/elastic/elasticsearch/issues/49568) )
-   지역 : 생성 된 WKT를 대문자 [# 50285로 전환](https://github.com/elastic/elasticsearch/pull/50285) (문제 : [# 49568](https://github.com/elastic/elasticsearch/issues/49568) )
-   GeoPointFieldMapper [# 49645](https://github.com/elastic/elasticsearch/pull/49645) 에서 null_value를 할당 할 때 오타 수정[](https://github.com/elastic/elasticsearch/pull/49645)
-   레거시 geo_shape 쿼리 [# 49410](https://github.com/elastic/elasticsearch/pull/49410) 에서 서클 처리 문제 [수정](https://github.com/elastic/elasticsearch/pull/49410) (문제 : [# 49296](https://github.com/elastic/elasticsearch/issues/49296) )
-   GEO : geo_shape 검색과 교차하여 잘못된 결과를 반환 함 [# 49017](https://github.com/elastic/elasticsearch/pull/49017)
-   Geo : 라인 스트링 [# 47939](https://github.com/elastic/elasticsearch/pull/47939) 의 범위를 벗어난 포인트 처리 개선 (문제 : [# 43916](https://github.com/elastic/elasticsearch/issues/43916) )

**강조 표시**

-   키워드 필드 [# 49566](https://github.com/elastic/elasticsearch/pull/49566) 에서 유효하지 않은 break iterator 강조 표시 수정

**인프라 / 코어**

-   [# 51581](https://github.com/elastic/elasticsearch/pull/51581) (문제 : [# 49914](https://github.com/elastic/elasticsearch/issues/49914) ) 이 사라지는 가상 이더넷 장치 무시
-   근본 원인 지원 추측 [풀기 # 50525](https://github.com/elastic/elasticsearch/pull/50525) (문제 : [# 50417](https://github.com/elastic/elasticsearch/issues/50417) )
-   완전히 제공된 시간 [# 50178](https://github.com/elastic/elasticsearch/pull/50178) 없이 구문 분석 시간대 허용 (문제 : [# 49351](https://github.com/elastic/elasticsearch/issues/49351) )
-   [Java.time] 포맷터 [# 48703](https://github.com/elastic/elasticsearch/pull/48703) 에서 접두사 날짜 패턴 유지 (문제 : [# 48698](https://github.com/elastic/elasticsearch/issues/48698) )
-   jdk8 / windows [# 48657](https://github.com/elastic/elasticsearch/pull/48657) 에서 사용자의 MaxDirectMemorySize 플래그를 삭제하지 마십시오 (문제 : [# 44174](https://github.com/elastic/elasticsearch/issues/44174) , [# 48365](https://github.com/elastic/elasticsearch/issues/48365) )
-   MaxDirectMemorySize가 올바르지 않은 경우 경고 (Windows / JDK8 전용 문제) [# 48365](https://github.com/elastic/elasticsearch/pull/48365) (문제 : [# 47384](https://github.com/elastic/elasticsearch/issues/47384) )
-   [Java.time] ISO 규칙 [# 48209](https://github.com/elastic/elasticsearch/pull/48209) (문제 : [# 41670](https://github.com/elastic/elasticsearch/issues/41670) , [# 42588](https://github.com/elastic/elasticsearch/issues/42588) , [# 43275](https://github.com/elastic/elasticsearch/issues/43275) , [# 43652](https://github.com/elastic/elasticsearch/issues/43652) ) 로 1 주일을 계산 합니다.

**인프라 / 로깅**

-   느린 로그는 각 인덱스 [# 47234](https://github.com/elastic/elasticsearch/pull/47234) 에 대해 별도의 기본 로거를 사용해야합니다 (문제 : [# 42432](https://github.com/elastic/elasticsearch/issues/42432) )

**인프라 / 포장**

-   시작 [# 49784](https://github.com/elastic/elasticsearch/pull/49784) 중 시스템 시간 초과 연장 (문제 : [# 49593](https://github.com/elastic/elasticsearch/issues/49593) )

**인프라 / REST API**

-   잘못된 JSON [# 49552를](https://github.com/elastic/elasticsearch/pull/49552) 처리 할 때 400을 반환합니다 (문제 : [# 49428](https://github.com/elastic/elasticsearch/issues/49428) )
-   URL의 indices.put_mapping 놓친 슬래시 [# 49468를](https://github.com/elastic/elasticsearch/pull/49468)

**기계 학습**

-   find_file_structure [# 51469](https://github.com/elastic/elasticsearch/pull/51469) 에서 2 자리 연도 정규식 수정[](https://github.com/elastic/elasticsearch/pull/51469)
-   분류 `dependent_variable`카디널리티 검증 이 2 이상인 경우 [# 51232](https://github.com/elastic/elasticsearch/pull/51232)
-   회귀 분석에서 종속 변수에서 예측 필드로의 매핑을 복사하지 마십시오 [# 51227](https://github.com/elastic/elasticsearch/pull/51227)
-   매핑을 복사 할 때 제대로 중첩 및 별칭 필드를 처리 [# 50918을](https://github.com/elastic/elasticsearch/pull/50918) (문제 : [# 50787](https://github.com/elastic/elasticsearch/issues/50787) )
-   `ml_classic`토크 나이저 엔드 오프셋 [# 50655의 개별](https://github.com/elastic/elasticsearch/pull/50655) 오류 수정[](https://github.com/elastic/elasticsearch/pull/50655)
-   결과 문서 ID [# 50644의](https://github.com/elastic/elasticsearch/pull/50644) 고유성 향상 (문제 : [# 50613](https://github.com/elastic/elasticsearch/issues/50613) )
-   멀티 클래스 혼란 매트릭스에서 수정 정확도 메트릭 [# 50310](https://github.com/elastic/elasticsearch/pull/50310) (문제 : [# 48759](https://github.com/elastic/elasticsearch/issues/48759) )
-   [# 50276](https://github.com/elastic/elasticsearch/pull/50276) 을 시작한 직후 데이터 프레임 분석 작업을 중지 할 때 경쟁 조건 수정 (문제 : [# 49680](https://github.com/elastic/elasticsearch/issues/49680) , [# 50177](https://github.com/elastic/elasticsearch/issues/50177) )
-   데이터 프레임 분석 메모리 추정 [# 49517](https://github.com/elastic/elasticsearch/pull/49517) 에 소스 쿼리 적용 (문제 : [# 49454](https://github.com/elastic/elasticsearch/issues/49454) )
-   분산이 0 일 때 r_squared eval 수정 [# 49439](https://github.com/elastic/elasticsearch/pull/49439)
-   많은 예측 필드 이름을 블랙리스트에 [올립니다](https://github.com/elastic/elasticsearch/issues/48808) [# 49371](https://github.com/elastic/elasticsearch/pull/49371) (문제 : [# 48808](https://github.com/elastic/elasticsearch/issues/48808) )
-   매우 짧은 수명의 분석을 위해 데이터 프레임 분석을보다 강력하게 만듭니다 [# 49282](https://github.com/elastic/elasticsearch/pull/49282) (문제 : [# 49095](https://github.com/elastic/elasticsearch/issues/49095) )
-   계절성 [# 852를](https://github.com/elastic/ml-cpp/pull/852) 결정할 때 잠재적 인 메모리 손상 수정[](https://github.com/elastic/ml-cpp/pull/852)
-   `prediction_field_name`기계 학습 결과의 다른 필드와 충돌 방지 [# 861](https://github.com/elastic/ml-cpp/pull/861)
-   분류 역 검색 [# 950](https://github.com/elastic/ml-cpp/pull/950) (문제 : [# 949](https://github.com/elastic/ml-cpp/issues/949) ) 에 비 순차적 용어와 비 순차적 용어를 포함

**매핑**

-   필드 축소가 필드 별명과 함께 작동하는지 확인하십시오. [# 50722](https://github.com/elastic/elasticsearch/pull/50722) (문제 : [# 32648](https://github.com/elastic/elasticsearch/issues/32648) , [# 50121](https://github.com/elastic/elasticsearch/issues/50121) )
-   DateFieldMapper `ignore_malformed`처리 [# 50090](https://github.com/elastic/elasticsearch/pull/50090) 개선 (문제 : [# 46675](https://github.com/elastic/elasticsearch/issues/46675) , [# 50081](https://github.com/elastic/elasticsearch/issues/50081) )
-   주석이 달린 텍스트 유형은 TextFieldType [# 49555를](https://github.com/elastic/elasticsearch/pull/49555) 확장해야합니다 (문제 : [# 49289](https://github.com/elastic/elasticsearch/issues/49289) ).
-   병합 된 맵핑을 병합 할 때 매개 변수가 업데이트되는지 확인하십시오. [# 48971](https://github.com/elastic/elasticsearch/pull/48971) (문제 : [# 48907](https://github.com/elastic/elasticsearch/issues/48907) )

**회로망**

-  TransportMasterNodeAction이 NodeClosedException [# 51325를](https://github.com/elastic/elasticsearch/pull/51325) 다시 시도하지 않는 문제 수정

**여과기**

-   중첩 된 분리 [# 50669에](https://github.com/elastic/elasticsearch/pull/50669) 대한 MSM을 올바르게 처리합니다 (문제 : [# 50305](https://github.com/elastic/elasticsearch/issues/50305) ).
-   용어 및 범위 [# 49803](https://github.com/elastic/elasticsearch/pull/49803) 의 혼합 된 결합에 대한 쿼리 분석기 로직 수정 (문제 : [#](https://github.com/elastic/elasticsearch/issues/49684) [49684](https://github.com/elastic/elasticsearch/pull/49803) )

**회복**

-   복구 [# 50656](https://github.com/elastic/elasticsearch/pull/50656) 에서 샤드 실패시 할당 ID 확인 (문제 : [# 50508](https://github.com/elastic/elasticsearch/issues/50508) )
-   [트랜스 로그](https://github.com/elastic/elasticsearch/pull/49448) 에서 보존리스 [# 49448](https://github.com/elastic/elasticsearch/pull/49448) 으로 피어 복구 마이그레이션 (문제 : [# 45136](https://github.com/elastic/elasticsearch/issues/45136) )
-   [트랜스 로그가](https://github.com/elastic/elasticsearch/pull/49114) 손상된 경우 피어 복구에서 Lucene 인덱스 무시 [# 49114](https://github.com/elastic/elasticsearch/pull/49114)

**재색 인**

-   RED 샤드 [# 45830에서 색인 재 작성](https://github.com/elastic/elasticsearch/pull/45830) 및 친구 실패 (문제 : [# 42612](https://github.com/elastic/elasticsearch/issues/42612) , [# 45739](https://github.com/elastic/elasticsearch/issues/45739) )

**SQL**

-   SQL : [# 51675](https://github.com/elastic/elasticsearch/pull/51675) 간격으로 밀리 초 처리 수정 (문제 : [# 41635](https://github.com/elastic/elasticsearch/issues/41635) )
-   SQL : ORDER BY YEAR () 함수 [# 51562 수정](https://github.com/elastic/elasticsearch/pull/51562) (문제 : [# 51224](https://github.com/elastic/elasticsearch/issues/51224) )
-   SQL : 지원되지 않는 데이터 형식 필드 처리 방식 변경 [# 50823](https://github.com/elastic/elasticsearch/pull/50823)
-   SQL : 결합 병합 [# 50703에](https://github.com/elastic/elasticsearch/pull/50703) 대한 최적화 수정 (문제 : [#](https://github.com/elastic/elasticsearch/issues/49637) [49637](https://github.com/elastic/elasticsearch/pull/50703) )
-   SQL : CAST 및 NULL 검사 문제 수정. [# 50371](https://github.com/elastic/elasticsearch/pull/50371) (문제 : [# 50191](https://github.com/elastic/elasticsearch/issues/50191) )
-   SQL : JdbcResultSet.getDate (param, Calendar) 호출에 대한 NPE 수정 [# 50184](https://github.com/elastic/elasticsearch/pull/50184) (문제 : [# 50174](https://github.com/elastic/elasticsearch/issues/50174) )
-   SQL : COUNT DISTINCT는 일치하는 문서 [# 50037에](https://github.com/elastic/elasticsearch/pull/50037) 대해 NULL 대신 0을 리턴합니다 (문제 : [# 50013](https://github.com/elastic/elasticsearch/issues/50013) )
-   LOCATE 기능 선택적 매개 변수 처리 [# 49666 수정](https://github.com/elastic/elasticsearch/pull/49666) (문제 : [#](https://github.com/elastic/elasticsearch/issues/49557) [49557](https://github.com/elastic/elasticsearch/pull/49666) )
-   FLOOR 및 CEIL 함수 [# 49644에](https://github.com/elastic/elasticsearch/pull/49644) 대한 NULL 처리 수정 (문제 : [# 49556](https://github.com/elastic/elasticsearch/issues/49556) )
-   INTERVAL [# 49633으로](https://github.com/elastic/elasticsearch/pull/49633) NULL 산술 연산 처리 (문제 : [# 49297](https://github.com/elastic/elasticsearch/issues/49297) )
-   GROUP BY YEAR ()와 수정 문제 [# 49559](https://github.com/elastic/elasticsearch/pull/49559) (문제 : [# 49386](https://github.com/elastic/elasticsearch/issues/49386) )
-   CASE / IIF 사전 계산 결과 [# 49553](https://github.com/elastic/elasticsearch/pull/49553) 관련 문제 [수정](https://github.com/elastic/elasticsearch/pull/49553) (문제 : [# 49388](https://github.com/elastic/elasticsearch/issues/49388) )
-   CASE / IIF [# 49449](https://github.com/elastic/elasticsearch/pull/49449) 접기 문제 해결 (문제 : [# 49387](https://github.com/elastic/elasticsearch/issues/49387) )
-   WEEK / ISO_WEEK / DATEDIFF [# 49405](https://github.com/elastic/elasticsearch/pull/49405) 관련 문제 [수정](https://github.com/elastic/elasticsearch/pull/49405) (문제 : [# 48209](https://github.com/elastic/elasticsearch/issues/48209) , [# 49376](https://github.com/elastic/elasticsearch/issues/49376) )
-   SQL : DATEDIFF [# 49252의](https://github.com/elastic/elasticsearch/pull/49252) 분 및 시간 문제 수정[](https://github.com/elastic/elasticsearch/pull/49252)
-   SQL : 다른 ExpressionIds [# 43072](https://github.com/elastic/elasticsearch/pull/43072) 로 인한 그룹 별 쿼리 실패 (문제 : [# 33361](https://github.com/elastic/elasticsearch/issues/33361) , [# 34543](https://github.com/elastic/elasticsearch/issues/34543) , [# 36074](https://github.com/elastic/elasticsearch/issues/36074) , [# 37044](https://github.com/elastic/elasticsearch/issues/37044) , [# 40001](https://github.com/elastic/elasticsearch/issues/40001) , [# 40240](https://github.com/elastic/elasticsearch/issues/40240) , [# 41159](https://github.com/elastic/elasticsearch/issues/41159) , [# 42041](https://github.com/elastic/elasticsearch/issues/42041) , [# 46316](https://github.com/elastic/elasticsearch/issues/46316) )

**검색**

-   사용자 정의 유사성 [# 50851의](https://github.com/elastic/elasticsearch/pull/50851) 업그레이드 수정 (문제 : [# 50763](https://github.com/elastic/elasticsearch/issues/50763) )
-   NPE 버그 inner_hits [# 50709](https://github.com/elastic/elasticsearch/pull/50709) 수정 (문제 : [# 50539](https://github.com/elastic/elasticsearch/issues/50539) )
-   부분 결과 [# 49828을](https://github.com/elastic/elasticsearch/pull/49828) 통지 할 때 로컬 목록에 결과 수집 (문제 : [# 49778](https://github.com/elastic/elasticsearch/issues/49778) )
-   인터벌 필터 직렬화 [# 49793](https://github.com/elastic/elasticsearch/pull/49793) 의 버그 수정 (문제 : [# 49519](https://github.com/elastic/elasticsearch/issues/49519) )
-   정렬되지 않은 간격 일치에서 중복을 올바르게 처리합니다. [# 49775](https://github.com/elastic/elasticsearch/pull/49775)
-   script_score 쿼리 [#](https://github.com/elastic/elasticsearch/pull/48425) 48425의 올바른 다시 [쓰기](https://github.com/elastic/elasticsearch/pull/48425) (문제 : [# 48081](https://github.com/elastic/elasticsearch/issues/48081) )
-   SearchAfterBuilder [# 48147](https://github.com/elastic/elasticsearch/pull/48147) 에서 알 수없는 유형에 오류를 발생시키지 마십시오 (문제 : [# 48074](https://github.com/elastic/elasticsearch/issues/48074) )

**보안**

-   항상 신체를 소비합니다 [# 50298](https://github.com/elastic/elasticsearch/pull/50298) 권한 (문제 : [# 50288](https://github.com/elastic/elasticsearch/issues/50288) )

**스냅 샷 / 복원**

-   지나치게 공격적인 요청 중복 제거 [# 51270](https://github.com/elastic/elasticsearch/pull/51270) 수정 (문제 : [# 51253](https://github.com/elastic/elasticsearch/issues/51253) )
-   예외 throw [# 50970에](https://github.com/elastic/elasticsearch/pull/50970) 대한 Guard Repository # [getRepositoryData](https://github.com/elastic/elasticsearch/pull/50970)
-   부분 스냅 샷 생성 중 인덱스 삭제 수정 [# 50234](https://github.com/elastic/elasticsearch/pull/50234) (문제 : [# 50200](https://github.com/elastic/elasticsearch/issues/50200) , [# 50202](https://github.com/elastic/elasticsearch/issues/50202) )
-   Snapshot Finalization [# 50202](https://github.com/elastic/elasticsearch/pull/50202) 중 인덱스 삭제 수정 (문제 : [# 45689](https://github.com/elastic/elasticsearch/issues/45689) , [# 50200](https://github.com/elastic/elasticsearch/issues/50200) )
-   Master-Failover [# 49217](https://github.com/elastic/elasticsearch/pull/49217) 에서 RepoCleanup이 제거되지 않는 문제 수정[](https://github.com/elastic/elasticsearch/pull/49217)
-   FsBlobContainer 리스팅을 동시 수정에 탄력적으로 작성 [# 49142](https://github.com/elastic/elasticsearch/pull/49142) (문제 : [# 37581](https://github.com/elastic/elasticsearch/issues/37581) )
-   실패한 샤드 [# 48556에](https://github.com/elastic/elasticsearch/pull/48556) 대한 SnapshotShardStatus보고 수정 (문제 : [# 48526](https://github.com/elastic/elasticsearch/issues/48526) )
-   정리 동시 저장소 데이터로드 [# 48329](https://github.com/elastic/elasticsearch/pull/48329) (문제 : [# 48122](https://github.com/elastic/elasticsearch/issues/48122) )

**변환**

-   scaled_float [# 51990에](https://github.com/elastic/elasticsearch/pull/51990) 대한 매핑 공제 수정 (문제 : [# 51780](https://github.com/elastic/elasticsearch/issues/51780) )
-   보안이 활성화 된 경우 수정 통계가 이전 상태 정보를 반환 할 수 있음 [# 51732](https://github.com/elastic/elasticsearch/pull/51732) (문제 : [# 51728](https://github.com/elastic/elasticsearch/issues/51728) )
-   누락 된 파이프 라인 [# 50701](https://github.com/elastic/elasticsearch/pull/50701) 에서 시작 / 실패하지 [못함](https://github.com/elastic/elasticsearch/pull/50701) (문제 : [# 50135](https://github.com/elastic/elasticsearch/issues/50135) )
-   롤링 업그레이드 [# 49731](https://github.com/elastic/elasticsearch/pull/49731) 후 발생 가능한 감사 로깅 [누락](https://github.com/elastic/elasticsearch/pull/49731) 문제 (문제 : [# 49730](https://github.com/elastic/elasticsearch/issues/49730) )
-   전역 검사 점 불일치로 인해 검사 점 생성에 실패하지 않음 [# 48423](https://github.com/elastic/elasticsearch/pull/48423) (문제 : [# 48379](https://github.com/elastic/elasticsearch/issues/48379) )

# 업그레이드

**엔진**

-   Lucene 8.4.0으로 업그레이드하십시오. [# 50518](https://github.com/elastic/elasticsearch/pull/50518)

**인프라 / 포장**

-   번들로 제공되는 JDK를 JDK 13.0.2로 업그레이드하십시오. [# 51511](https://github.com/elastic/elasticsearch/pull/51511)

