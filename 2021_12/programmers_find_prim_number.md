# 프로그래머스 level 2 -소수 찾기
> https://programmers.co.kr/learn/courses/30/lessons/42839

```java
import java.util.Set;
import java.util.HashSet;

class Solution {
    private Set<Integer> set = new HashSet<>();
    private boolean[] visited;

    public int solution(String numbers) {
        int length = numbers.length();
        char[] numberArr = numbers.toCharArray();
        visited = new boolean[length];

        for (int i = 1; i <= length; i++) {
            int[] temp = new int[i];
            comb(numberArr, temp, 0, i);
        }

        return set.size();
    }

    private void comb(char[] arr, int[] temp, int depth, int n) {
        if (depth == n) {
            int num = convertArrToInt(temp);
            if (isPrime(num)) {
                set.add(num);
            }
            return;
        }

        for (int i = 0; i < arr.length; i++) {
            if (!visited[i]) {
                visited[i] = true;
                temp[depth] = arr[i] - '0';
                comb(arr, temp, depth + 1, n);
                visited[i] = false;
            }
        }
    }

    private int convertArrToInt(int[] arr) {
        int num = 0;
        for (int a : arr) {
            num = num * 10 + a;
        }
        return num;
    }

    private boolean isPrime(int num) {
        if (num < 2) return false;

        for (int i = 2; i <= num / 2; i++) {
            if (num % i == 0) {
                return false;
            }
        }
        return true;
    }
}
```

### isPrime() 리팩토링
> 에라토스테네스의 체 이용

```java
public boolean isPrime(int n) {
    if(n < 2) return false;
    for (int i = 3; i <= (int)Math.sqrt(n); i += 2) {
        if(n % i == 0) {
            return false;
        }
    }
    return true;
}
```