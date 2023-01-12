### URL

- 자원이 어디 있는지 알려주기 위한 규약
- URL 가장 앞 부분에는 액세스 방법이 쓰여있음 (ex:http, ftp, file, mailto, news, ...)

#### URL 예제

```text
http: http://user:password@www.naver.com:80/dir/file1.html
ftp: ftp://user:password@www.naver.com:80/dir/file1.html
file: file://localhost/cL/path/file1.zip
```

### 브라우저

- 웹 서버에 액세스하는 클라이언트
- 파일 다운로드/업로드 하는 FTP의 클라이언트
- 메일의 클라이언트
- 👉 여러 클라이언트 기능을 겸한 복합적인 클라이언트 소프트웨어

> URL 의 앞 부분에 있는 액세스 방법에 따라 어떤 클라이언트 기능을 사용할지 정해짐

### 브라우저의 URL 해독 과정

> ex: http://www.naver.com:80/dir/file1.html

- URL 요소를 분해
    - 액세스 방법 `http`
    - 웹 서버명 `www.naver.com:80`
    - 데이터 출처 경로명 `/dir/file1.html`

#### 프로토콜

- : 통신 동작의 규칙을 정한 것
- http가 주어졌으므로 위 과정에서 http 프로토콜을 기록해둘 수 있음
- file과 같은 네트워크가 연결되지 않은 액세스 방법도 있으므로 프로토콜이 항상 기록되는 것은 아님

#### HTTP 프로토콜

client <-> server

- request message
    - 무엇을 어떻게 하겠다는 내용 포함
    - 무엇을 = URI
        - 데이터를 저장한 파일명
        - CGI 프로그램의 파일명
    - 어떻게 = 메서드
        - 웹 서버에 어떤 동작을 하고 싶은지
        - ex: GET, POST, ...
- response message
    - 상태 코드
    - 헤더 파일
    - 페이지의 데이터

#### 데이터 출처 경로명이 생략되었다면?

- 서버 측에서 미리 설정해둔 것을 사용
- ex: index.html