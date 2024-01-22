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







