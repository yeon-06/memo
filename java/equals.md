equals()를 정의할 때는 hashCode()도 함께 재정의하라곤 한다.

그래서 나는 hashCode() = 주소값 정도로 생각하고 해당 메서드들을 재정의하면 `==`으로 비교했다.

하지만 hashCode != 주소값 이었고..

`equals`는 재정의한 것에 따라 다르겠지만 내부 값을 비교하고,  
`==`는 주소 값을 비교한다.

주소값도 아닌데 hashCode를 재정의하는 이유는 HashMap 때문이다.

***
https://okky.kr/article/596050