# HTTP 상태 코드

## 1xx - 조건부 응답
- `100`(Continue): 지금까지의 상태 OK. 클라이언트가 계속해서 요청을 하거나 이미 요청을 완료한 경우에는 무시해도 됨
- `101`(Switching Protocol): 요청자가 서버에 프로토콜 전환을 요청했으며 서버는 이를 승인중
- `102`(Processing): 서버가 요청 처리 중이지만 제대로 된 응답 X
- `103`(Early Hints): Link 헤더와 함께 사용되어 서버가 응답을 준비하는 동안 사용자 에이전트가(user agent) 사전 로딩(preloading)을 시작할 수 있도록 함

## 2xx - 성공
- `200`(OK): 서버가 요청을 제대로 처리함
- `201`(Created): 성공적으로 요청되었으며 서버가 새 리소스를 작성
- `202`(Accepted): 서버가 요청을 접수했지만 아직 처리 X
- `203`(Non-Authoritative Information): 서버가 요청을 성공적으로 처리했지만 다른 소스에서 수신된 정보를 제공중
- `204`(No Content): 서버가 요청을 성공적으로 처리했지만 콘텐츠를 제공 X
- `205`(Reset Content): 서버가 요청을 성공적으로 처리했지만 콘텐츠를 표시 X. 204 응답과 달리 이 응답은 요청자가 문서 보기를 재설정할 것을 요구 (예: 새 입력을 위한 양식 비우기).
- `206`(Partial Content): 서버가 GET 요청의 일부만 성공적으로 처리
- `207`(Multi Status): 여러 리소스가 여러 상태 코드인 상황이 적절한 경우 해당 정보 전달
- `208`(Multi Status): DAV에서 사용
- `226`(IM Used): GET 요청에 대한 리소스 의무 다함

## 3xx - 디라이렉션 완료
- `300`(Multiple Choice): 서버가 요청에 따라 여러 조치를 선택 가능. 서버가 사용자 에이전트에 따라 수행할 작업을 선택하거나, 요청자가 선택할 수 있는 작업 목록을 제공
- `301`(Moved Permanently): 요청한 페이지를 새 위치로 영구적으로 이동. GET 또는 HEAD 요청에 대한 응답으로 이 응답을 표시하면 요청자가 자동으로 새 위치로 전달
- `302`(Found): 현재 서버가 다른 위치의 페이지로 요청에 응답하고 있지만 요청자는 향후 요청 시 원래 위치를 계속 사용해야 함
- `303`(See Other): 요청자가 다른 위치에 별도의 GET 요청을 하여 응답을 검색할 경우 표시. HEAD 요청 이외의 모든 요청을 다른 위치로 자동으로 전달.
- `304`(Not Modified): 마지막 요청 이후 요청한 페이지는 수정 X. 서버가 이 응답을 표시하면 페이지의 콘텐츠를 표시 X. 요청자가 마지막으로 페이지를 요청한 후 페이지가 변경되지 않으면 이 응답(If-Modified-Since HTTP 헤더라고 함)을 표시하도록 서버를 구성해야 함.
- `305`(Use Proxy): 요청자는 프록시를 사용하여 요청한 페이지만 액세스 O. 서버가 이 응답을 표시하면 요청자가 사용할 프록시를 가리키는 것
- `306`(unused): HTTP 1.1 이전 버전에서만 사용하던 응답 코드
- `307`(temporary redirect): 현재 서버가 다른 위치의 페이지로 요청에 응답하고 있지만 요청자는 향후 요청 시 원래 위치를 계속 사용.
- `308`(Permanent Redirect): HTTP 응답 헤더의 Location에 명시된 다른 URI에 위치하고 있음

## 4xx - 요청 오류
- `400`(Bad Request): 서버가 요청의 구문을 인식 X
- `401`(Unauthorized): 이 요청은 인증이 필요 (인증 실패)
- `402`(Payment Required): 이 요청은 결제가 필요
- `403`(Forbidden): 서버가 요청을 거부. (인가 실패)
- `404`(Not Found): 서버가 요청한 페이지(Resource)를 찾을 수 없음
- `405`(Method Not Allowed): 요청에 지정된 방법을 사용 X.
- `406`(Not Acceptable): 요청한 페이지가 요청한 콘텐츠 특성으로 응답 X
- `407`(Proxy Authentication Required): 요청자가 프록시를 사용한 인증 필수. 서버가 이 응답을 표시하면 요청자가 사용할 프록시를 가리키는 것.
- `408`(Request Timeout): 서버의 요청 대기가 시간을 초과
- `409`(Conflict): 서버가 요청을 수행하는 중에 충돌이 발생
- `410`(Gone): 서버는 요청한 리소스가 영구적으로 삭제되었을 때 이 응답을 표시
- `411`(Length Required): 서버는 유효한 콘텐츠 길이 헤더 입력란 없이는 요청을 수락 ㅌ
- `412`(Precondition Failed): 서버가 요청자가 요청 시 부과한 사전조건을 만족 X
- `413`(Payload Too Large): 요청이 너무 커서 서버가 처리 X
- `414`(URI Too Long): 요청 URI(일반적으로 URL)가 너무 길어 서버가 처리
- `415`(Unsupported Media Type): 요청이 요청한 페이지에서 지원하지 않는 형식
- `416`(Requested Range Not Satisfiable): 요청이 페이지에서 처리할 수 없는 범위에 해당되는 경우 서버는 이 상태 코드를 표시
- `417`(Expectation Failed): 서버는 Expect 요청 헤더 입력란의 요구사항을 만족 X
- `418`(I'm a teapot)
- `421`(Misdirected Request): 서버로 유도된 요청은 응답을 생성 X
- `422`(Unprocessable Entity)
- `423`(Locked): 접근하려는 리소스가 lock
- `424`(Failed Dependency): 이전 요청 실패하여 현재 요청도 실패
- `426`(Upgrade Required): 클라이언트는 업그레이드 헤더 필드에 주어진 프로토콜로 요청을 보내야 함
- `428`(Precondition Required)
- `429`(Too Many Request): 사용자가 일정 시간 동안 너무 많은 요청함
- `431`(Request Header Fields Too Large)
- `451`(Unavailable For Legal Reasons): 불법적 리소스

## 5xx - 서버 오류
- `500`(Internal Server Error): 서버에 오류가 발생
- `501`(Not Implemented): 서버에 요청을 수행할 수 있는 기능 X (ex: 요청 메소드를 인식 불가)
- `502`(Bad Gateway): 서버가 게이트웨이나 프록시 역할을 하고 있거나 또는 업스트림 서버에서 잘못된 응답 받음
- `503`(Service Unavailable): 서버가 오버로드되었거나 유지관리를 위해 다운되었기 때문에 현재 서버를 사용 X
- `504`(Gateway Timeout): 서버가 게이트웨이나 프록시 역할을 하고 있거나 또는 업스트림 서버에서 제때 요청을 받지 못함
- `505`(HTTP Version Not Supported): 서버가 요청에 사용된 HTTP 프로토콜 버전을 지원 X
- `506`(Variant Also Negotiates): 서버 내부 구성 오류. 요청을 위한 투명한 컨텐츠 협상이 순환 참조로 이어짐
- `507`(Insufficient Storage): 서버 내부 구성 오류. 선택한 가변 리소스는 투명한 콘텐츠 협상에 참여하도록 구성되므로 협상 프로세스의 적절한 종료 지점이 아님
- `508`(Loop Detected): 요청 처리 중 무한 루프 감지
- `510`(Not Extended): 서버 요청 이행을 위해 요청에 대한 추가 확장 필요
- `511`(Network Authentication Required): 클라이언트가 네트워크 액세스를 얻기 위해 인증 받아야 할 필요 있음

### 참조
1. wiki - https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C
2. mozilla - https://developer.mozilla.org/ko/docs/Web/HTTP/Status