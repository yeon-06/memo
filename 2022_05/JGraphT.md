> 지하철 최단 경로를 구하기 위해 JGraphT 라이브러리를 사용했다.

### graph 생성하기

- 참고로 value는 DefaultWeightedEdge를 상속받은 클래스여야 한다.
- DefaultWeightedEdge의 getWeight()를 오버라이드하지 않는다면 graph.setEdgeWeight()를 해줘야 한다.

```
WeightedMultigraph<key 타입, value 타입> graph = new WeightedMultigraph<>(value타입.class);
graph.addVertex(key추가);
graph.addEdge(value추가);
```

### 최단 경로 찾기

- 위에서 생성했던 WeightedMultigraph 활용
- getVertextList()를 통해 거쳐온 vertex를 구할 수 있다.
- getEdgeList(), getWeight() 등 다양한 메서드 지원

```
DijkstraShortestPath<key타입, value타입> dijkstraShortestPath = new DijkstraShortestPath<>(graph);
dijkstraShortestPath.getPath(출발지점, 도착지점).getVertexList();
```

