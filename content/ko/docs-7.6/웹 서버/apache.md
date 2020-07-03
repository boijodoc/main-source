---
title: "아파치"
linkTitle: "아파치"
type: docs
weight: 1
date: 2020-05-20
description: >
  아파치의 로그를 통합하는 방법에 대해 설명합니다.
---

## 아파치 로그 통합 관리하기

 앞서 설치한 ELK 스택에 아파치의 로그를 통합해서 관리할 수 있습니다. 아파치 로그를 통함 관리하는 방법에 대해 알아보도록 하겠습니다.

## 아파치 웹 로그 종류

 로그를 통합 관리하기 위해선 어떤 로그들이 있는지 알아야 합니다. 아파치에는 기본적으로 두가지 로그가 제공되는데 그 종류는 다음과 같습니다.

<table>
    <thead>
        <th>파일 이름</th>
        <th>내용</th>
    </thead>
    <tbody>
        <tr>
            <td>acces_log</td>
            <td>접속 기록</td>
        </tr>
        <tr>
            <td>error_log</td>
            <td>상세 에러 정보</td>
        </tr>
    </tbody>
</table>


## 아파치 웹 로그 형식

 로그를 파싱해서 Elasticsearch에 저장하려면 로그가 어떻게 생겼는지 알아야 합니다. 로그는 필드로 구분되어 지정된 형식으로 쓰이기 때문에 일종의 패턴이 있습니다.  아파치의 기본 로그 형식에 대해서 알아보겠습니다. 사실 추가적인 설정을 통해 로그에 포함되는 정보의 양을 늘릴 수 있지만 먼저 기본적인 로그들을 한번 이용해보도록 하겠습니다.

- access_log

  ```
  # [원격지 호스트] [원격지 사용자 이름] [인증이 요청된 원격 사용자 이름] [요청한 시간과 날짜] [HTTP 메소드를 포함한 요청의 첫 라인] [HTTP 상태 코드] [헤더를 제외한 전송된 크기]
  196.52.43.100 - - [26/May/2020:04:26:36 +0900] "GET / HTTP/1.1" 200 1711
  ```

   access_log에서는 얻어낼 정보가 많은 것 같습니다. 원격지 호스트를 이용해서 요청한 사람의 위치를 알아낼 수 있고, 어떤 페이지에 어떤 메소드로 요청이 많이 오는지 알 수 있습니다. 어떤 시간이나 어떤 분기에 요청이 많이 들어오는지 분석해서 서버를 스케일 다운/업, 인/아웃 할 지 결정할 수 있고, 요청의 크기를 통해 공격인이 아닌지도 어느 정도 예측이 가능할 것 같습니다.

   하지만 access_log의 기본 형식에서는 어떤 Virtual Host에 대한 요청인지 표시하지 않습니다. 만약 한 서버에서 여러개의 Virtual Host를 운영하고 있다면 아파치의 설정을 변경에 로그의 포맷을 아래와 같이 변경합니다.

  ```
  # /etc/apache2/apache2.conf
  
  # 없다면 추가
  LogFormat "%v:%p %h %l %u %t \"%r\" %>s %O \"%{Referer}i\" \"%{User-Agent}i\"" vhost_combined
  
  # Virtual Host 태그 안에 추가
  CustomLog logs/access.log vhost_combined
  ```

  

- error_log

  ```
  # [요청한 시간과 날짜] [에러 레벨] [pid] [client [IP:Port]] [로그 메시지]
  [Fri May 26 04:13:58.570775 2020] [php7:notice] [pid 2093] [client ::1:56854] PHP Notice:  Undefined variable: remember in /srv/http/getSalt.php on line 13, referer: http://localhost:3000/~120140261/app/login
  ```

  반면 error_log에서는 사실 분석을 자동화하기는 힘들 것 같습니다. 공격을 시도하는 방법은 셀 수 없을 정도로 여러 방법이 있고 어떠한 에러가 발생할지 예측하기는 사실 힘듭니다. 다만 에러 레벨을 통해 크리티컬한 에러들을 모아서 따로 분석할 수 있을 것 같습니다. 또는 에러 레벨로 1차적으로 뽑아낸 로그 메시지들의 분석을 자동화할 수 있을 것 같습니다.

## Filebeat 설치 및 설정

 위에 분석해본 아파치 웹 로그 형식에 따라 로그들을 파싱해서 Elasticsearch에 저장해보도록 하겠습니다. 사실 Logstash만으로도 파일을 읽어들여 Elasticsearch에 저장할 수 있습니다. 하지만, 새로운 데이터가 있을 때 지속적으로 읽어서 Elasticsearch에 저장하기 위해선 Filebeat를 사용해야 합니다. Filebeat를 설치한 후 아파치의 로그를 읽어 Logstash로 전송하게 해보도록 하겠습니다.

**Filebeat의 버전을 ELK 스택과 맞춰줘야 합니다!**

1. [Elastic 홈페이지](https://elastic.co) 접속 후 우측 위에 있는 **무료로 시작**을 클릭합니다.

   ![Elastic 홈페이지](/images/elastic-home.png)

2. Beats의 **다운로드** 버튼을 클릭합니다.

   ![Filebeat 다운로드 1](/images/7.6/filebeat-download-1.png)

3. Filebeat의 **다운로드** 버튼을 클릭합니다.

   ![Filebeat 다운로드 2](/images/7.6/filebeat-download-2.png)

4. 버전을 확인하고 운영체제에 맞는 파일을 다운로드합니다.

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


   ![Filebeat 다운로드 3](/images/7.6/filebeat-download-3.png)

5. 이전 버전을 설치하고 싶다면 아래에 있는 **past releases** 링크를 클릭해서 맞는 버전을 다운로드합니다.

   ![Filebeat 다운로드 3](/images/7.6/filebeat-download-4.png)

6. 패키지 관리자로 다운로드한 Filebeat를 설치합니다.

   ```shell
   # Windows
   logstash-버전-아키텍처.exe or filebeat-버전-아키텍처.msi 실행
   
   # Debian, Ubuntu
   sudo apt-get install ./filebeat-버전-아키텍처.deb
   
   # Red Hat 8 이상, Fedora 22 이상
   sudo dnf install ./filebeat-버전-아키텍처.rpm
   
   # Red Hat 7 이하, Fedora 21 이하, CentOS
   sudo yum install ./filebeat-버전-아키텍처.rpm
   
   # OpenSUSE
   sudo zypper install ./filebeat-버전-아키텍처.rpm
   ```

7. Filebeat의 Apache 모듈 활성 합니다. 설정에서 기본 false인 reload.enable을 true로 바꿔줍니다.

   ```yaml
   # /etc/filebeat/filebeat.yml
   #============================= Filebeat modules ===============================
   
   filebeat.config.modules:
     # Glob pattern for configuration loading
     path: ${path.config}/modules.d/*.yml
   
     # 기본값 false. true로 변경하기
     # Set to true to enable config reloading
     reload.enabled: true
   
     # Period on which files under path should be checked for changes
     #reload.period: 10s
   ```

   ```shell
   sudo filebeat modules enable apache
   ```

    Filebeat는 OS를 감지해서 아파치 로그의 위치를 결정합니다. 만약 로그의 위치를 바꿨거나 여러 개의 로그를 읽어오고 싶다면 Apache 모듈 설정을 변경해서 로그의 위치를 알려줘야 합니다.

   ```yaml
   # /etc/filebeat/modules.d/apache.yml
   
   # Module: apache
   # Docs: https://www.elastic.co/guide/en/beats/filebeat/7.6/filebeat-module-apache.html
   
   - module: apache
     # Access logs
     access:
       enabled: true
   
       # Set custom paths for the log files. If left empty,
       # Filebeat will choose the paths depending on your OS.
       var.paths: ["[경로]"...]
   
     # Error logs
     error:
       enabled: true
   
       # Set custom paths for the log files. If left empty,
       # Filebeat will choose the paths depending on your OS.
       var.paths: ["[경로]"...]
   ```

   

8. Filebeat에서 읽은 데이터를 Logstash로 보내도록 설정합니다. Elasticsearch output 관련 설정을 주석 처리하고 Logstash output 관련 설정을 주석 해제하면 됩니다.

   ```yaml
   # /etc/filebeat/filebeat.yml
   #================================ Outputs =====================================
   
   # Configure what output to use when sending the data collected by the beat.
   
   #-------------------------- Elasticsearch output ------------------------------
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   
     # Protocol - either `http` (default) or `https`.
     #protocol: "https"
   
     # Authentication credentials - either API key or username/password.
     #api_key: "id:api_key"
     #username: "elastic"
     #password: "changeme"
   
   #----------------------------- Logstash output --------------------------------
   output.logstash:
     # The Logstash hosts
     hosts: ["localhost:5044"]
   
     # Optional SSL. By default is off.
     # List of root certificates for HTTPS server verifications
     #ssl.certificate_authorities: ["/etc/pki/root/ca.pem"]
   
     # Certificate for SSL client authentication
     #ssl.certificate: "/etc/pki/client/cert.pem"
   
     # Client Certificate Key
     #ssl.key: "/etc/pki/client/cert.key"
   ```

## Logstash 설정

 앞서 Logstash를 설치했지만 Logstash의 설정은 어떤 데이터를 처리하느냐에 따라 달라지기 때문에 하지 않았습니다. Apache의 로그 데이터를 가공해서 Elasticsearch 저장할 수 있도록 Logstash를 설정합니다.

1. 5044포트에 Filebeat로부터 데이터를 입력받아 Apache2에 맞게 데이터를 가공해서 Elasticsearch의 apache index에 저장하도록 설정합니다.

```
# /etc/logstash/conf.d/logstash.conf

input {
  beats {
    port => 5044
    host => "0.0.0.0"
  }
}
filter {
  if [event][module] == "apache" {
    if [fileset][name] == "access" {
      grok {
        match => { "message" => ["%{IPORHOST:[apache2][access][remote_ip]} - %{DATA:[apache2][access][user_name]} \[%{HTTPDATE:[apache2][access][time]}\] \"%{WORD:[apache2][access][method]} %{DATA:[apache2][access][url]} HTTP/%{NUMBER:[apache2][access][http_version]}\" %{NUMBER:[apache2][access][response_code]} %{NUMBER:[apache2][access][body_sent][bytes]}( \"%{DATA:[apache2][access][referrer]}\")?( \"%{DATA:[apache2][access][agent]}\")?",
          "%{IPORHOST:[apache2][access][remote_ip]} - %{DATA:[apache2][access][user_name]} \\[%{HTTPDATE:[apache2][access][time]}\\] \"-\" %{NUMBER:[apache2][access][response_code]} -" ] }
        remove_field => "message"
      }
      mutate {
        add_field => { "read_timestamp" => "%{@timestamp}" }
      }
      date {
        match => [ "[apache2][access][time]", "dd/MMM/YYYY:H:m:s Z" ]
        remove_field => "[apache2][access][time]"
      }
      useragent {
        source => "[apache2][access][agent]"
        target => "[apache2][access][user_agent]"
        remove_field => "[apache2][access][agent]"
      }
      geoip {
        source => "[apache2][access][remote_ip]"
        target => "[apache2][access][geoip]"
      }
    }
    else if [fileset][name] == "error" {
      grok {
        match => { "message" => ["\[%{APACHE_TIME:[apache2][error][timestamp]}\] \[%{LOGLEVEL:[apache2][error][level]}\]( \[client %{IPORHOST:[apache2][error][client]}\])? %{GREEDYDATA:[apache2][error][message]}",
          "\[%{APACHE_TIME:[apache2][error][timestamp]}\] \[%{DATA:[apache2][error][module]}:%{LOGLEVEL:[apache2][error][level]}\] \[pid %{NUMBER:[apache2][error][pid]}(:tid %{NUMBER:[apache2][error][tid]})?\]( \[client %{IPORHOST:[apache2][error][client]}\])? %{GREEDYDATA:[apache2][error][message1]}" ] }
        pattern_definitions => {
          "APACHE_TIME" => "%{DAY} %{MONTH} %{MONTHDAY} %{TIME} %{YEAR}"
        }
        remove_field => "message"
      }
      mutate {
        rename => { "[apache2][error][message1]" => "[apache2][error][message]" }
      }
      date {
        match => [ "[apache2][error][timestamp]", "EEE MMM dd H:m:s YYYY", "EEE MMM dd H:m:s.SSSSSS YYYY" ]
        remove_field => "[apache2][error][timestamp]"
      }
    }
  }
}
output {
  elasticsearch {
    hosts => localhost
    manage_template => false
    index => "apache"
  }를
}
```

## Index 초기 설정

 Logstash와 Filebeat를 실행해서 데이터를 저장하기 전에 위치 정보 같은 특별한 정보들은 Elasticsearch에서 제대로 인식할 수 있도록 미리 설정해야합니다. 

1. Kibana에 접속해서 Explore my own 링크를 클릭합니다.

   ![Kibana main](/images/7.6/kibana-start.png)

2. Kibana의 왼쪽 메뉴에서 Dev Tools 버튼을 클릭합니다.

   ![Kibana dev tools 1](/images/7.6/kibana-dev-tool.png)

3. 연결된 Elasticsearch에 아래 쿼리를 실행해서 위치 정보에 대한 초기 설정을 진행합니다.

   ```
   PUT apache
   {
     "mappings" : { 
       "properties": {
         "apache2.access.geoip.location" : { 
           "type" : "geo_point"
         }
       }
     }
   }
   ```

   ![Create index 1](/images/7.6/kibana-create-index-1.png)

   ![Create index 2](/images/7.6/kibana-create-index-2.png)

## Logstash, Filebeat 실행

```shell
sudo systemctl enable --now logstash filebeat
```

## Index 패턴 생성

 Elasticsearch에서 저장된 데이터를 사용하기 전에 index 식별과 필드의 설정을 위해서 반드시 index 패턴을 생성해야 합니다. 아래는 위 설정으로 저장된 Apache의 로그 데이터 index의 index 패턴을 생성하는 방법입니다.

2. Kibana의 왼쪽 메뉴에서 Dev Tools 버튼을 클릭합니다.

   ![Kibana dev tools 1](/images/7.6/kibana-dev-tool.png)

3. 연결된 Elasticsearch에 데이터가 정상적으로 저장되고 있는지 확인하는 쿼리를 보냅니다. 하나 이상의 document라도 있다면 데이터의 입력이 시작된 것입니다.

   ```
   GET apache/_count
   ```

   ![Kibana dev tools 1](/images/7.6/kibana-make-pattern-1.png)

   ![Kibana dev tools 2](/images/7.6/kibana-make-pattern-2.png)

4. 다음과 같이 document의 개수가 확인되었다면 index 패턴을 생성하기 위해 왼쪽 메뉴에서 Management 버튼을 클릭합니다. 그 후 Kibana 아래 Index Patterns 버튼을 클릭합니다.

   ![Kibana management 3](/images/7.6/kibana-make-pattern-3.png)

   ![Kibana management 4](/images/7.6/kibana-make-pattern-4.png)

5. Create index pattern 버튼을 클릭해서 index 패턴 생성을 시작합니다.

   	![Kibana management 5](/images/7.6/kibana-make-pattern-5.png)

6. Index 이름을 입력하고 Next step을 클릭합니다. 와일드카드 문자도 사용 가능합니다.

   ![Kibana management 6](/images/7.6/kibana-make-pattern-6.png)

7. @timestamp로 시간 필터 필드를 설정 후 Create index pattern 버튼을 클릭합니다.

   ![Kibana management 7](/images/7.6/kibana-make-pattern-7.png)

## Document 확인하기

1. 생성된 index 패턴을 확인한 뒤 저장된 데이터를 보기 위해서 왼쪽 메뉴에서 Discover를 클릭합니다.

   ![Kibana discover 1](/images/7.6/kibana-check-index-1.png)

2. 오른쪽 위 시간 필터를 보면 기본으로 최근 15분의 데이터를 불러옵니다. 하지만 최근 15분의 데이터가 없기 때문에 아무것도 보이지 않습니다. 시간 필터를 조절해서 데이터를 확인할 수 있습니다.

   ![Kibana discover 2](/images/7.6/kibana-check-index-2.png)

   ![Kibana discover 3](/images/7.6/kibana-check-index-3.png)