> 자세한 설명: https://yeonyeon.tistory.com/173

## 1. 어쩌다 발견되었나? 🤔

마인 크래프트라는 게임을 누구나 한번쯤은 본 적이 있을 것이다.  
이번 사태는 해당 게임의 기술자를 통해 본격적으로 널리 알려지게 되었다.

### 11/24
- 알리바바에 의해 취약점 발견

### 12/10
- PaperMC가 Discord를 통해 긴급 패치된 파일로 업데이트 하도록 긴급 공지  
  (PaperMC: 마인크래프트의 마크 멀티플레이 버킷 서비스)
- GitHub Advisory Database에 CVE-2021-44228 취약점 게재  
  (GitHub Advisory Database: 오픈소스 sw의 알려진 보안 취약점에 대한 db web site)
- 마인크래프트 기술 책임자가 본인 트위터 및 마인크래프트 홈페이지에 해당 내역 발표

이와 관련해 CVE-2021-45046, CVE-2021-4104까지 여러 취약점이 나왔다.

## 2. 취약점의 원인 👿

취약점의 원인은 Log4j 2에 있다.  
Log4j란 Java 기반의 로깅 프레임워크 오픈 소스이다.  
Java에서 로그를 사용한다면 다 한번쯤은 써봤고 정말 많은 기업들이 사용하는 프레임워크라 이와 같은 이슈화가 됐다.

이 Log4j 라이브러리를 통해 zero-day 공격이 가능하다.  
어떤 상황에서는 사용자가 입력한 데이터가 로그로 남기도 한다.  
이 사용자 입력에 특수 문자를 포함하거나 log4j의 컨텍스트에서 기록되어야 하는 경우, Java 메소드 조회가 호출되며 LDAP 서버에서 사용자 정의한 원격 클래스를 실행한다.  
이로 인해 취약한 Log4j 2 인스턴스를 사용하는 서버에서는 RCE로 이어진다.

## 3. 악용될 수 있는 범위 😭

많은 서비스들이 이 취약점에 시달리고 있다.  
Steam, Apple iCloud 같은 클라우드 서비스들을 포함해 많은 서비스들이 대응 완료 또는 진행중이다.

### 영향받는 버전
Log4j 2.x ~ 2.15.0-rc1
(2버전 미만은 해당 문제는 적용되지 않지만 많은 취약점이 존재하므로 업데이트를 권장)

### 영향받는 소프트웨어
- Apache Struts
- Apache Solr
- Apache Druid
- Apache Flink
- ElasticSearch
- Flume
- Apache Dubbo
- Logstash
- Kafka
- Spring-Boot-starter-log4j2

## 4. 대응 방법 👊
Java 8의 경우에는 `Log4j 2.16.0`,  
Java 7의 경우에는 `Log4j 2.12.2` 버전을 권고하고 있다.

JndiLookup 클래스를 경로에서 직접 제거할 수 있으나 임시 조치에 불과하다.
```
zip -q -d log4j-core-*.jar org/apache/logging/log4j/core/lookup/JndiLookup.class
```

### Spring boot
spring-boot-starter-logging에 포함된 log4j-ot-slf4j와 log4j-api jar는 악용될 수 없다고 밝혔다.  
다만 log4j-core는 취약점에 해당되는데 12/23에 2.5.8과 2.6.2 버전의 release를 예정해두었다.  
그 전까지는 임의로 종속성을 overriding해서 사용하면 될 것 같다.

***
참고
- Paloalto Network - Another Apache Log4j Vulnerability Is Actively Exploited in the Wild (CVE-2021-44228)
- wiki - Log4j 보안 취약점 사태
- 전자 정부 표준 프레임워크 - Log4j 보안 업데이트 긴급 공지
- fireeye - zero-day
- encyclopedia - RCE
- Spring boot - Log4J2 Vulnerability and Spring Boot
- unit42 - apache log4j vulnerability
- lunasec - Log4Shell
- docs.oracle - JNDI
- IT 용어 위키 - LDAP