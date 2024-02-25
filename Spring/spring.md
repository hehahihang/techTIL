#Spring

## @RequestBody, @ResponseBody
1) RequestBody 동작
  - @RequestBody를 처리할 수 있는, resolver를 가져온다(RequestResponseBodyMethodProcessor)
  - 해당 Resolver에 등록되어 있는 Converter 중 MappingJackson2HttpMessageConverter 에서 body 정보를 생성한다
    - 생성 시 ObjectMapper 활용
  - 리플렉션을 통해 가져온 body값을 controller의 파라미터에 invoke 해주면서 데이터가 dto에 binding 된다.

## DataSourceConfig 구성하기
### 2개 이상의 데이터베이스에 연결하는 요구사항을 만족하기 위해 빈네임과 프로퍼티를 적절히 등록해야 함
### DataSource, DataProperties, SqlSessionFactory, SqlSessionTemplate 빈을 별도로 생성하는 작업이 필요하다.

1) DatasourceProperties
  - DataSourceProperties 클래스에 의해 연결을 원하는 데이터베이스 정보를 매핑한다.
    - .yml / .properties
  - @ConfigurationProperties 를 사용해서 접두어(prefix = path)를 지정한다

2) DataSource
  - Conncection Pool을 구현하기 위한 스펙을 정해 놓은 인터페이스

3) SqlSessionFactory
  - Mybatis에서 데이터베이스의 연결과 SQL실행에 대한 객체
  - DataSource 를 참조하여 Mybatis와 MySql 서버를 연동시켜준다.
  - SqlSessionFactory를 생성해주는 SqlSessionFactoryBean 객체를 먼저 설정하여야 한다.

4) SqlSessionTemplate
  - Mybatis 쿼리문을 수행하는 역할

<img width="933" alt="image" src="https://github.com/hehahihang/techTIL/assets/57223501/35e21a1a-8afd-4b17-a697-0d736f053f3f">


## Hikari CP
- Hikari CP란? 
    - 데이터베이스 연결(Connection)을 관리해주는 라이브러리
    - 커넥션 풀(Connection Pool)이 설정된 커넥션 사이즈만큼의 연을 혀용하며, HTTP요청에 대해 순차적으로 DB커넥션을 처리하는 기능 수행
 
### Spring Connection Pool
- Java 에서는 기본적으로 DataSource 인터페이스를 사용하여 커넥션풀 관리

### DBCP(Database Connection Pool)
- 최초 생성해둔 커넥션 풀에서 생긴 연결들로 요청을 처리하고, 이를 재사용함

* DBCP를 사용하는 이유?
  * JDBC 연결은 드라이버를 로드하고 연결하여 객체를 받아오는 과정을 수행한다.
  * Client 요청마다 위 과정을 반복하여 속도와 자원소모의 단점

* DBCP 과정
1) WAS를 실행하며 Pool 내에 Connection들을 생성
2) HTTP 요청이 올 때, Pool 내 Connection 객체를 가져다가 사용
3) 사용이 완료된 객체는 Pool에 반환

* DBCP 장점
1. WAS와 DB사이의 연결을 정해둔 만큼만 미리하여, Connection 생성 비용 감소
  - Connection을 크게하면? -> 메모리 소모량 증가, 대기시간 감소
  - Connection을 작게하면? -> 대기시간 증가

* DeadLock
- 커넥션 풀 사이즈를 지정할 때는 항상 데드락을 고려해야 함
  Poolsize = Tn x (Cm-1) + 1 (최소)
  Poolsize = Tn x (Cm-1) + (Tn/2) (여유)
  - Tn : 전체 쓰레드 개수
  - Cm : 하나의 Task에서 동시에 필요한 Connection의 수













