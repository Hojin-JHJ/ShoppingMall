## Chapter 2 : Spring Data JPA
* JPA(Java Persistence API) : 자바 ORM 기술에 대한 API 표준
  * ORM(Object Relational Mapping) : 객체와 관계형 DB를 매핑해주는 것<br/>
         -> 객체를 DB에 넣고 꺼내기 위해 반복적으로 SQL을 매핑할 필요 X<br/><br/>
  * 장점 : 특정 DB에 종속 X, 객체지향적 프로그래밍, 생산성 향상
  * 단점 : 복잡한 쿼리 처리, 성능 저하 위험, 학습 시간<br/><br/>
* JPA 동작 방식
![image](https://github.com/user-attachments/assets/27bc41b0-6300-4612-8030-409725a368ef)<br/>
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
    ![image](https://github.com/user-attachments/assets/a0e6aeea-aaa2-464c-8453-e9d7e0e7319b)<br/>
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
  ![image](https://github.com/user-attachments/assets/f1c3e815-8e25-4a0c-9b4e-0e2217b88dd2)<br/>
  * username, password 입력<br/>
    ![image](https://github.com/user-attachments/assets/0a78813c-576a-447a-bf93-065b87e2bb37)<br/>
  * DB 초기화 전략 설정<br/>
    ![image](https://github.com/user-attachments/assets/cbec0018-3df6-46f9-9902-a6fa24d2b7c0)<br/>
    * none : 사용 X
    * create : 기존 테이블 삭제 후 생성
    * create-drop : create + 종료 시점에 테이블 삭제
    * update : 변경된 스키마 적용
    * validate : 엔티티와 정상 매핑 확인<br/>
    *create, create-drop, update는 운영환경에서 절대 사용 X<br/><br/>
  * MySQL8Dialect 사용 선언<br/>
  ![image](https://github.com/user-attachments/assets/0bb351b8-6e29-4b56-8b05-08b33144b896)<br/>
  * 기타<br/>
  ![image](https://github.com/user-attachments/assets/80db74d8-bfb6-4d44-8c23-0c796e764604)<br/>
* 엔티티 관련 어노테이션<br/>
  ![image](https://github.com/user-attachments/assets/a3d4a399-a26e-4338-b9c4-37a4297474b5)<br/><br/>
* @Column 속성<br/>
  ![image](https://github.com/user-attachments/assets/5e333958-996d-4e42-9698-ea2752a36bbb)<br/><br/>
* @GeneratedValue 속성<br/>
  ![image](https://github.com/user-attachments/assets/f6644288-be62-479b-9d1f-7120047f3960)<br/><br/>





  
