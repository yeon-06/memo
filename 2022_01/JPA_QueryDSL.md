[어제 TIL](./JPA_query_method.md)에서 확인했다시피 JPA는 다양한 방법으로 쿼리를 지원해준다.  
그럼에도 불구하고 직접 쿼리를 작성해야 하는 일이 생기는데 이때 `@Query`를 이용해 편리하게 쿼리를 작성할 수 있다.

```java
@Query("select u from User u where u.id = :id and u.deleteYn = 'N'")
Optional<User> findByUserId(@Param("id") Long id);
```

하지만 위 방식은 내가 작성한 쿼리문이 문법적인 오류를 포함하는지 따로 검사하지는 않는다.  
직접 **실행해본 후에야 내가 작성한 쿼리가 잘 돌아가는지 확인**할 수 있다.  
이런 문제를 덜 발생시키기 위해 **QueryDSL**라는 프레임워크가 생겨났다.

QueryDSL을 사용하면 좋은 점
1. 동적 쿼리 생성 가능
2. IDE의 자동 완성 지원
3. 컴파일 시점에 쿼리의 오류 발견 가능
4. 쿼리 작성 후 재사용 가능

직접 설정하는 방법에 대해서는 이후 프로젝트에 적용하면서 블로그에 정리하겠다.  
이 글에서는 일단 사용하는 방법에 대해 기술해보려 한다.

build.gradle 설정
```
buildscript {
    ext {
        queryDslVersion = "4.4.0"
    }
}
dependencies {
    ...
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
    annotationProcessor(
            "javax.persistence:javax.persistence-api",
            "javax.annotation:javax.annotation-api",
            "com.querydsl:querydsl-apt:${queryDslVersion}:jpa")
    ...
}
```

정상적으로 build 됐다면 각 Entity에 대해 Q엔티티명이라는 클래스가 생성됐을 것이다.  
해당 클래스를 이용해 아래와 같이 간단히 쿼리문을 작성할 수 있다.

예제
```
JPAQuery<User> query;
...
QUser user = new QUser("test");
List<User> posts = query.from(user)
        .where(user.deleteYn.eq('N'))
        .orderBy(user.id.desc())
        .fetchOne();
```


언뜻 보면 사용 방법을 알아야한다는 면에서 더 불편하지 않을까? 의문이 들 수 있다.  
하지만 QueryDSL은 동적 쿼리를 걸거나 

***
참고
1. https://tecoble.techcourse.co.kr/post/2021-08-08-basic-querydsl/
2. https://www.baeldung.com/intro-to-querydsl