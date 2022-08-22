*`@Column*(nullable = false)`

컬럼 값이고 반드시 값이 존재해야 함을 나타냅니다.

Entity(테이블) 임을 만들었다면

컬럼(열) 이라는 것을 나타내는 것

```sql
//생성
CREATE TABLE IF NOT EXISTS courses ( // courses이란 CREATE TABLE 테이블 만들어라 IF NOT EXISTS 만약 존재를 안하면 
    id bigint NOT NULL AUTO_INCREMENT, // NOT NULL id를 반드시 가지고 있어야 한다. bigint(java:Long과 같다) 정수
		// AUTO_INCREMENT 자동으로 증가해라 라는 뜻
    title varchar(255) NOT NULL, // varchar(255) 문자열 (String 과 비슷)
    tutor varchar(255) NOT NULL, // 
    PRIMARY KEY (id) // id라는 값은 행(데이터)을 구분해주는 유일한 값, id가 아니라 title로 들어 갈 수 있는데 중복되면안되서 고유값을 할 수 있는 id로
);

--------------------------------------------------------
bigint , varchar(255) -> Long String
NOT NULL -> (nullable = false)

title varchar(255) NOT NULL, -> 이렇게 한줄 한줄의 열을 Column 으로 표시

PRIMARY KEY (id) ->  @Id // ID 값, Primary Key로 사용하겠다는 뜻입니다.
									 
AUTO_INCREMENT, -> @GeneratedValue(strategy = GenerationType.AUTO)

@Entity// 테이블임을 나타냅니다.
public class Course {

    @Id // ID 값, Primary Key로 사용하겠다는 뜻입니다.
    @GeneratedValue(strategy = GenerationType.AUTO) // 자동 증가 명령입니다.
    private Long id;

    @Column(nullable = false) // 컬럼 값이고 반드시 값이 존재해야 함을 나타냅니다.
    private String title;

    @Column(nullable = false)
    private String tutor;
```

```sql
컬럼(column)과 필드(field) 무엇이 다를까?

칼럼(column)과 필드(field)는 주로 행을 뜻하는 용어로, 
백 엔더들은 주로 혼용해서 쓴다고 알고 있었다.
정확한 차이가 무엇인지 구글링을 해보고 알게 되었다.
레코드, 필드는 파일 시스템상에서 표현되는 용어라고 한다.
실무에서는 어떤 걸 써도 크게 상관은 없을 것 같지만 차이는 알아두면 좋을 것 같다.
```
![](C:/Users/User/Desktop/Untitled.png)