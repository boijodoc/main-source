---
title: "Kibana 설치하기"
linkTitle: "Kibana 설치"
type: docs
weight: 3
date: 2020-04-19
description: >
  가장 기본적인 Kibana를 설치 및 설정하는 방법에 대해 설명합니다.
---

 Kibana는 Elasticsearch를 조작하거나, 저장되어있는 데이터를 시각화할 수 있는 툴입니다. 웹 서버 형태로 동작하기 때문에 웹 브라우저로 어떤 디바이스에서든지 쉽게 접근할 수 있습니다. 이번에는 Kibana의 가장 기본적인 설치 및 설정 방법에 대해 설명합니다. 이 매뉴얼을 따라하면 Kibana를 통해 로컬 또는 외부에 있는 Elasticsearch에 접근할 수 있을 것입니다.

# Kibana 설치 및 실행

**ELK 스택의 버전은 모두 같은 버전으로 맞춰줘야 합니다!**

**ELK 스택을 모두 같은 서버에 설치할 필요는 없습니다!**

1. [Elastic 홈페이지](https://elastic.co) 접속 후 우측 위에 있는 **무료로 시작**을 클릭합니다.

   ![Elastic 홈페이지](/images/elastic-home.png)

2. Kibana의 **다운로드** 버튼을 클릭합니다.

   ![Kibana 다운로드 1](/images/7.6/kibana-download-1.png)

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

   ![Kibana 다운로드 2](/images/7.6/kibana-download-2.png)

4. 이전 버전을 설치하고 싶다면 아래에 있는 **past releases** 링크를 클릭해서 맞는 버전을 다운로드합니다.

   ![Logstash 다운로드 2](/images/7.6/kibana-download-3.png)

5. 패키지 관리자로 다운로드한 Kibana를 설치합니다.

   ```shell
   # Windows
   logstash-버전-아키텍처.exe or kibana-버전-아키텍처.msi 실행
   
   # Debian, Ubuntu
   sudo apt-get install ./kibana-버전-아키텍처.deb
   
   # Red Hat 8 이상, Fedora 22 이상
   sudo dnf install ./kibana-버전-아키텍처.rpm
   
   # Red Hat 7 이하, Fedora 21 이하, CentOS
   sudo yum install ./kibana-버전-아키텍처.rpm
   
   # OpenSUSE
   sudo zypper install ./kibana-버전-아키텍처.rpm
   ```

6. Kibana가 제어할 Elasticsearch가 로컬에 있다면 단순히 Kibana 실행시키기만 해도 작동합니다. Kibana를 실행합니다.

   ```shell
   # Windows
   bin\kibana.bat
   
   # Linux
   sudo systemctl start kibana
   ```

7. 필요한 경우 부팅 시 Kibana를 자동 시작하도록 설정합니다.

   ```shell
   # Windows
   # C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp에 bin\kibana.bat 링크 생성
   
   # Linux
   sudo systemctl enable kibana
   ```

8. 웹 브라우저로 Kibana가 제대로 시작됐는지 확인합니다.

   ![Kibana 시작](/images/7.6/kibana-start-1.png)

# Kibana 설정

 Kibana의 설정 파일인 /etc/kibana/kibana.yml을 변경하여 설정할 수 있는 부분에 대해서 다룹니다.

## 포트 변경

 Kibana의 기본 포트는 5601 입니다. 만약 다른 포트를 사용하고 싶다면 아래 옵션을 변경합니다.

```yaml
server.port: [포트]
```

## 외부 접속 허용

 Kibana는 기본적으로 로컬에서만 접속 가능하도록 되어있습니다. 외부에서 접속이 가능하게 하려면 아래 옵션을 서버의 IP 주소로 설정합니다. 아래 옵션을 0.0.0.0으로 설정하면 어디서나 접속 가능합니다.

 Elasticsearch와 마찬가지로 Kibana는 연결된 Elasticsearch를 제어할 수 있기 때문에 외부 접속을 허용하는 것은 좋지 않습니다. 부득이하게 외부에 공개해야될 상황에는 방화벽이나 Apache, Nginx의 접근 제어로 보안을 하는 것이 좋습니다.

```yaml
server.host: "[IP]"
```

## 다른 Elasticsearch 연결

 Kibana는 기본적으로 로컬에 있는 Elasticsearch를 제어합니다. 다른 서버에 있는 Elasticsearch를 제어하려면 Kibana의 설정 파일인 /etc/kibana/kibana.yml에 있는 옵션을 바꿔야합니다.

```yaml
elasticsearch.hosts: ["http://[IP]:[Port]"...]
```



