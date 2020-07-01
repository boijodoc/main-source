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

- 사용자 정의 영역에서 클라이언트와 역할 매핑(RoleMapping) 지원
