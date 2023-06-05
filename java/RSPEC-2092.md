# RSPEC-2092 Creating cookies without the "secure" flag is security-sensitive

> https://rules.sonarsource.com/java/RSPEC-2092

Cookie에는 secure라는 필드가 있다.
암호화되지 않은 HTTP 요청을 보내는 경우, 브라우저에서 쿠키를 보내지 않도록 설정할 수 있다.
무분별하게 쿠키를 보낼 수 있게 하는 경우, 중간에서 메시지 가로챔 당할 수 있다.
