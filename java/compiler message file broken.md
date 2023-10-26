컴파일 실패 에러 로그 `compiler message file broken`

저 로그를 보고 컴파일 실패 원인을 정확히 알 수는 없었지만, 커밋 단위를 작게 했던 덕에 어떤 코드에서 문제가 있는지는 바로 알 수 있었다.
RestTemplate을 호출한 다음 try-catch하는 코드가 반복적이기 때문에 제네릭을 이용해 메서드 추출을 했는데 해당 부분에서 발생한 문제였다.

```
restTemplate.exchange(
          targetUrl,
          HttpMethod.GET,
          new HttpEntity<>(null, getAuthHeader()),
          new ParameterizedTypeReference<>() {
          }
  );
```
위 코드에서 ParameterizedTypeReference에 결과값에 대한 타입을 정확히 명시해주었더니 해결이 되었다.

참고: https://reiphiel.tistory.com/130
