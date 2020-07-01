---
title: "Elasticsearch 설치하기"
linkTitle: "Elasticsearch 설치"
type: docs
weight: 1
date: 2020-04-19
description: >
  가장 기본적인 Elasticsearchfmf 설치 및 설정하는 방법에 대해 설명합니다.
---

 이번에는 Elasticsearch의 가장 기본적인 설치 및 설정 방법에 대해 설명합니다. 이 매뉴얼을 따라하면 로컬 서버에서 Elasticsearch를 통해서 여러 데이터들을 저장하고 분석해서 사용할 수 있을 것입니다.

## Elasticsearch 설치 및 실행

**ELK 스택의 버전은 모두 같은 버전으로 맞춰주는 것이 좋습니다!**

**ELK 스택을 모두 같은 서버에 설치할 필요는 없습니다!**

1. [Elastic 홈페이지](https://elastic.co) 접속 후 우측 위에 있는 **무료로 시작**을 클릭합니다.

   ![Elastic 홈페이지](/images/elastic-home.png)

2. Elasticsearch **다운로드** 링크를 클릭합니다.

   ![Elasticsearch 다운로드 1](/images/7.6/elasticsearch-download-1.png)

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

   ![Elasticsearch 다운로드 2](/images/7.6/elasticsearch-download-2.png)

4. 이전 버전을 설치하고 싶다면 아래에 있는 **past releases** 링크를 클릭해서 맞는 버전을 다운로드합니다.

   ![Elasticsearch 버전 선택](/images/7.6/elasticsearch-download-3.png)

5. 패키지 관리자로 다운로드한 Elasticsearch를 설치합니다.

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

6. Elasticsearch는 기본적으로 로컬에서 운용할 수 있는 설정과 함께 설치됩니다. 설치한 Elasticsearch를 실행합니다.

   ```
   # Windows
   bin\elasticsearch.bat 실행
   
   # Linux
   sudo systemctl start elasticsearch
   ```

7. Elasticsearch는 기본적으로 9200포트에서 돌아갑니다. 웹 요청을 통해 제대로 실행됐는지 확인할 수 있습니다. Curl 명령어를 통해 쉽게 사용이 가능합니다. 윈도우의 경우 [postman](https://www.postman.com/)을 사용하면 GUI 환경에서 쉽게 사용할 수 있습니다.

   ![Elasticsearch 시작](/images/7.6/elasticsearch-start-1.png)

## Elasticsearch 설정

 Elasticsearch가 설치된 시스템을 하나의 노드라고 합니다. Elasticsearch는 여러개의 노드로 구성된 클러스터 단위로 시스템을 운용하는 기능을 제공하지만 이번에는 가장 기본적인 시스템을 구성할 것입니다. 아래 방법들을 통해 Elasticsearch를 단일 노드로 운영할 수 있도록 설정해보도록 하겠습니다.

 Elasticsearch의 설정은 리눅스 기준 /etc/elasticsearch/elasticsearch.yml 입니다. 모든 설정은 이미 파일에 존재하지만 주석이 되어있어 적용되지 않는 상태입니다. 주석을 해제한 후 값을 바꾸거나 주석된 줄을 아래에 복사 붙여넣기한 후 수정하면 됩니다.

 클러스터의 필요성은 [여기](클러스터)에서 설명하겠습니다.

### 포트 변경

```yaml
http.port: [포트]
```

### 외부 접속 허용

 [IP]에 루프백 주소가 들어가면 로컬에서, 사설 혹은 공인 IP가 들어가면 같은 네트워크 대역대에서, 0 혹은 0.0.0.0이 들어가면 전체에서 접근이 가능합니다.

 미리 설정된 값을 입력할 수 도 있는데 미리 설정된 값들은 [여기](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/modules-network.html#network-interface-values)에서 확인 가능합니다.

 모든 IP에서 접속을 허용하는 것은 보안상 안전하지 않습니다. 네트워크 대역대로 제한할 수 없다면 접근할 호스트를 화이트리스트 형식으로 제한하는 것이 안전합니다. 접근 제한 설정은 [여기](#접근-제한)에서 확인할 수 있습니다.

```yaml
cluster.initial_master_nodes: ["node-1"]
network.host: [IP]
```

### 접근 제한

 부득이하게 모든 호스트에서 접속을 허용해야됐지만 특정 호스트만 접근할 수 있도록 하고싶다면 외부 프로그램을 사용해야 합니다. Elastic에서도 이러한 기능들을 제공하지 않는 것은 아니지만 보안 기능의 경우 유료인 [xpack](https://www.elastic.co/guide/kr/x-pack/current/xpack-introduction.html)으로 제공되고 있기 때문입니다. 아래는 xpack 외에 생각해볼만한 옵션들입니다.

1. iptables 등 방화벽으로 Elasticsearch 포트(기본 9200)의 인바운드 제한

   ```shell
   iptables -A INPUT -p tcp -s [IP] --dport 9200 -j ACCEPT
   iptables -A INPUT -p tcp --dport 9200 -j DROP
   ```

2. Elasticsearch를 루프백 주소로 운용하고 Apache의 [mod_proxy](https://httpd.apache.org/docs/current/mod/mod_proxy.html)나, Nginx의 [Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/) 등의 프록시 기능을 사용. Apache의 [Access Control](https://httpd.apache.org/docs/2.4/howto/access.html) 설정, Nginx [접근 제한 설정](https://docs.nginx.com/nginx/admin-guide/security-controls/controlling-access-proxied-tcp/) 등의 접근 제한 사용.

### 자동 시작

 Elasticsearch가 부팅 시 자동으로 시작되게 하는 방법은 다음과 같습니다.

```shell
# Windows
# C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp에 bin\elasticsearch.bat 링크 생성

# Linux
sudo systemctl enable elasticsearch
```



