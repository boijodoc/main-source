---
title: 도입 효과
linkTitle: 도입 효과
layout: docs
---

{{% blocks/cover title="도입 효과" height="auto" %}}

통합 로그 관리 시스템은 여러 시스템들을 운영해야되는 상황에서 정말 유용한 시스템이며, 그 중 ELK스택은 쉬운 접근성과 기술적인 유연함으로 부담없이 구축하실 수 있습니다.
{{% /blocks/cover %}}

{{% blocks/section type="section" color="primary" %}}

## **ELK스택이란?**

**ELK스택**은 Elasticsearch, Logstash, Kibana 이 세 가지의 앞 글자를 따서 ELK스택이라 불립니다.

<table>
  <tr>
   <td><strong>Beats</strong>
   </td>
   <td>특정 목적을 위한 데이터 수집용 플랫폼입니다.
경량 에이전트로 설치되어 로그파일, 메트릭, 네트워크 데이터, windows 이벤트 로그 등 
다양한 유형의 수백, 수천 개의 데이터를 수집하여 Logstash 또는 Elasticsearch로 전송합니다.
   </td>
  </tr>
  <tr>
   <td><strong>Logstash</strong>
   </td>
   <td>모든 데이터를 수집하고 강화 및 통합하기 위한 ELK스택의 중앙 데이터 플로우 엔진입니다.
Logstash 필터는 입력된 데이터들을 통합된 형식으로 변환하여 분석이 용이하도록 만들어줍니다. 
그 후 저장소인 Elasticsearch로 데이터를 전송합니다.
   </td>
  </tr>
  <tr>
   <td><strong>Elasticsearch</strong>
   </td>
   <td>데이터를 분산하여 저장하기에 모든 데이터에 빠른 속도로 접근할 수 있습니다.
Java, Python, .NET, PHP와 같은 다양한 언어로도 클라이언트 구축 및 유지 관리가 가능하기에 작업이 용이합니다.
Elasticsearch 클러스터는 인덱스와 쿼리 배포 방법을 자동으로 관리하면서 초당 엄청난 양의 이벤트를 처리할 수 있도록 수평적 확장이 가능합니다.
   </td>
  </tr>
  <tr>
   <td><strong>Kibana</strong>
   </td>
   <td>사용자들이 단순히 클릭과 드래그만으로도 데이터의 심층 분석이 가능하도록 개발되었습니다.
히스토그램, 라인 그래프, 파이 차트, 선버스트와 같은 형태로 데이터를 시각화하며, 
Elastic Map 서비스를 활용해 위치정보 데이터를 시각화하기도 합니다.
   </td>
  </tr>
  <tr>
   <td><strong>X-Pack</strong>
   </td>
   <td>ELK스택의 확장 패키지입니다.
확실한 보안, 효율적인 모니터링, 용이한 보고서 작성 기능과 같은 엔터프라이즈 운영환경을 갖출 수 있습니다.
   </td>
  </tr>
</table>

{{% /blocks/section %}}

{{% blocks/section type="section" color="white" %}}

## **도입 효과**

<table>
  <tr>
   <td><strong>운영개선</strong>
   </td>
   <td>ㆍ분산되어 관리한 로그를 로그세이버를 통해 통합 관리할 수 있습니다. <br>
ㆍ로그 수집 및 검색 시 빠른 속도로 이용할 수 있습니다.
   </td>
  </tr>
    <tr>
   <td><strong>사고대응</strong>
   </td>
   <td>ㆍ이상징후를 탐지할 수 있습니다. <br>
ㆍ사고발생 시 원활한 추적 및 원인 분석을 할 수 있습니다. <br>
   </td>
  </tr>
    <tr>
   <td><strong>보안관리</strong>
   </td>
   <td>ㆍ실시간 모니터링을 지원합니다. <br>
   ㆍ행위분석을 통한 기업의 내부정보 유출 및 위협을 감시할 수 있습니다.
   </td>
  </tr>
</table>

{{% /blocks/section %}}

{{% blocks/section type="section" color="white" %}}

## **적용 사례**

<table>
  <tr>
   <td><strong>POSCO</strong>
   </td>
   <td>사용자 중심의 Enterprise search 기능 구현을 위한 검색엔진 교체 
   </td>
  </tr>
    <tr>
   <td><strong>NSHC</strong>
   </td>
   <td>Dark Web에서 Elasticsearch를 활용한 보안 데이터 수집 및 분석
   </td>
  </tr>
    <tr>
   <td><strong>BPCE</strong>
   </td>
   <td>보안과 확장성이 좋은 멀티비즈니스 서비스 플랫폼
   </td>
  </tr>
    <tr>
   <td><strong>11번가</strong>
   </td>
   <td>Elasticsearch를 통한 주문/결제에 대한 모니터링 및 이상 감지에 대한 Alert & 머신러닝 적용
   </td>
  </tr>
    <tr>
   <td><strong>InfoTrack</strong>
   </td>
   <td>lasticsearch Service로 데이터 기반 혁신을 위한 검색 지원
   </td>
  </tr>
    <tr>
   <td><strong>Box</strong>
   </td>
   <td>Observability를 위한 ELK Stack 적용 및 로깅 수집 비용 절감
   </td>
  </tr>
    <tr>
   <td><strong>PSCU</strong>
   </td>
   <td>수백만 달러에 달하는 신용 조합 사기를 방지하여 위험 절감 탐지
   </td>
  </tr>
    <tr>
   <td><strong>Barclays</strong>
   </td>
   <td>문제 발생 시 원활한 추적 및 원인 분석을 하고 머신러닝을 적용하여 관리
   </td>
  </tr>
</table>


{{% /blocks/section %}}
