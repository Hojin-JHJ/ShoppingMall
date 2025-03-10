## Chapter 2 : Spring Data JPA
* JPA(Java Persistence API) : 자바 ORM 기술에 대한 API 표준
  * ORM(Object Relational Mapping) : 객체와 관계형 DB를 매핑해주는 것<br/>
         -> 객체를 DB에 넣고 꺼내기 위해 반복적으로 SQL을 매핑할 필요 X<br/><br/>
  * 장점 : 특정 DB에 종속 X, 객체지향적 프로그래밍, 생산성 향상
  * 단점 : 복잡한 쿼리 처리, 성능 저하 위험, 학습 시간<br/><br/>
  
* JPA 동작 방식<br/>
![image](https://github.com/user-attachments/assets/66ea8958-3396-4b86-a37b-85cc26b28ac0)<br/>
  * 엔티티 : DB의 테이블에 대응되는 클래스<br/>
   @Entity 어노테이션이 붙은 클래스는 JPA에서 관리하는 엔티티<br/><br/>
   
  * 엔티티 매니저 팩토리 : 엔티티 매니저 인스턴스를 관리하는 주체<br/>
  애플리케이션 실행 시 한 개만 만들어지며 사용자로부터 요청이 오면 엔티티 매니저 생성<br/><br/>
  
  * 엔티티 매니저 : 영속성 컨텍스트에 접근해 엔티티에 대한 DB 작업 제공
    * find() 메소드 : 영속성 컨텍스트에서 엔티티를 검색하고 없을경우 DB에서 찾아 저장
    * persist() 메소드 : 엔티티를 영속성 컨텍스트에 저장
    * remove() 메소드 : 엔티티를 영속성 컨텍스트에서 삭제
    * flush() 메소드 : 영속성 컨텍스트에 저장된 내용을 DB에 반영<br/><br/>
    
  * 영속성 컨텍스트 : 엔티티를 영구 저장하는 환경<br/>
    애플리케이션과 DB사이의 중간계층 -> 버퍼링, 캐싱 등 가능
    ![image](https://github.com/user-attachments/assets/43bcbfd1-c4f4-492d-9ed8-0798b1d1c16e)<br/>
    * 1차 캐시 : Map<KEY, VALUE>로 저장
    * 장점
      * 동일성 보장 : 같은 트랜잭션에 같은 키값으로 find()시 같은 엔티티 조회 보장
      * 트랜잭션을 지원하는 쓰기 지연 : persist()시 1차 캐시에 저장과 동시에 쓰기 쓰기 지연 SQL 저장소에 SQL문 저장<br/>
      -> 트랜잭션을 커밋하는 시점에 flush() -> 성능에서 이점 (모아서 flush())
      * 변경 감지 : JPA가 1차 캐시에 DB에서 처음 불러온 엔티티의 스냅샷을 보유<br/>
      -> 1차 캐시와 스냅샷 비교 -> UPDATE SQL문을 쓰기 지연 SQL로 -> 커밋 시점에 DB 반영<br/><br/>
      
* 사용 DEPENDENCIES
  * Thymeleaf : 서버에서 가공한 데이터를 뷰에 보여주기 위한 템플릿 엔진
  * Spring Data JPA : JPA를 쉽게 구현하게 도와주는 모듈
  * MySQL Driver : MySQL 드라이버
  * H2 Database : 가볍고 빠른 DB, 디스크 기반 저장, 인메모리 DB 기능 -> 테스트용 데이터베이스
  * Lombok
  * Spring Web<br/><br/>
      
* MySQL 설정<br/>
  * 연결할 DB 설정<br/>
  ```
  spring.datasource.driver-class-name = com.mysql.cj.jdbc.Driver
  spring.datasource.url=jdbc:mysql://localhost:3306/shop?serverTimezone=UTC
  ```
  
  * username, password 입력<br/>
  ```
  spring.datasource.username=(username)
  spring.datasource.password=(password)
  ```
    
  * DB 초기화 전략 설정<br/>
  ```
  spring.jpa.hibernate.ddl-auto=(전략)
  ```
    * none : 사용 X
    * create : 기존 테이블 삭제 후 생성
    * create-drop : create + 종료 시점에 테이블 삭제
    * update : 변경된 스키마 적용
    * validate : 엔티티와 정상 매핑 확인<br/>
    *create, create-drop, update는 운영환경에서 절대 사용 X<br/><br/>
    
  * MySQL8Dialect 사용 선언<br/>
  ```
  spring.jap.database-platform=org.hibernate.dialect.MySQL8Dialect
  ```
    
  * 기타<br/>
 ```
 spring.jpa.properties.hibernate.show_sql=true : 실행되는 쿼리 콘솔 출력<br/>
 spring.jap.properties.hibernate.type.format_sql=true : 콘솔창에 출력되는 쿼리를 가독성 좋게 포맷팅<br/>
 logging.level.org.hibernate.type.descriptor.sql=trace : 쿼리에 물음표로 출력되는 바인드 파라미터 출력<br/><br/>
 ```
   
* Entity : 테이블에 대응하는 하나의 클래스<br/><br/>

* 엔티티 관련 어노테이션<br/>
  @Entity : 클래스를 엔티티로 선언<br/>
  @Table : 엔티티와 매핑할 테이블을 지정<br/>
  @Id : 테이블의 기본키에 사용할 속성을 지정<br/>
  @GeneratedValue : 키 값을 생성하는 전략 명시<br/>
  @Column : 필드와 컬럼 매핑<br/>
  @Lob : BLOB, CLOB 타입 매핑<br/>
  @CreationTimestamp : insert 시 시간 자동 저장<br/>
  @UpdateTimestamp : update 시 시간 자동 저장<br/>
  @Enumerated : enum 타입 매핑<br/>
  @Transient : 해당 필드 데이터베이스 매핑 무시<br/>
  @Temporal : 날짜 타입 매핑<br/>
  @CreateDate : 엔티티가 생성되어 저장될 때 시간 자동 저장<br/>
  @LastModifiedDate : 조회한 엔티티의 값을 변경할 때 시간 자동 저장<br/><br/>

* @Column 속성<br/>
name : 필드와 매핑할 컬럼의 이름 설정<br/>
unique(DDL) : 유니크 제약 조건 설정<br/>
insertable : insert 가능 여부<br/>
updatable : update 가능 여부<br/>
length : String 타입의 문자 길이 제약조건 설정<br/>
nullable(DDL) : null 값의 허용 여부 설정<br/>
columnDefinition : DB 컬럼 정보 직접 기술<br/>
precision/scale(DDL) : 소수점을 포함한 전체 자리수/소수점 자리수(BigDecimal)<br/><br/>

* @GeneratedValue 속성<br/>
GenerationType.AUTO(defailt) : JPA 구현체가 자동으로 생성 전략 결정<br/>
GenerationType.IDENTITY : 기본키 생성을 DB에 위임<br/>
GenerationType.SEQUENCE : 데이터 베이스 시퀀스 오브젝트를 이용한 기본키 생성(@SequenceGenerator 필요)<br/>
GenerationType.TABLE : 키 생성용 테이블 사용(@TableGeneratror 필요)<br/><br/>

* Repository : Entity에 의해 생성된 DB에 접근하는 메소드들을 사용하기 위한 인터페이스<br/><br/>

* JpaRepository에서 지원하는 메소드<br/>
&#60;S extends T> save(S entity) : 엔티티 저장 및 수정<br/>
void delete(T entity) : 엔티티 삭제<br/>
count() : 엔티티 총 개수 반환<br/>
Iterable<T> findAll() : 모든 엔티티 조회<br/><br/>

* Repository를 사용하기 위해선 Bean 주입 필요 -> @Autowired 어노테이션<br/>
```
@Autowired
ItemRepository itemRepository
```

* 쿼리 메소드 : find(엔티티 이름)By변수이름<br/>
  ex)
  ```
  List<Item> findByItemNm(String itemNm); (엔티티 이름 생략 가능)
  ```
  * And, Or, Is, Equals, Not, True, False
  * Between, LessThan, LessThanEqual, GreaterThan, GreaterThanEqual
  * After, Before (날짜)
  * IsNull, Null, IsNotNull, NotNull
  * Like, NotLike
  * StartingWith, EndingWith, Containing
  * OrderBy<br/><br/>
Repository에 메소드 생성 -> 코드에 사용<br/><br/>
 
* @Query 어노테이션 : JPQL을 통해 복잡한 쿼리 처리 가능<br/>
  ex)
  ```
  @Query("select i from Item i where i.itemDetail like %:itemDetail% order by i.price desc")
  List<Item> findByItemDetail(@Param("itemDetail") String itemDetail);
  ```
  * 테이블이 아닌 엔티티를 대상으로 쿼리 수행(seelct i : Item 이라는 객체를 선택)<br/>
    -> 특정 DB SQL에 의존 X
  * itemDetail 이라는 파라미터를 :itemDetail로 받아 사용<br/><br/>
  
  * nativeQuery 속성 : 기존 DB의 쿼리를 그대로 사용 -> 특정 DB에 종속
    ex)
    ```
    @Query(value = "select * from item i where i.item_detail like %:itemDetail% order by i.price desc", nativeQuery = true)
    List<Item> findByItemDetailNative(@Param("itemDetail") String itemDetail);
    ```
    <br/><br/>
    
*Querydsl : JPQL을 코드로 작성할 수 있도록 도와주는 빌더 API 
  * 장점
    * 고정된 SQL문이 아닌 조건에 맞게 동적으로 쿼리 생성
    * 비슷한 쿼리 재사용 가능, 제약 조건 조립 및 가독성 향상
    * 컴파일 시점에 오류 발견 가능
    * IDE의 도움을 받아 자동 완성 기능 사용 가능 -> 생산성 향상
    <br/><br/>
  * 필요 설정
    ```
    <dependency>
            <groupId>com.querydsl</groupId>
            <artifactId>querydsl-jpa</artifactId>
            <version>5.0.0</version>
            <classifier>jakarta</classifier>
    </dependency>
    <dependency>
            <groupId>com.querydsl</groupId>
            <artifactId>querydsl-apt</artifactId>
            <version>5.0.0</version>
            <classifier>jakarta</classifier>
    </dependency>
    <dependency>
            <groupId>com.querydsl</groupId>
            <artifactId>querydsl-core</artifactId>
            <version>5.0.0</version>
    </dependency>

    <plugin>
             <groupId>com.mysema.maven</groupId>
             <artifactId>apt-maven-plugin</artifactId>
             <version>1.1.3</version>
             <executions>
                 <execution>
                     <goals>
                        <goal>process</goal>
                     </goals>
                     <configuration>
                         <outputDirectory>target/generated-sources/java</outputDirectory>
                         <processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
                     </configuration>
                  </execution>
              </executions>
    </plugin>

    ```
    (교재와 변경점 : 버전 변경, querydsl-core 추가, jakarta로 분류 명시)






