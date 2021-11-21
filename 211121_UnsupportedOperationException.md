# java.lang.UnsupportedOperationException ... 에러

### ❓ 에러 원인
Unsupported Opertation Exception. 지원되지 않는 작업을 요청했기 때문에 발생한 에러이다.

해당 에러가 발생한 코드는 아래와 같다.

```
List<Integer> list = List.of(1,2,3,4,5,6,7,8,9);
list.remove(1);
```

List.of()를 이용해 만든 list에서 값을 변경하려고 했기 때문에 발생했다.  
(Arrays.asList()를 이용해 만든 list에서도 같은 에러가 발생했을 것이다.)
 

### 💡 해결 방법
아래와 같이 new ArrayList<>()로 생성하면 해당 에러가 발생하지 않는다.

```
List<Integer> list = new ArrayList<>(List.of(1,2,3,4,5,6,7,8,9));
list.remove(1);
 ```

### 🤔 궁금한 점
그렇다면 List.of()로 생성한 List와 new ArrayList로 생성한 List가 무슨 차이가 있을까?  

먼저 List와 ArrayList의 차이점에 대해 주목할 필요가 있을 것 같다.  

List는 인터페이스고 ArrayList는 List 인터페이스를 구현한 클래스이다.  

다들 알다시피 List는 인터페이스이기 때문에 remove()와 같은 메소드가 구현되지 않았고 ArrayList나 LinkedList를 통해 메소드를 정의해야 사용할 수 있게 된다.  

#### List.of()
메소드를 한번 열어보자.
e1, e2, ... 등의 요소를 여러개 넣으면 ListN이라는 형태의 객체로 반환해준다.  


```
static <E> List<E> of(E e1, E e2, E e3) {
    return new ImmutableCollections.ListN<>(e1, e2, e3);
}

static <E> List<E> of(E e1, E e2, E e3, E e4) {
    return new ImmutableCollections.ListN<>(e1, e2, e3, e4);
}

...
```

ImmutableCollections.ListN<>()는 아래와 같다.
자세한 동작은 생략하고 메소드가 존재하는지만 확인해봤는데 remove() 같은 메소드를 지원하지 않는다.

```
static final class ListN<E> extends AbstractImmutableList<E> implements Serializable {
    static final List<?> EMPTY_LIST = new ListN<>();
    
    @Stable
    private final E[] elements;
    
    @SafeVarargs
    ListN(E... input) { ... }
    
    @Override
    public boolean isEmpty() { ... }
    
    @Override
    public int size() { ... }
    
    @Override
    public E get(int index) {... }
    
    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException { ...}
    
    private Object writeReplace() { ... }
}
```

결론은 List.of를 통해 생성된 List는 remove() 메소드를 지원하지 않았고,
나는 존재하지 않는 메소드를 호출하려고 하니 위와 같은 오류를 겪은 것이었다.


#### Arrays.asList()
해당 메소드를 살펴보면 아래와 같이 new ArrayList<>()로 생성해준다.  
그런데 왜 오류가 날까??   

```
@SafeVarargs
@SuppressWarnings("varargs")
public static <T> List<T> asList(T... a) {
    return new ArrayList<>(a);
}
```

원인은 import 부분을 살펴보면 알 수 있다.  
우리가 ArrayList를 사용할 때는 java.util.ArrayList 를 이용한다.  
하지만 Arrays.asList()에서 사용하는 ArrayList는 내부에 선언된 class를 이용한다.
 
Arrays 클래스의 일부

```
@SafeVarargs
@SuppressWarnings("varargs")
public static <T> List<T> asList(T... a) {
    return new ArrayList<>(a);
}

private static class ArrayList<E> extends AbstractList<E> implements RandomAccess, java.io.Serializable
{
    private static final long serialVersionUID = -2764017481108945198L;
    private final E[] a;

    ArrayList(E[] array) { ... }

    @Override
    public int size() { ... }

    @Override
    public Object[] toArray() { ... }

    @Override
    @SuppressWarnings("unchecked")
    public <T> T[] toArray(T[] a) { ... }

    @Override
    public E get(int index) { ... }

    @Override
    public E set(int index, E element) { ... }

    @Override
    public int indexOf(Object o) { ... }

    @Override
    public boolean contains(Object o) { ... }

    @Override
    public Spliterator<E> spliterator() { ... }

    @Override
    public void forEach(Consumer<? super E> action) { ... }

    @Override
    public void replaceAll(UnaryOperator<E> operator) { ... }

    @Override
    public void sort(Comparator<? super E> c) { ... }

    @Override
    public Iterator<E> iterator() { ... }
}

...
```

예상했겠지만 당연히 remove() 메소드에 관한건 없다.  
이로써 Arrays.asList()를 통해 생성된 List는 remove() 메소드를 지원하지 않는 것을 확인해보았다.  

***

### 참고

1. https://docs.oracle.com/javase/7/docs/api/java/lang/UnsupportedOperationException.html
2. https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html
3. https://docs.oracle.com/javase/8/docs/api/java/util/List.html
