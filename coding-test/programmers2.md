### 문제

### 첫번째 시도
- 시간 초과

```java

class Solution {

    private int max = 0;
    private boolean[] visited;

    public String solution(String number, int k) {
        int[] arr = Arrays.stream(number.split(""))
                .mapToInt(Integer::parseInt)
                .toArray();
        int length = arr.length;
        visited = new boolean[length];

        calculate(arr, length, length - k, 0);
        return String.valueOf(max);
    }

    private void calculate(int[] numbers, int length, int k, int cnt) {
        if (k == cnt) {
            max = Math.max(toNumber(numbers, k), max);
            return;
        }

        for (int i = 0; i < length; i++) {
            if (!visited[i]) {
                visited[i] = true;
                calculate(numbers, length, k, cnt + 1);
                visited[i] = false;
            }
        }
    }

    private int toNumber(int[] numbers, int k) {
        int length = numbers.length;
        int sum = 0;

        for (int i = 0; i < length; i++) {
            if (visited[i]) {
                sum = sum * 10 + numbers[i];
            }
        }
        return sum;
    }
}

```

### 두번째 시도

- 테스트 1, 11, 12 통과
- 나머지 런타임 에러
- 이 경우 자연수 범위가 0인 경우도 고려하라는데 전혀 도움이 되지 않은 말이었음..

```java

class Solution {

    private long max = Integer.MIN_VALUE;
    private boolean[] visited;

    public String solution(String number, int k) {
        int length = number.length();
        visited = new boolean[length];

        calculate(number, 0, length, length - k, 0);
        return String.valueOf(max);
    }

    private void calculate(String number, int start, int length, int selectCount, int nowCount) {
        if (selectCount == nowCount) {
            StringBuilder now = new StringBuilder();
            for (int i = 0; i < length; i++) {
                if (now.length() == selectCount) {
                    break;
                }
                if (visited[i]) {
                    now.append(number.charAt(i));
                }
            }
            max = Math.max(Long.parseLong(now.toString()), max);
            return;
        }

        for (int i = start; i < length; i++) {
            if(visited[i]) {
                continue;
            }
            visited[i] = true;
            calculate(number, i + 1, length, selectCount, nowCount + 1);
            visited[i] = false;
        }
    }
}

```

### 해답

- 결국은 풀지 못했다
- 내일 재시도해보기로 하자.
