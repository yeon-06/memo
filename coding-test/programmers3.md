### 문제

> 카카오 - 신고 결과 받기

- https://school.programmers.co.kr/learn/courses/30/lessons/92334

<br/>

### 풀이

```java
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;
import java.util.Set;

class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        Map<String, Set<String>> reportUsers = new HashMap<>();
        Map<String, Set<String>> reportedUsers = new HashMap<>();

        for (String r : report) {
            String[] arr = r.split(" ");

            reportUsers.computeIfAbsent(arr[0], it -> new HashSet<>());
            reportUsers.get(arr[0]).add(arr[1]);

            reportedUsers.computeIfAbsent(arr[1], it -> new HashSet<>());
            reportedUsers.get(arr[1]).add(arr[0]);
        }

        int length = id_list.length;
        int[] answer = new int[length];
        for (int i = 0; i < length; i++) {
            int count = 0;
            for (String name : reportUsers.getOrDefault(id_list[i], new HashSet<>())) {
                if (reportedUsers.getOrDefault(name, new HashSet<>()).size() >= k) {
                    count++;
                }
            }
            answer[i] = count;
        }

        return answer;
    }
}
```

### 개선점

- 신고한 사람이 누구인지 기억할 필요 없다. 중복 신고를 미리 제거한 뒤, 신고받은 횟수를 기록하여 메모리를 아낄 수 있다.
- 알고리즘에 집착하지 않고 객체지향 적으로도 풀 수 있다. (ex: User 객체 안에 reportList, reportedList를 만든다던가)
