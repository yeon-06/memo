### 문제

👉 https://school.programmers.co.kr/learn/courses/30/lessons/86051

### 풀이

1. numbers에서 등장한 숫자를 true로 체크한 뒤, false인 숫자에 대해서만 더하기
2. 전체 합에서 numbers에 등장한 숫자를 제거하기 (👉 선택)

```java
class Solution {
    public int solution(int[] numbers) {
        int sum = 45;
        for (int number : numbers) {
            sum -= number;
        }
        return sum;
    }
}
```
