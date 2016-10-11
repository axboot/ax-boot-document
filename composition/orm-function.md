## 다양한 형태의 데이터 영속화 기능 제공

- ORM : JPA(Hibernate) 기반의 ORM을 SpringDataJPA기반으로 제공합니다. 스키마 추출 도구를 사용할 경우 JPA를 통해 데이터를 영속화 할 수 있는 Repository가 자동 생성됩니다. 해당 Repository는 조회, 저장, 삭제, 페이징, QueryDSL등 SpringDataJPA와 QueryDSL이 제공하는 기능들을 별도의 확장 없이 사용할 수 있습니다. 

- QueryDSL : 복잡도가 높은 쿼리의 경우 QueryDSL을 통해서 TypeSafe한 쿼리를 생성할 수 있습니다.

- SQLMapper : 고전적인 방식의 SQL Mapper또한 제공합니다. MyBatis와 Groovy 기반의 쿼리 문자열과 JdbcTemplate을 조합하여 사용할 수 있는 2가지 방식을 제공합니다.
    - MyBatis : MyBatis
    - Groovy Multiline String + JdbcTemplate