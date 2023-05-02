### `Accept`와 `Content-Type` 은 무엇이 다를까

* Accept: 클라이언트가 어떤 컨텐츠 타입을 받길 원하는가
* Content-Type: 클라이언트가 어떤 컨텐츠 타입을 실제로 보내는가

따라서 일반적으로 Accept는 request에, Content-Type은 response에 포함되는듯하다.
Content-Type이 request에 포함되는 경우도 종종 있는데, POST나 PUT같이 request임에도 불구하고 데이터를 보내야하는 경우가 있기 때문이다.

***
참고: https://webmasters.stackexchange.com/questions/31212/difference-between-the-accept-and-content-type-http-headers 
