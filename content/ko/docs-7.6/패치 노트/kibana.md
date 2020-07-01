 


---
title: "Kibana 패치 노트"
linkTitle: "Kibana"
type: docs
weight: 1
date: 2020-07-01
description: >
  Kibana v7.6 패치 노트
---

# 알려진 문제

-   기본 `dateFormat:tz: browser`설정 을 사용하면 타임 스탬프가 사용자 브라우저의 현지 시간 대신 UTC로 나타납니다. 사용자 브라우저의 현지 시간을 사용하려면 사용자 `dateFormat:tz:`의 시간대로 설정 하십시오. [# 57457](https://github.com/elastic/kibana/issues/57457)
-   이 `server.customResponseHeaders`옵션은 문자열 이외의 유형을 사용하여 헤더를 설정 한 경우 Kibana가 시작되지 않도록합니다. 이 문제를 해결하려면 부울 및 숫자 헤더를 문자열로 변환하십시오. 예를 들어 `my-header: "true"`대신을 사용하십시오 `my-header: true`. [# 66146](https://github.com/elastic/kibana/issues/66146)

# 향상

**APM**

-   APM 인덱스 패턴 [# 54095](https://github.com/elastic/kibana/pull/54095) 업데이트[](https://github.com/elastic/kibana/pull/54095)
-   jvm [# 50830에](https://github.com/elastic/kibana/pull/50830) 서비스 이름 추가[](https://github.com/elastic/kibana/pull/50830)
-   메타 데이터 테이블 [# 48520에](https://github.com/elastic/kibana/pull/48520) 필터 옵션 추가[](https://github.com/elastic/kibana/pull/48520)
-   버킷주기 [# 49638의](https://github.com/elastic/kibana/pull/49638) 시작 및 종료를 표시하도록 오류 발생 그래프 툴팁 업데이트[](https://github.com/elastic/kibana/pull/49638)
-   톱 10 미량 샘플의 페이지 매김 [# 51911](https://github.com/elastic/kibana/pull/51911)
-   trace.id [# 51450](https://github.com/elastic/kibana/pull/51450) 만으로 트레이스에 직접 연결할 수 있습니다.[](https://github.com/elastic/kibana/pull/51450)
-   거래에 [# 53760](https://github.com/elastic/kibana/pull/53760) 이 없으면 거래 페이지에서 처리되지 않은 예외가 발생합니다. `http.request`[](https://github.com/elastic/kibana/pull/53760)
-   `message`메타 데이터 테이블 [# 54017에](https://github.com/elastic/kibana/pull/54017) 필드를 추가합니다.[](https://github.com/elastic/kibana/pull/54017)
-   거래가 아닌 타임 라인에 오류를 표시합니다 [# 53756](https://github.com/elastic/kibana/pull/53756)
-   다른 서비스에서 온 경우에도 동일한 트랜잭션 이름을 가진 추적이 결합됩니다. [# 54247](https://github.com/elastic/kibana/pull/54247)
-   kuery 바 제안에 indexPatternsService 사용 [# 49169](https://github.com/elastic/kibana/pull/49169)
-   서버 경로를 NP [# 49455](https://github.com/elastic/kibana/pull/49455) 로 마이그레이션[](https://github.com/elastic/kibana/pull/49455)
-   `service.version`거래보기에 필터를 추가합니다 [# 52748](https://github.com/elastic/kibana/pull/52748)
-   시계열 차트에 버전 주석 추가 [# 52640](https://github.com/elastic/kibana/pull/52640)
-   오류 스택 추적 개선 [# 49254](https://github.com/elastic/kibana/pull/49254)
-   사용자 에이전트 별 성능 비교 차트 (브라우저) [# 49582](https://github.com/elastic/kibana/pull/49582)
-   UI 인덱스 런타임 구성 추가 [# 48079](https://github.com/elastic/kibana/pull/48079)
-   APM 인덱스 패턴 [# 54693](https://github.com/elastic/kibana/pull/54693) 업데이트[](https://github.com/elastic/kibana/pull/54693)
-   UI [# 51767을](https://github.com/elastic/kibana/pull/51767) 통해 인덱스를 업데이트 할 때 캐시를 지웁니다.

**캔버스**

-   [퍼갈](https://github.com/elastic/kibana/pull/53971) 수있는지도를 활성화합니다 [# 53971](https://github.com/elastic/kibana/pull/53971)
-   사이드 바 [# 49419](https://github.com/elastic/kibana/pull/49419) 에서 압축 된 양식을 사용합니다 [.](https://github.com/elastic/kibana/pull/49419)

**계기반**

-   빈 화면을 다시 디자인합니다 [# 53681](https://github.com/elastic/kibana/pull/53681)
-   dasbhoard 빈 화면에서 시각화를 추가합니다 [# 52670](https://github.com/elastic/kibana/pull/52670)
-   읽기 전용 모드에서 빈 화면을 다시 디자인합니다 [# 54073](https://github.com/elastic/kibana/pull/54073)
-   대시 보드 [# 53110에](https://github.com/elastic/kibana/pull/53110) 렌즈 추가[](https://github.com/elastic/kibana/pull/53110)
-   대시 보드에서 "새로 만들기"UI 개선 [# 49189](https://github.com/elastic/kibana/pull/49189)

**발견**

-   리 팩터, 렌즈 `ChangeIndexPattern`부품 [# 51973에 대한](https://github.com/elastic/kibana/pull/51973) 인덱스 패턴 선택기 발견[](https://github.com/elastic/kibana/pull/51973)
-   KQL [# 47070에](https://github.com/elastic/kibana/pull/47070) 중첩 필드 지원 추가[](https://github.com/elastic/kibana/pull/47070)
-   기존 필터 유형에서 중첩 필드 지원 [# 49537](https://github.com/elastic/kibana/pull/49537)
-   필터 배지 [# 52751](https://github.com/elastic/kibana/pull/52751) 에서 클릭 + 시프트로 필터 비활성화 / 활성화[](https://github.com/elastic/kibana/pull/52751)
-   스크립팅 된 필드를 테스트 할 때 필터링 가능성 (# 35379) [# 44220](https://github.com/elastic/kibana/pull/44220)
-   문서 테이블에 중첩 된 필드에 레이블 및 아이콘을 추가합니다. [# 54199](https://github.com/elastic/kibana/pull/54199)

**그래프**

-   그래프 요청시 오류 메시지 개선 [# 54230](https://github.com/elastic/kibana/pull/54230)
-   샘플 데이터 [# 54558](https://github.com/elastic/kibana/pull/54558) 추가

**렌즈**

-   숫자 용어 aggs 허용 [# 50177](https://github.com/elastic/kibana/pull/50177)
-   스크립팅 된 필드 및 기본 색인 패턴 [# 53948에](https://github.com/elastic/kibana/pull/53948) 대한 지원 추가[](https://github.com/elastic/kibana/pull/53948)
-   kibana 앱과 함께 렌즈로드 [# 50164](https://github.com/elastic/kibana/pull/50164)
-   문서가 변경되지 않을 때까지 시각화 저장을 비활성화합니다. [# 52982](https://github.com/elastic/kibana/pull/52982)
-   클리어 레이어 기능 추가 [# 53627](https://github.com/elastic/kibana/pull/53627)
-   존재 API [# 54064](https://github.com/elastic/kibana/pull/54064) 에 스크립팅 된 필드 및 별명에 대한 지원을 추가합니다.

**로그**

-   로그 속도 설정 색인 유효성 검사 [# 50008](https://github.com/elastic/kibana/pull/50008)
-   분류 탭에 카테고리 테이블을 추가합니다. [# 53004](https://github.com/elastic/kibana/pull/53004)
-   설치가 보류중인 동안 ML 작업 설정 양식을 비활성화합니다. [# 54705](https://github.com/elastic/kibana/pull/54705)

**기계 학습**

-   이상 감지 작업 마법사 버튼 스타일, 페이지 패널 및 제목 업데이트 [# 53340](https://github.com/elastic/kibana/pull/53340)
-   데이터 인식기 마법사에서 그룹 처리 향상 [# 49310](https://github.com/elastic/kibana/pull/49310)
-   File Data Visualizer [# 50147](https://github.com/elastic/kibana/pull/50147) 에서 가져 오기에 필요한 권한이 없음을 나타냅니다.[](https://github.com/elastic/kibana/pull/50147)
-   데이터 프레임 분석을위한 통계 표시 줄 [# 49464](https://github.com/elastic/kibana/pull/49464)
-   데이터 프레임 분석에 작업 메시지 탭을 추가합니다 [# 50468](https://github.com/elastic/kibana/pull/50468)
-   Single Metric Viewer [# 51008의](https://github.com/elastic/kibana/pull/51008) 반응 시간 범위 선택[](https://github.com/elastic/kibana/pull/51008)
-   작업 마법사에 사용자 정의 URL 및 달력을 추가합니다 [# 51281](https://github.com/elastic/kibana/pull/51281)
-   모델 플롯을 활성화 할 때 카디널리티 검사를 수행합니다. [# 51915](https://github.com/elastic/kibana/pull/51915)
-   최신 작업 메시지를 [가져오고 시간별로](https://github.com/elastic/kibana/pull/52388) 정렬 할 수 있습니다. [# 52388](https://github.com/elastic/kibana/pull/52388)
-   전체 너비로 확장 될 때 시간 범위 브러시 지속 [# 54020](https://github.com/elastic/kibana/pull/54020)
-   Single Metric Viewer [# 53879](https://github.com/elastic/kibana/pull/53879) 에서 파티션 검색을 지원합니다[](https://github.com/elastic/kibana/pull/53879)
-   RUM Javascript 및 NodeJS [# 53792에](https://github.com/elastic/kibana/pull/53792) 대한 APM 모듈 구성[](https://github.com/elastic/kibana/pull/53792)
-   다중 메트릭 작업 마법사를위한 모델 메모리 제한 계산기 기능 향상 [# 54573](https://github.com/elastic/kibana/pull/54573)
-   데이터 시각화 [도우미](https://github.com/elastic/kibana/pull/54358) 재 설계 [# 54358](https://github.com/elastic/kibana/pull/54358)
-   추가 타이밍 및 모델 크기 통계 포맷 [# 55062](https://github.com/elastic/kibana/pull/55062)
-   개요 및 분석 페이지에 ML 노드 경고를 추가합니다 [# 50766](https://github.com/elastic/kibana/pull/50766)
-   고급 마법사에서 lat_long 감지기 기능을 사용합니다. [# 50787](https://github.com/elastic/kibana/pull/50787)
-   분류 마법사 [# 53009](https://github.com/elastic/kibana/pull/53009)
-   회귀 결과보기 [# 49667](https://github.com/elastic/kibana/pull/49667)
-   model_memory_limit [# 50714](https://github.com/elastic/kibana/pull/50714) 자동 입력[](https://github.com/elastic/kibana/pull/50714)
-   [재실행](https://github.com/elastic/kibana/pull/50991) 은 검색 창 쿼리에 대한 엔드 포인트를 평가합니다. [# 50991](https://github.com/elastic/kibana/pull/50991)
-   검색 창 [# 51235](https://github.com/elastic/kibana/pull/51235) 추가[](https://github.com/elastic/kibana/pull/51235)
-   UI [# 51619](https://github.com/elastic/kibana/pull/51619) 를 통해 분류 작업을 만듭니다.[](https://github.com/elastic/kibana/pull/51619)
-   작업 작성에 설명 필드를 추가하고 작업 목록에 표시 [# 52217](https://github.com/elastic/kibana/pull/52217)
-   분류 작업 결과보기 [# 52584를](https://github.com/elastic/kibana/pull/52584) 만듭니다.[](https://github.com/elastic/kibana/pull/52584)
-   추가합니다 _제외_ 입력 필드를 형성하는 단계 [# 53856을](https://github.com/elastic/kibana/pull/53856)
-   문서에 링크를 추가합니다 [# 54189](https://github.com/elastic/kibana/pull/54189)
-   필드 대문자 api를 사용하여 열 유형 [# 54543](https://github.com/elastic/kibana/pull/54543) 설정[](https://github.com/elastic/kibana/pull/54543)
-   개요 페이지에서 텍스트를 자릅니다. _최신 시간 소인_ 열 [# 50004](https://github.com/elastic/kibana/pull/50004)
-   색상 범위 범례 구성 요소 [# 52794](https://github.com/elastic/kibana/pull/52794)

**조치**

-   Webhook 작업으로 임계 값 경고를 만들 때 지원 체계 필드 [# 53757](https://github.com/elastic/kibana/pull/53757)
-   색인 템플릿 마법사에 매핑 편집기 추가 [# 47562](https://github.com/elastic/kibana/pull/47562)
-   NP [# 48795에 대한 검색 프로파일 러](https://github.com/elastic/kibana/pull/48795)
-   새 플랫폼으로 업그레이드 도우미 지원 [# 50163](https://github.com/elastic/kibana/pull/50163)
-   새로운 플랫폼 [# 51886에 대한](https://github.com/elastic/kibana/pull/51886) 라이센스 관리[](https://github.com/elastic/kibana/pull/51886)
-   새 플랫폼 (NP) 마이그레이션 [# 50908](https://github.com/elastic/kibana/pull/50908)
-   더 나은 SQL 지원 콘솔 [# 51446](https://github.com/elastic/kibana/pull/51446)
-   사용자가 UI [# 53047](https://github.com/elastic/kibana/pull/53047) 에서 리포지토리를 [정리할 수 있습니다](https://github.com/elastic/kibana/pull/53047)
-   사용 데이터에 대한 고급 설정 텍스트를 업데이트합니다. [# 52657](https://github.com/elastic/kibana/pull/52657)

**지도**

-   그리드 사각형을 [지오그리드](https://github.com/elastic/kibana/pull/50169) 소스의 기본 상징으로 만듭니다. [# 50169](https://github.com/elastic/kibana/pull/50169)
-   편집기가 [팝 오버를](https://github.com/elastic/kibana/pull/51487) 열 때 입력에 초점을 [맞 춥니](https://github.com/elastic/kibana/pull/51487) 다 [# 51487](https://github.com/elastic/kibana/pull/51487)
-   스타일 메타 데이터를 사용하여 [기호](https://github.com/elastic/kibana/pull/51713) 밴드를 계산합니다. [# 51713](https://github.com/elastic/kibana/pull/51713)
-   더 나은 스타일 기본값 [# 52420](https://github.com/elastic/kibana/pull/52420)
-   벡터 스타일 [ui](https://github.com/elastic/kibana/pull/53946) 재 설계 [# 53946](https://github.com/elastic/kibana/pull/53946)
-   EMS베이스 맵 선택 [# 53631](https://github.com/elastic/kibana/pull/53631) 편집 가능[](https://github.com/elastic/kibana/pull/53631)
-   텍스트 후광 색상 및 너비 스타일 속성 추가 [# 53827](https://github.com/elastic/kibana/pull/53827)
-   샘플 데이터 맵에 레이블을 추가합니다 [# 54671](https://github.com/elastic/kibana/pull/54671)
-   범주 스타일 추가 [# 54408](https://github.com/elastic/kibana/pull/54408)
-   기본 kibana.yml 설정으로지도 시각화 유형을 숨 깁니다. [# 49103](https://github.com/elastic/kibana/pull/49103)
-   포함 가능한 패널에서 헤더 패널을 숨 깁니다. [# 50728](https://github.com/elastic/kibana/pull/50728)

**측정 항목**

-   데이터 세트의 기간을 기반으로 간격을 계산합니다. [# 50194](https://github.com/elastic/kibana/pull/50194)
-   스냅 샷 및 노드 세부 사항에 대한 graphql 쿼리를 hapijs로 포트 [# 50730](https://github.com/elastic/kibana/pull/50730)
-   계정 및 지역별로 스냅 샷보기를 필터링하는 기능을 추가합니다 [# 53307](https://github.com/elastic/kibana/pull/53307)
-   지역 및 계정으로 인벤토리 메타 데이터 api를 추가합니다 [# 52660](https://github.com/elastic/kibana/pull/52660)
-   graphql 유형을 제거합니다 [# 54176](https://github.com/elastic/kibana/pull/54176)
-   인벤토리 모델에 AWS 지표 세트 추가 [# 49983](https://github.com/elastic/kibana/pull/49983)

**모니터링**

-   더 효율적으로 샤드 데이터를 [가져옵니다. # 54028](https://github.com/elastic/kibana/pull/54028)
-   바이트 [# 54275로](https://github.com/elastic/kibana/pull/54275) APM 서버 메모리를 표시합니다

**운영**

- 로그 회전 [# 49750에](https://github.com/elastic/kibana/pull/49750) 대한 지원 추가

**모니터링**

- 접근성을위한 h1 요소 [# 52276](https://github.com/elastic/kibana/pull/52276)

**플랫폼**

-   경로가 일부 페이로드 구성 값을 정의 할 수 있도록합니다. [# 50783](https://github.com/elastic/kibana/pull/50783)
-   IndexPatterns를 NP [# 51199](https://github.com/elastic/kibana/pull/51199) 로 이동[](https://github.com/elastic/kibana/pull/51199)
-   구성 검증을 새로운 플랫폼 [# 51880으로 이동](https://github.com/elastic/kibana/pull/51880)
-   "브라우저 클라이언트가 오래되었습니다"오류 메시지 개선 [# 50296](https://github.com/elastic/kibana/pull/50296)

**보고**

-   기본보고 색인을 TS [# 49129](https://github.com/elastic/kibana/pull/49129) 로 변환[](https://github.com/elastic/kibana/pull/49129)
-   Hapi [# 49250에](https://github.com/elastic/kibana/pull/49250) 대한 모든 유형 및 참조를 제거합니다[](https://github.com/elastic/kibana/pull/49250)
-   일부 런타임 유효성 검사를 업데이트합니다 [# 53975](https://github.com/elastic/kibana/pull/53975)

**보안**

-   역할 매핑 UI [# 53620](https://github.com/elastic/kibana/pull/53620)
-   로그인 페이지 [# 51557에](https://github.com/elastic/kibana/pull/51557) 메시지를 추가합니다[](https://github.com/elastic/kibana/pull/51557)
-   Node.js를 버전 10.18.0으로 업데이트합니다 [# 52865](https://github.com/elastic/kibana/pull/52865)
-   세션 유휴 시간 초과 향상, 세션 수명 추가 [# 49855](https://github.com/elastic/kibana/pull/49855)
-   PKCS # 12 (P12) 키 저장소 [# 53810](https://github.com/elastic/kibana/pull/53810) 에서 인증서 지원 추가

**심**

-   새로운 개요 페이지 [# 54783](https://github.com/elastic/kibana/pull/54783)
-   DNS 히스토그램 [# 50409](https://github.com/elastic/kibana/pull/50409) 추가[](https://github.com/elastic/kibana/pull/50409)
-   경고 테이블 [# 51959](https://github.com/elastic/kibana/pull/51959) 추가[](https://github.com/elastic/kibana/pull/51959)
-   히스토그램 향상 [# 54544](https://github.com/elastic/kibana/pull/54544)
-   Dns 히스토그램 향상 [# 54902](https://github.com/elastic/kibana/pull/54902)
-   search_after 및 대량 인덱스 [# 50129에](https://github.com/elastic/kibana/pull/50129) 대한 테스트[](https://github.com/elastic/kibana/pull/50129)
-   규칙에 ecs 위협 속성 추가 [# 51782](https://github.com/elastic/kibana/pull/51782)
-   신호 상태 열림 REST API [# 52356을 설정합니다.](https://github.com/elastic/kibana/pull/52356)
-   검색 신호 색인 [# 52661](https://github.com/elastic/kibana/pull/52661)
-   규칙에 created_at 및 updated_at 타임 스탬프를 추가합니다 [# 53137](https://github.com/elastic/kibana/pull/53137)
-   규칙 상태 모니터링 [# 54452](https://github.com/elastic/kibana/pull/54452)
-   KQL REST API [# 49451에](https://github.com/elastic/kibana/pull/49451) 필터링 기능 추가[](https://github.com/elastic/kibana/pull/49451)
-   REST API 추가 [# 50514](https://github.com/elastic/kibana/pull/50514)
-   REST API 개선 및 UI / UX 피드백 [# 50797의](https://github.com/elastic/kibana/pull/50797) 변경 사항[](https://github.com/elastic/kibana/pull/50797)
-   위험 점수, 출력 지수, 규칙 복사 등의 추가 [# 51190](https://github.com/elastic/kibana/pull/51190)
-   인덱스 명명 규칙을 통해 공간 당 신호 데이터 인덱스를 추가합니다. [# 52237](https://github.com/elastic/kibana/pull/52237)
-   권한 API 엔드 포인트 [# 52707](https://github.com/elastic/kibana/pull/52707) 추가[](https://github.com/elastic/kibana/pull/52707)
-   태그 서비스를 추가하고 alert_id 조회를 최적화합니다 [# 52838](https://github.com/elastic/kibana/pull/52838)
-   사전 패키징 규칙 기능 추가 [# 53062](https://github.com/elastic/kibana/pull/53062)
-   규칙에 timeline_id 문자열을 추가합니다 [# 53343](https://github.com/elastic/kibana/pull/53343)
-   생성, 업데이트 및 삭제를위한 대량 REST API [# 53543](https://github.com/elastic/kibana/pull/53543)
-   REST 엔드 포인트 가져 오기 / 내보내기 [# 54332](https://github.com/elastic/kibana/pull/54332)
-   시간 간격 감지 및 로깅 [# 54547](https://github.com/elastic/kibana/pull/54547)
-   규칙 표 [# 50839](https://github.com/elastic/kibana/pull/50839) 추가[](https://github.com/elastic/kibana/pull/50839)
-   StatefulEventsViewer [# 52044에](https://github.com/elastic/kibana/pull/52044) Signals Table 및 추가 구성 옵션 추가[](https://github.com/elastic/kibana/pull/52044)
-   네트워크 맵에 apm- *에 대한 지원을 추가합니다 [# 54876](https://github.com/elastic/kibana/pull/54876)
-   HTTP 요청 테이블 [# 49955](https://github.com/elastic/kibana/pull/49955)
-   인증 히스토그램 추가 [# 48260](https://github.com/elastic/kibana/pull/48260)
-   호스트 및 네트워크 이상 히스토그램 추가 [# 50295](https://github.com/elastic/kibana/pull/50295)
-   탐지 엔진 자리 표시 자 [# 50220](https://github.com/elastic/kibana/pull/50220)
-   타임 라인 [# 49813에 SavedQuery](https://github.com/elastic/kibana/pull/49813) 추가[](https://github.com/elastic/kibana/pull/49813)
-   생성 규칙 [# 51376](https://github.com/elastic/kibana/pull/51376) 추가[](https://github.com/elastic/kibana/pull/51376)
-   규칙 생성시 편집 추가 [# 51670](https://github.com/elastic/kibana/pull/51670)
-   MITER ATT & CK [# 52398](https://github.com/elastic/kibana/pull/52398) 추가[](https://github.com/elastic/kibana/pull/52398)
-   규칙에 대한 세부 정보 및 편집보기 [# 53252](https://github.com/elastic/kibana/pull/53252)
-   권한 II [# 54292](https://github.com/elastic/kibana/pull/54292)
-   규칙 세부 사항에 상태를 추가합니다. [# 54812](https://github.com/elastic/kibana/pull/54812)
-   신호에서 타임 라인 [# 54769까지](https://github.com/elastic/kibana/pull/54769)
-   탐지는 사전 패키지 규칙을 만듭니다. [# 55403](https://github.com/elastic/kibana/pull/55403)
-   생성 된 암호화 키 [# 56464](https://github.com/elastic/kibana/pull/56464) 에 대한 사용자 의견

**가동 시간**

-   스냅 샷 수 [# 48035](https://github.com/elastic/kibana/pull/48035) 업데이트[](https://github.com/elastic/kibana/pull/48035)
-   가동 시간 서버 라우팅을 새로운 플랫폼 [# 51125로 마이그레이션](https://github.com/elastic/kibana/pull/51125)
-   태그 드롭 다운을 개요 필터 그룹 [# 50837에](https://github.com/elastic/kibana/pull/50837) 추가합니다[](https://github.com/elastic/kibana/pull/50837)
-   새 모니터 목록 확장 된 행 [# 46567](https://github.com/elastic/kibana/pull/46567)
-   포함 할 수있는 맵에서 확대 / 축소, 도구 설명 숨기기, 위젯 / 오버레이를 비활성화하는 옵션을 추가합니다. [# 50663](https://github.com/elastic/kibana/pull/50663)
-   새로운 세부 정보 패널 및 위치지도 [# 50518](https://github.com/elastic/kibana/pull/50518)
-   외부 링크 [# 53098을](https://github.com/elastic/kibana/pull/53098) 나열합니다.[](https://github.com/elastic/kibana/pull/53098)
-   모니터 세부 사항 페이지 왼쪽 제목 [# 53529](https://github.com/elastic/kibana/pull/53529)
-   경고 [# 54040에](https://github.com/elastic/kibana/pull/54040) 대한 SSL 인증서 색상 버전 모니터링

# 버그 수정

**APM**

-   APM 마이그레이션 스크립트 v1 지원 업그레이드 [# 52824](https://github.com/elastic/kibana/pull/52824)
-   스타일이 지정된 구성 요소에 누락 된 세미콜론 추가 [# 51436](https://github.com/elastic/kibana/pull/51436)
-   10 개 이상의 항목이 표시되도록 ACM에 대한 빠른 수정 [# 52262](https://github.com/elastic/kibana/pull/52262)
-   차트 [# 50904](https://github.com/elastic/kibana/pull/50904) 에 사용 가능한 너비를 기준으로 눈금을 설정하지 않습니다.[](https://github.com/elastic/kibana/pull/50904)
-   분당 오류가 올바르게보고되는지 확인하십시오. [# 54751](https://github.com/elastic/kibana/pull/54751)
-   차트를 렌더링 할 때 파이어 폭스 SVG NaN 오류 수정 [# 56578](https://github.com/elastic/kibana/pull/56578)
-   초기 오류 정렬 필드 [# 56577](https://github.com/elastic/kibana/pull/56577) 수정[](https://github.com/elastic/kibana/pull/56577)
-   레이블 및 사용자 메타 데이터 섹션에 대한 빈 메시지 "데이터가 없습니다" [# 49846](https://github.com/elastic/kibana/pull/49846)

**캔버스**

-   axisConfig 위치 인수 UI [# 50717](https://github.com/elastic/kibana/pull/50717) 수정[](https://github.com/elastic/kibana/pull/50717)
-   수정 # 45896 [# 50229](https://github.com/elastic/kibana/pull/50229)
-   전체 화면 필터로 버그 수정 [# 54792](https://github.com/elastic/kibana/pull/54792)
-   포스트 URL 링크 복사 [# 54831](https://github.com/elastic/kibana/pull/54831) 수정[](https://github.com/elastic/kibana/pull/54831)
-   색상 수정 및 접근성 전환 [# 54661](https://github.com/elastic/kibana/pull/54661)

**계기반**

-   더블 핸들러 [# 53707를](https://github.com/elastic/kibana/pull/53707) 제거합니다[](https://github.com/elastic/kibana/pull/53707)
-   URL 매개 변수를 해독하므로 두 번 인코딩되지 않습니다. [# 54738](https://github.com/elastic/kibana/pull/54738)
-   EUI 색상에 맞게 배경색을 변경합니다. [# 54060](https://github.com/elastic/kibana/pull/54060)
-   대시 보드를위한 모바일 _편집_ 버튼 숨기기 _수정_ [# 50639](https://github.com/elastic/kibana/pull/50639)

**발견**

-   히스토그램 최소 간격 수정 [# 53979](https://github.com/elastic/kibana/pull/53979)
-   kql 오류 메시지 처리를 개선하고 두 번 페치하지 않도록 [# 54239](https://github.com/elastic/kibana/pull/54239)
-   이중 반입 오류 [# 54701](https://github.com/elastic/kibana/pull/54701) 수정[](https://github.com/elastic/kibana/pull/54701)
-   저장된 검색을 위해 페이지 매김 컨트롤을 가로로 스크롤하지 않아야하는 문제 수정 [# 50764](https://github.com/elastic/kibana/pull/50764)
-   인덱스 패턴의 필드를 새로 고칠 때 예외를 throw하지 마십시오 [# 55836](https://github.com/elastic/kibana/pull/55836)
-   앨리어스가 [무시 된](https://github.com/elastic/kibana/pull/50743) 필터의 필터 필 레이블 수정 [# 50743](https://github.com/elastic/kibana/pull/50743)
-   스크립트 된 필드 미리보기 필드 목록을 소스 필드로 [필터링 # 53826](https://github.com/elastic/kibana/pull/53826)
-   운영자가 팝 오버 [# 50030을](https://github.com/elastic/kibana/pull/50030) 초과하는 문제 수정

**그래프**

- 탐색 가능한 필드 만 표시 [# 54101](https://github.com/elastic/kibana/pull/54101)

**렌즈**

-   자동 날짜 [# 52931](https://github.com/elastic/kibana/pull/52931) 과 동일한 논리를 사용하도록 병합 테이블을 수정합니다 [.](https://github.com/elastic/kibana/pull/52931)
-   카운트 작업을 선택한 경우 레코드 필드를 선택합니다. [# 53911](https://github.com/elastic/kibana/pull/53911)
-   7.3 이전 색인 패턴에 대한 키워드 필드를 표시합니다. [# 52410](https://github.com/elastic/kibana/pull/52410)
-   정렬에 사용되는 Y 축을 제거 할 때 정렬 충돌을 수정합니다. [# 52694](https://github.com/elastic/kibana/pull/52694)
-   시간 필드없이 색인 패턴을 사용할 때 필드를 표시합니다. [# 54804](https://github.com/elastic/kibana/pull/54804)
-   렌즈 필터의 버그 수정 [# 56441](https://github.com/elastic/kibana/pull/56441)

**로그**

-   로그 및 메트릭에 누락 된 헤더 추가 [# 52405](https://github.com/elastic/kibana/pull/52405)
-   기능에 올바른 아이콘 및 레이블을 사용 하여 계속 [# 55292](https://github.com/elastic/kibana/pull/55292)
-   ... 기계와 로그 / ML 통합 결과에 대한 액세스를 허용 [# 55884](https://github.com/elastic/kibana/pull/55884)
-   검색 마커의 규모를 수정 [# 55731](https://github.com/elastic/kibana/pull/55731)

**기계 학습**

-   Lucene 쿼리 언어에 대한 이스케이프 특수 문자 수정 [# 50494](https://github.com/elastic/kibana/pull/50494)
-   새로 고칠 때 규칙 편집기 플라이 아웃을 열어 둡니다. [# 53458](https://github.com/elastic/kibana/pull/53458)
-   Data Visualizer 페이지에서 배열 필드의 카운터 및 백분율을 수정합니다. [# 55209](https://github.com/elastic/kibana/pull/55209)
-   마우스 휴가에 툴팁의 지속성을 수정합니다 [# 55694](https://github.com/elastic/kibana/pull/55694)
-   Anomaly Explorer 스 [lane](https://github.com/elastic/kibana/pull/55827) 레인 툴팁 문제 [# 55827](https://github.com/elastic/kibana/pull/55827) 수정[](https://github.com/elastic/kibana/pull/55827)
-   주석 영역 툴팁 오프셋 [# 55955](https://github.com/elastic/kibana/pull/55955) 수정[](https://github.com/elastic/kibana/pull/55955)
-   정보 내용 탐지기 필드 선택 수정 [# 51914](https://github.com/elastic/kibana/pull/51914)
-   작업 검증 로딩 스피너 [# 54450](https://github.com/elastic/kibana/pull/54450)
-   데이터 피드 집계를 사용하여 작업 마법사를 개선합니다. [# 55180](https://github.com/elastic/kibana/pull/55180)
-   작업 메시지 검색에서 누락 된 job_type을 수정합니다. [# 55330](https://github.com/elastic/kibana/pull/55330)
-   불충분 한 인덱스 패턴 권한에 대한 모듈 설정 오류 수정 [# 55989](https://github.com/elastic/kibana/pull/55989)
-   비어있는 경우 고급 편집기를 확인할 수 있습니다. [# 52831](https://github.com/elastic/kibana/pull/52831)
-   고급 편집기가 모델 메모리 장치를 올바르게 검증하도록합니다 [# 54011](https://github.com/elastic/kibana/pull/54011)
-   결과 필드 열을 선택 취소했다가 다시 선택할 수 있도록합니다. [# 54766](https://github.com/elastic/kibana/pull/54766)
-   탭이 포함 된 경우에만 탭리스트 렌더링 [# 54838](https://github.com/elastic/kibana/pull/54838)
-   텍스트 필드 처리 향상 [# 55002](https://github.com/elastic/kibana/pull/55002)
-   결과 테이블 [# 54826](https://github.com/elastic/kibana/pull/54826) 에서 예측 데이터가없는 문서를 [필터링합니다.](https://github.com/elastic/kibana/pull/54826)
-   IE의 개요 페이지 사이드 바에서 줄 바꿈 수정 [# 50668](https://github.com/elastic/kibana/pull/50668)
-   lat_long 예외 테이블 링크 메뉴 및 값 형식 수정 [# 50916](https://github.com/elastic/kibana/pull/50916)
-   KQL 저장된 검색으로 Data Visualizer의로드를 수정합니다. [# 51882](https://github.com/elastic/kibana/pull/51882)
-   작업 팁 문서 작성 페이지의 URL 수정 [# 53576](https://github.com/elastic/kibana/pull/53576)
-   모형 플롯이 활성화 된 경우 차트 툴팁에 실제 이상 표시 [# 54364](https://github.com/elastic/kibana/pull/54364)
-   Data Visualizer 작업 링크 작성에 대한 권한 점검 수정 [# 55431](https://github.com/elastic/kibana/pull/55431)
-   빈 테이블 헤더 셀 및 중복 ID 접근성 문제 해결 [# 54917](https://github.com/elastic/kibana/pull/54917)
-   테이블 행의 구조적 마크 업에 대한 접근성 수정 [# 55075](https://github.com/elastic/kibana/pull/55075)

**조치**

-   Kibana는 ILM 정책 단계 [# 53719](https://github.com/elastic/kibana/pull/53719) 에서 min_age 설정을 0ms로 허용해야합니다.[](https://github.com/elastic/kibana/pull/53719)
-   URI [# 56051](https://github.com/elastic/kibana/pull/56051) 에서 인덱스 필터를 구문 분석 할 때 try / catch를 추가합니다.[](https://github.com/elastic/kibana/pull/56051)
-   ThresholdWatch 함수를 serialize하기 위해 termOrder 및 hasTermsAgg 속성을 [전달합니다.](https://github.com/elastic/kibana/pull/54391)
-   스냅 샷 이름에 대문자 날짜 형식에 대한 지원 추가 [# 53751](https://github.com/elastic/kibana/pull/53751)
-   [Kibana](https://github.com/elastic/kibana/pull/55228) UI에서 인덱스 수명주기 정책에 잘못된 단위가 [표시됨 # 55228](https://github.com/elastic/kibana/pull/55228)
-   테마 및 모드 가져 오기 [# 50473](https://github.com/elastic/kibana/pull/50473)
-   프록시 대체 [# 50185](https://github.com/elastic/kibana/pull/50185)
-   원격 [# 52814의](https://github.com/elastic/kibana/pull/52814) 로드 수정[](https://github.com/elastic/kibana/pull/52814)
-   범위 쿼리 [# 53841](https://github.com/elastic/kibana/pull/53841) 에서 time_zone의 제안 된 값 수정[](https://github.com/elastic/kibana/pull/53841)
-   큰 따옴표 특수 사례 [# 54474 처리](https://github.com/elastic/kibana/pull/54474)
-   잘못된 프로필 데이터 및 업데이트 탭 동작 처리 수정 [# 55806](https://github.com/elastic/kibana/pull/55806)
-   튜토리얼 소개에서 아이콘 경로 수정 [# 49684](https://github.com/elastic/kibana/pull/49684)
-   매핑 유형을 지원하도록 색인 템플릿 편집기 수정 [# 55804](https://github.com/elastic/kibana/pull/55804)

**지도**

-   맵 원격 측정이 작업 관리자 논리를 [채우고](https://github.com/elastic/kibana/pull/52834) 제거하지 못하도록 회귀 문제 수정 [# 52834](https://github.com/elastic/kibana/pull/52834)
-   범주 팔레트 [# 54918](https://github.com/elastic/kibana/pull/54918)
-   빈 필터 설정 변경에 대한 데이터를 다시 가져 오지 마십시오 [# 49382](https://github.com/elastic/kibana/pull/49382)
-   툴팁 필드 선택을위한 다중 필드 제거 수정 [# 49816](https://github.com/elastic/kibana/pull/49816)
-   셰이프 [# 50747로](https://github.com/elastic/kibana/pull/50747) 필터링 할 때 사용자가 URL을 넘치지 않도록 방지[](https://github.com/elastic/kibana/pull/50747)
-   벡터 레이어에 조인이있을 때만 가시성 검사 제공 [# 51388](https://github.com/elastic/kibana/pull/51388)
-   최고 조회수에 대한 too_many_buckets_exception 수정 [#](https://github.com/elastic/kibana/pull/51497) 51497[](https://github.com/elastic/kibana/pull/51497)
-   범례 [# 52335](https://github.com/elastic/kibana/pull/52335) 에서 레이어 피처 유형에 적용되는 스타일 만 표시[](https://github.com/elastic/kibana/pull/52335)
-   CCS [# 52793에](https://github.com/elastic/kibana/pull/52793) 대한 툴팁 수정[](https://github.com/elastic/kibana/pull/52793)
-   getFieldFormatter를 DynamicTextProperty [# 53937에 전달합니다.](https://github.com/elastic/kibana/pull/53937)
-   범위 필터를 확장하여 범위 필터 확장 [# 54276](https://github.com/elastic/kibana/pull/54276)
-   반응 요소 [# 55372](https://github.com/elastic/kibana/pull/55372) 에서 누락 된 키에 대한 경고 수정[](https://github.com/elastic/kibana/pull/55372)
-   결합 메트릭 필드 선택 버그 수정 [# 56044](https://github.com/elastic/kibana/pull/56044)
-   RTL 언어 용 mapbox-gl-rtl-text 라이브러리 추가 [# 54842](https://github.com/elastic/kibana/pull/54842)
-   쿼리 개체가 채워지도록합니다. [# 49917](https://github.com/elastic/kibana/pull/49917)
-   스프라이트 시트가로드 될 때까지 벡터 타일 레이어 동기화 지연 [# 48955](https://github.com/elastic/kibana/pull/48955)
-   저작자 표시 [# 52309](https://github.com/elastic/kibana/pull/52309)
-   레이어가 표시 될 때만 범례 표시 [# 53781](https://github.com/elastic/kibana/pull/53781)
-   범례에서 사용자 지정 색 램프를 보여줍니다 [# 53780](https://github.com/elastic/kibana/pull/53780)
-   파일 대화 상자에서 파일 유형 검사를 시행합니다 [# 55063](https://github.com/elastic/kibana/pull/55063)

**측정 항목**

-   지표 [# 55893을](https://github.com/elastic/kibana/pull/55893) 삭제할 때 지표 탐색기 예외를 수정합니다.[](https://github.com/elastic/kibana/pull/55893)
-   Metrics Explorer [# 55917](https://github.com/elastic/kibana/pull/55917) 에서 제목 잘림 수정[](https://github.com/elastic/kibana/pull/55917)
-   관련 shouldAllowEdit 기능을 SettingsPage [# 49781에 전달](https://github.com/elastic/kibana/pull/49781)
-   동일한 이름의 중복 저장된보기를 허용하지 마십시오 [# 52040](https://github.com/elastic/kibana/pull/52040)
-   필드 [# 54510에](https://github.com/elastic/kibana/pull/54510) 아리아 레이블을 추가합니다

**모니터링**

-   다중 클러스터 환경에서 Logstash 파이프 라인 페이지를 수정합니다 [# 50166](https://github.com/elastic/kibana/pull/50166)
-   설정 모드 [# 50421에](https://github.com/elastic/kibana/pull/50421) 필요한 권한을 향상시킵니다.[](https://github.com/elastic/kibana/pull/50421)
-   비정형 로그에 대한 오류 상태를 추가합니다. [# 53299](https://github.com/elastic/kibana/pull/53299)
-   CCS 환경에서 설정 모드 작동 보장 [# 54361](https://github.com/elastic/kibana/pull/54361)
-   이 인증 설정은 데이터를 전송하기위한 것입니다. [# 48437](https://github.com/elastic/kibana/pull/48437)

**운영**

-   누락 된 도커 설정 추가 [# 56411](https://github.com/elastic/kibana/pull/56411)
-   xpack.task_manager.index가 .tasks [# 52002](https://github.com/elastic/kibana/pull/52002) 로 설정되지 않도록합니다.

**플랫폼**

-   하드 페이지 새로 고침없이 변경된 필드 형식을 표시합니다. [# 52874](https://github.com/elastic/kibana/pull/52874)
-   Kibana 7.0.0 URL 필드 포맷터가 상대 하이퍼 링크를 올바르게 렌더링하지 않음 [# 53265](https://github.com/elastic/kibana/pull/53265)
-   문자열을 숫자로 해석하면 NaN # 27788 [# 50063](https://github.com/elastic/kibana/pull/50063) 에 던져집니다.[](https://github.com/elastic/kibana/pull/50063)
-   폐기 된 KQL 값 제안 요청을 취소합니다. [# 51411](https://github.com/elastic/kibana/pull/51411)
-   마이그레이션 전에 Elasticsearch 버전 확인을 성공적으로 수행합니다. [# 51311](https://github.com/elastic/kibana/pull/51311)

**보고**

-   요청이 중단 된 경우 보고서에 실패하지 마십시오 [# 52344](https://github.com/elastic/kibana/pull/52344)
-   Chrome의 원격 프로토콜 [# 55137](https://github.com/elastic/kibana/pull/55137) 을 사용하여지도 타일이로드되지 않는 문제 수정[](https://github.com/elastic/kibana/pull/55137)
-   검색 쿼리의 docvalue_fields 매개 변수를 대시 보드 패널에서 CSV 다운로드 [# 52833 수정](https://github.com/elastic/kibana/pull/52833)

**보안**

-   SAML ACS [# 51391을](https://github.com/elastic/kibana/pull/51391) 구축 할 때 서버의 basePath를 사용합니다[](https://github.com/elastic/kibana/pull/51391)
-   elasticsearch.ssl.alwaysPresentCertificate 기본값 [# 52242](https://github.com/elastic/kibana/pull/52242) 수정[](https://github.com/elastic/kibana/pull/52242)
-   사용자 이름이 단단한 긴 문자열 인 경우 줄 바꿈을 강제합니다. [# 50807](https://github.com/elastic/kibana/pull/50807)
-   여러 쿠키가 전송 될 때 무한 리디렉션 루프를 수정합니다. [# 50452](https://github.com/elastic/kibana/pull/50452)
-   [# 50946](https://github.com/elastic/kibana/pull/50946) 로그 아웃 할 때 구성된 기본 경로를 [적용합니다](https://github.com/elastic/kibana/pull/50946)

**심**

-   비어 있음 수정 `Source`/ `Destination`포트만 채워 졌을 때 [표시됨 # 50843](https://github.com/elastic/kibana/pull/50843)
-   고정 된 이벤트 툴팁에서 자리 표시자를 제거합니다. [# 52361](https://github.com/elastic/kibana/pull/52361)
-   필터 기능 추가 및 잘못된 값 주위의 기타 버그 수정 [# 50999](https://github.com/elastic/kibana/pull/50999)
-   필터 설정시 빈 쿼리 문자열을 허용하는 버그 수정 [# 51398](https://github.com/elastic/kibana/pull/51398)
-   ECS event.kind에 신호를 추가하고 신호의 상태를 수정합니다 [# 51772](https://github.com/elastic/kibana/pull/51772)

**가동 시간**

-   찾아보기 [# 52008](https://github.com/elastic/kibana/pull/52008) 에서 반응 라우터 [-dom](https://github.com/elastic/kibana/pull/52008) 경고를 제거합니다[](https://github.com/elastic/kibana/pull/52008)
-   [# 54395](https://github.com/elastic/kibana/pull/54395) 에서 고장난 기능 테스트 수정`master`[](https://github.com/elastic/kibana/pull/54395)
-   수직으로 중심에 도넛 형 차트 로더 위치 [# 50219](https://github.com/elastic/kibana/pull/50219)
-   모니터 목록 페이지 매김 화살표 수정 [# 51912](https://github.com/elastic/kibana/pull/51912)
-   확장 된 목록 업데이트 가장 최근 오류 시간 소인 [# 51935](https://github.com/elastic/kibana/pull/51935)
-   기능 / 모니터 세부 사항보기는 빈 열 [# 51892를](https://github.com/elastic/kibana/pull/51892) 피하십시오[](https://github.com/elastic/kibana/pull/51892)
-   세부 정보 ping 목록 [# 51890의](https://github.com/elastic/kibana/pull/51890) 기능 / 확장 가능 행[](https://github.com/elastic/kibana/pull/51890)
-   날짜 선택기는 고급 설정에서 일반적으로 사용되는 범위를 사용합니다. [# 52944](https://github.com/elastic/kibana/pull/52944)
-   모니터 페이지 [# 54251](https://github.com/elastic/kibana/pull/54251) 에서 깨진 기간 차트 수정[](https://github.com/elastic/kibana/pull/54251)
-   Ping List 본문이 없으면 확장 행을 사용하지 않도록 설정합니다. [# 54898](https://github.com/elastic/kibana/pull/54898)
-   날짜 범위 선택기 중지 새로 고침 버튼 [# 55499 수정](https://github.com/elastic/kibana/pull/55499)
-   핑 히스토그램 자동 날짜 히스토그램을 사용 하여 [# 55605](https://github.com/elastic/kibana/pull/55605)
-   가동 시간 [# 55446](https://github.com/elastic/kibana/pull/55446) 에서 동적 인덱스 패턴을 사용합니다.[](https://github.com/elastic/kibana/pull/55446)
-   Ping 히스토그램 [# 56381의](https://github.com/elastic/kibana/pull/56381) 절대 날짜 범위를 새로 고칩니다.

**시각화**

-   0 불투명도 TSVB 꺾은 선형 차트에 도메인 맞춤 옵션을 추가합니다. [# 54314](https://github.com/elastic/kibana/pull/54314)
-   CSV [# 54003을](https://github.com/elastic/kibana/pull/54003) 내보낼 때 기본 파일 이름을 추가합니다[](https://github.com/elastic/kibana/pull/54003)
-   CodeEditor의 높이 수정-Safari [# 56050](https://github.com/elastic/kibana/pull/56050)
-   특정 축 및 레이블 필터 구성에서 누락 된 레이블 수정 [# 47563](https://github.com/elastic/kibana/pull/47563)
-   CSV 포맷 [# 54127](https://github.com/elastic/kibana/pull/54127)
-   중첩 된 필드를 집계 불가능으로 플래그 지정 [# 51774](https://github.com/elastic/kibana/pull/51774)

# 지원 중단

**측정 항목**

- 설정에서 재정의 필드를 더 이상 사용하지 않습니다 [# 54206](https://github.com/elastic/kibana/pull/54206)

**보안**

- elasticsearch 사용자 이름 [# 48247에](https://github.com/elastic/kibana/pull/48247) 대한 추가 검증



