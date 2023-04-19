### org.hibernate.tool.schema.spi.SchemaManagementException: Schema-validation: missing table [name]

hibernate에는 ddl-auto 옵션을 통해 여러가지 기능을 부여할 수 있다.

* create: 기존테이블 삭제 후 다시 생성
* create-drop: 테이블 생성 + 종료 시 삭제
* update: 반영
* validate: 엔티티와 테이블이 정상 매핑되었는지 확인
* none: 미사용

여기서 validate 설정을 한 경우 엔티티와 테이블이 정상 매핑되었는지 확인한다.  
만약 정상 매핑되지 않았다면 제목과 같은 에러가 발생한다.
