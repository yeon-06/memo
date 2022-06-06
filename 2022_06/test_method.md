## 테스트 코드 작성 시 스트레스 줄이기

> 나는 테스트 메서드 이름을 짓는게 너무 스트레스였다.
> `@DisplayName`을 통해 열심히 이름을 생각하고 메서드 이름을 또 생각해야한다니...
> 과감하게 한글 이름을 지어보려고 한다.

### 메서드 이름 한글로 짓기

```java
@SuppressWarnings("NonAsciiCharacters")
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
class NicknameTest {
    // ...
}
```

- `@SuppressWarnings`
    - 여러 경고를 무시할 수 있게 해준다.
    - `NonAsciiCharacters` 옵션을 줘서 한글 메서드를 이름을 지어도 경고가 뜨지 않는다.
- `@DisplayNameGeneration`
    - 클래스, 메서드 등의 이름을 변형시켜준다.
    - `DisplayNameGenerator.ReplaceUnderscores.class`를 통해 _로 표기한 부분은 공백으로 처리된다.

#### 예제 코드

```java
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
@SuppressWarnings("NonAsciiCharacters")
class NicknameTest {

    @Test
    void 올바르지_않은_글자수로_생성(String value) {
        assertThatIllegalArgumentException()
                .isThrownBy(() -> new Nickname("연"))
                .withMessage(String.format("닉네임은 2 ~ 10자로 생성 가능합니다. 입력값: %s", value));
    }
}
```

![](../images/test_result.png)

#### 예제 코드

> 영어로 된 메서드를 이해하기 힘든건 아니지만 같은 코드를 놓고 볼 때 한글이 눈에 더 잘 들어온다.

AS-IS

```java
@SuppressWarnings("NonAsciiCharacters")
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
public class CustomerAcceptanceTest {

    @Test
    void 회원_가입_비밀번호_빈값으로_인해_실패() {
        Map<String, Object> request = 회원_정보("leo123", "");
        ExtractableResponse<Response> response = 회원_가입(request);
        assertThat(response.statusCode()).isEqualTo(HttpStatus.BAD_REQUEST.value());
    }
}
```

TO-BE

```java
public class CustomerAcceptanceTest {

    @DisplayName("회원 가입 비밀번호 빈값으로 인해 실패")
    @Test
    void sign_up_with_empty_password() {
        Map<String, Object> request = createUserInfo("leo123", "");
        ExtractableResponse<Response> response = signUp(request);
        assertThat(response.statusCode()).isEqualTo(HttpStatus.BAD_REQUEST.value());
    }
}
```