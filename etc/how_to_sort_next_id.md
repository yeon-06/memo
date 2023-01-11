Section은 2개의 Station을 가지고 있다.

```java
public class Section {
    private Long start_id;
    private Long end_id;
}
```

아래 예제가 있다고 하면 `정자역 -> 수내역 -> 서현역` 순서로 이어졌다고 표현할 수 있다.

```java
Section section1 = new Section(정자역_id, 수내역_id);
Section section2 = new Section(수내역_id, 서현역_id);
```

주어진 `List<Section>`을 이용해 정렬된 `List<Station>`을 가져오려고 한다.  
여러가지 정렬 알고리즘이 존재하겠지만 어떤 크루가 제안해준 방법을 사용하면 O(n)로도 충분해서 이 방법을 적용해보려고 한다.

1. List -> HashMap으로 변환
    - `Map<Long, Long>`
    - key, value -> {start_id, end_id}
2. 아무 Section이나 기준점을 두고 start_id와 이어지는 Station 찾기 (map 이용)
    - 더 찾지 못할때까지 반복
    - List의 0번째 위치에 넣기
3. end_id와 이어지는 Station 찾기
    - 더 찾지 못할때까지 반복
    - List의 마지막 위치에 넣기
