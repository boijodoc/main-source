---
title: "Elasticsearch 설치하기"
linkTitle: "Elasticsearch 설치하기"
type: docs
weight: 1
description: >
  가장 기본적인 Elasticsearchfmf 설치 및 설정하는 방법에 대해 설명합니다.
---

 Elasticsearch이 설치된 시스템을 노드라고 합니다. Elasticsearch는 여러 시스템에 설치한 후 연동하는 기능을 제공합니다.  이번에는 Elasticsearch의 가장 기본적인 설치 및 설정 방법에 대해 설명합니다. 이 매뉴얼을 따라하면 로컬 서버에서 Elasticsearch를 통해서 여러 데이터들을 저장하고 분석해서 사용할 수 있을 것입니다.

 여러 노드들을 연동해서 사용하는 방법은 [여기](#)에서 설명하겠습니다.

## Elasticsearch 다운로드 및 설치

**ELK 스택의 버전은 모두 같은 버전으로 맞춰주는 것이 좋습니다!**

1. [Elastic 홈페이지](https://elastic.co) 접속 후 우측 위에 있는 **무료로 시작** 클릭

   ![Elastic 홈페이지](/images/elastic-home.png)

2. Elasticsearch **다운로드** 클릭

   ![Elasticsearch 다운로드 1](/images/7.6/elasticsearch-download-1.png)

3. 버전을 확인하고 운영체제에 맞는 파일 다운로드

   <table>
       <thead>
           <tr>
               <th>운영체제</th>
               <th>파일</th>
           </tr>
       </thead>
       <tbody>
           <tr>
               <td>Windows</td>
               <td>WINDOWS, MSI</td>
           </tr>
           <tr>
               <td>MacOS</td>
               <td>MACOS</td>
           </tr>
           <tr>
               <td>Debian, Ubuntu etc.</td>
               <td>DEB</td>
           </tr>
           <tr>
               <td>Red Hat, Fedora, CentOS, OpenSUSE etc.</td>
               <td>RPM</td>
           </tr>
           <tr>
               <td>Other Linux</td>
               <td>LINUX</td>
           </tr>
       </tbody>
   </table>

   ![Elasticsearch 다운로드 2](/images/7.6/elasticsearch-download-2.png)

4. 이전 버전을 설치하고 싶다면 아래에 있는 **past releases** 링크를 클릭해서 맞는 버전 다운로드

   ![Elasticsearch 버전 선택](/images/7.6/elasticsearch-download-3.png)

5. 패키지 관리자로 다운로드한 Elasticsearch 설치

   ```shell
   # Windows
   elasticsearch-버전-아키텍처.exe or elasticsearch-버전-아키텍처.msi 실행
   
   # Debian, Ubuntu
   sudo apt-get install ./elasticsearch-버전-아키텍처.deb
   
   # Red Hat 8 이상, Fedora 22 이상
   sudo dnf install ./elasticsearch-버전-아키텍처.rpm
   
   # Red Hat 7 이하, Fedora 21 이하, CentOS
   sudo yum install ./elasticsearch-버전-아키텍처.rpm
   
   # OpenSUSE
   sudo zypper install ./elasticsearch-버전-아키텍처.rpm
   ```

