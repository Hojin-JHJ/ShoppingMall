## Chapter 1 : 개발 환경 구축
* 설정 파일(application.properties)
  * server.port = 80 : 포트 설정(기본 : 8080)<br/><br/>
* 함께 해봐요 1-2 : Hello World 출력하기
  * @RestController
    * @Controller + @ResponseBody
    * @Controller : 클래스를 요청을 처리하는 컨트롤러로 사용
    * @ResponseBody : 객체를 HTTP 응답 본문의 객체로 변환해 전송 -> html 파일 없이 웹 브라우저에 출력 가능<br/><br/>
  * @GetMapping(value = "/")
    * localhost:8080/ 로 요청이 들어오면 아래의 함수 실행<br/><br/>
* Lombok 라이브러리
  * 반복적인 자바 코드를 컴파일할 때 자동으로 생성

| 어노테이션               | 설명                                                                  |
|--------------------------|-----------------------------------------------------------------------|
| @Getter / @Setter         | 속성들에 대한 Getter/Setter 메소드 생성                               |
| @ToString                | toString() 메소드 생성                                               |
| @NonNull                 | 변수 null 체크, NullPointerException 예외 발생                        |
| @EqualsAndHashCode       | equals(), hashCode() 메소드 생성                                      |
| @Builder                 | 빌더 패턴을 이용한 객체 생성                                          |
| @NoArgsConstructor       | 파라미터(매개변수)가 없는 기본 생성자 생성                            |
| @AllArgsConstructor      | 모든 속성에 대한 생성자 생성                                          |
| @RequiredArgsConstructor | 초기화되지 않은 Final, @NonNull 어노테이션이 붙은 필드에 대한 생성자 생성      |
| @Log                     | log 변수 자동 생성                                                   |
| @Value                   | 불변 클래스 생성                                                     |
| @Data                    | @ToString, @EqualsAndHashCode,<br/> @Getter, @Setter, @RequiredArgsConstructor를 합친 어노테이션 |<br/><br/>

* MySQL로 shop 데이터베이스 생성
  * create database shop default character set utf8mb4 collate utf8mb4_general_ci;
  * (교재 : create database shop default character set utf8 collate utf8_general_ci;(MySQL 버전 차이))
  * utf8 : 가변 3바이트 사용, utf8mb4 : 4바이트 사용(이모지 사용 가능)
