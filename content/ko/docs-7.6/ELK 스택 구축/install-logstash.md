---
title: "Logstash 설치하기"
linkTitle: "Logstash 설치"
type: docs
weight: 2
date: 2020-04-19
description: >
  가장 기본적인 Logstash를 설치 및 설정하는 방법에 대해 설명합니다.
---

 Logstash는 각 서비스에서 보내오는 데이터들을 가공해서 Elasticsearch에 저장할 수 있는 툴입니다. 사실 Elastic에서 제공하는 Beats만 가지고도 충분히 통합 로그 관리 시스템의 구성이 가능합니다. 하지만 여러 시스템에서 로그를 보내오는 특성상 Elasticsearch로만 처리할 수 있는 데이터의 양엔 한계가 있습니다. 그렇게 때문에 어떠한 중간 매체 없이는 보내오는 데이터 중 일부를 놓치게 되는데 queueing 등의 기능을 통해 이를 해결해주는 것이 Logstash 입니다.

 Logstash의 설정은 통합 로그 관리 시스템을 구성하면서 가장 많이 신경써야할 부분이기도 합니다. 이번에는 Logstash의 가장 기본적인 설치 방법에 대해 설명합니다. Logstash의 세부적인 설정은 각 서비스들을 설치하면서 진행할 것입니다.

# Logstash 설치 및 실행

**ELK 스택의 버전은 모두 같은 버전으로 맞춰줘야 합니다!**

**ELK 스택을 모두 같은 서버에 설치할 필요는 없습니다!**

1. [Elastic 홈페이지](https://elastic.co) 접속 후 우측 위에 있는 **무료로 시작**을 클릭합니다.

   ![Elastic 홈페이지](/images/elastic-home.png)

2. Logstash의 **다운로드** 버튼을 클릭합니다.

   ![Logstash 다운로드 1](/images/7.6/logstash-download-1.png)

3. 버전을 확인하고 운영체제에 맞는 파일을 다운로드합니다.

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

   ![Logstash 다운로드 2](/images/7.6/logstash-download-2.png)

4. 이전 버전을 설치하고 싶다면 아래에 있는 **past releases** 링크를 클릭해서 맞는 버전을 다운로드합니다.

   ![Logstash 다운로드 2](/images/7.6/logstash-download-3.png)

5. Logstash 7.6 버전을 사용하려면 Java 버전 8 이상이 필요합니다. Logstash를 운영할 서버에 Java Runtime Environment 설치합니다.

   ![자바 설치](/images/7.6/logstash-install-1.png)

6. 패키지 관리자로 다운로드한 Logstash를 설치합니다.

   ```shell
   # Windows
   logstash-버전.exe or logstash-버전.msi 실행
   
   # Debian, Ubuntu
   sudo apt-get install ./logstash-버전.deb
   
   # Red Hat 8 이상, Fedora 22 이상
   sudo dnf install ./logstash-버전.rpm
   
   # Red Hat 7 이하, Fedora 21 이하, CentOS
   sudo yum install ./logstash-버전.rpm
   
   # OpenSUSE
   sudo zypper install ./logstash-버전.rpm
   ```

7. Logstash를 시작합니다.

   ```shell
   # Windows
   bin\logstash.bat
   
   # Linux
   sudo systemctl start logstash
   ```

8. 필요한 경우 부팅 시 Logstash를 자동 시작하도록 설정합니다.

   ```shell
   # Windows
   # C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp에 bin\logstash.bat 링크 생성
   
   # Linux
   sudo systemctl enable logstash
   ```
