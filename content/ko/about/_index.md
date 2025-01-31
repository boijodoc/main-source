---
title: 프로젝트 소개
linkTitle: 소개
layout: docs
---

{{% blocks/cover title="프로젝트 소개" height="auto" %}}

 보이조는 누구나 손쉽게 따라하면서 ELK 스택으로 로그 통합 관리 시스템을 구축할 수 있도록 도와주는 서비스입니다. ELK 스택을 구성하는 방법과 각종 서비스들이 생성하는 로그들을 통합하는 방법을 매뉴얼로 제공합니다. 매뉴얼은 버전마다 따로 제공되고 버전 선택에 참고할 수 있도록 버전이 바뀌면서 변경된 사항들을 제공합니다.

가장 최근 버전의 매뉴얼은 [여기](/docs/)에서 확인할 수 있습니다!
{{% /blocks/cover %}}

{{% blocks/section type="section" color="primary" %}}
## 통합 로그 관리 시스템이란?

 4차 산업혁명 시대가 열리면서 여러 가지 정보 시스템이 생겨났습니다. 모든 사물을 인터넷에 연결한다는 IoT, 인공지능을 결합한 인공지능 자동차, 네트워크에서 해킹을 방어하는 방화벽, 의료기기, PC까지 모든 정보 시스템이 엄청난 수의 로그를 생성합니 다. 하지만, 어떤 시스템인지, 어떤 회사에서 만들었는지에 따라 로그의 형식이 달라 각 각 따로 확인해야 하는 현실입니다. 

 **통합 로그 관리 시스템**은 모든 시스템에서 생성된 로그를 모아서 관리할 수 있는 시 스템입니다. 통합 로그 관리 시스템을 사용하면 이러한 것들을 할 수 있습니다.:

*   **통합**: 어떤 시스템에서 생성된 로그던지 원하는 형식에 맞춰 통합할 수 있습니다.
*   **분석**: 통합된 로그들을 이용해서 분석하여 사용할 수 있습니다. 여러 로그들의 정보를 취합해 의미있는 정보로 만들 수 있습니다.
*   **위협 감지**: 로그 분석으로 얻은 데이터를 대시보드에 시각화해서 위협 감지 등 실시간으로 어떠한 일이 일어나는 지 쉽게 파악할 수 있습니다.

{{% /blocks/section %}}

{{% blocks/section type="section" color="white" %}}
## 보이조로 무엇을 할 수 있나요?

 대기업이 아닌 회사에서는 쉽게 통합 로그 관리 시스템을 도입하기 어렵습니다. 비용 적인 측면의 문제부터 구축의 어려움 등 여러 가지 문제가 있습니다. 하지만, Elastic이 무료로 제공하는 [ELK 스택](https://elastic.co)을 사용하면 로그 통합 관리 시스템을 구축할 수 있습니다. 보이조는 ELK 스택의 설치부터 각종 시스템의 로그들을 통합하는 방법까지 단계별로 매뉴얼을 제공합니다.

 매뉴얼은 ELK 스택의 메이저 버전마다 따로 제공되며 각 매뉴얼은 다음과 같은 항목 들을 포함합니다.

<table>
  <tr>
   <td><strong>ELK 스택 설치</strong>
   </td>
   <td>Elasticsearch와 Kibana를 설치하고, Elasticsearch에 저장된 데이터를 Kibana에서 운용하는 방법을 설명합니다.
   </td>
  </tr>
  <tr>
   <td><strong>Beats 사용</strong>
   </td>
   <td>각 정보 시스템에서 생성되는 로그들을 Beats를 이용해서 Elasticsearch로 통합하는 방법을 설명합니다.
   </td>
  </tr>
  <tr>
   <td><strong>Logstash 사용</strong>
   </td>
   <td>여러 시스템에서 로그를 통합할 때 Logstash를 사용하여 여러 로그를 원하는 형식으로 변환해서 Elasticsearch에 통합하는 방법을 설명합니다.
   </td>
  </tr>
  <tr>
   <td><strong>자동화</strong>
   </td>
   <td>로그 통합 시스템 구축을 자동화하는 방법에 대해 설명하고, 자동화 예제들을 제공합니다.
   </td>
  </tr>
</table>
{{% /blocks/section %}}

