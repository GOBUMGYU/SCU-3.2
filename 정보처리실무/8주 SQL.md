# SQL 
## SQL의 종류

### DDL(데이터 정의어)

- DB를 구축하거나 수정할 목적으로 사용하는 언어
- 수행 결과가 데이터사전(DD)이라는 특별한 파일에 여러 개의 테이블로 저장됨
- **CREATE**
    - SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 정의함
- **ALTER**
    - TABLE에 대한 정의를 변경할 때 사용함
- **DROP**
    - SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 삭제함

**DDL의 3가지 유형** 

- **CREATE SCHEMA**
    - 스키마(개체, 속성, 관계 , 제약조건 등)을 정의하는 명령문
    - CREATE SCHEMA 스키마이름 AUTHORIZATION 사용자이름;
- **CREATE DOMAIN**
    - 도메인(속성이 가질 수 있는 유형의 범위)를 정의하는 명령문
    - CREATE DOMAIN 도메인이름 [AS] 데이터타입 [DEFAULT 기본값] [CONSTRAINT 제약조건명 CHECK 범위];
    - 예) CREATE DOMAIN 성별 VARCHAR(1) DEFAULT ‘남’ CONSTRAINT 성별체크 CHECK(VALUE IN(’남’, ‘여’));
- **CREATE TABLE**
    - CREATE TABLE 테이블이름 [속성이름 데이터타입 [DEFAULT 기본값] [NOT NULL], …
    - [,PRIMARY KEY(속성명)] PRIMARY KEY
    - [,UNIQUE KEY(속성명)] UNIQUE KEY
    - [,FOREIGN KEY(속성명)] FOREIGN KEY [REFERENCES 참조테이블(속성명)]
    - [ON DELETE옵션] [ON UPDATE옵션]
        - FOREIGN KEY : 외래키로 사용할 속성을 지정하고 이하 해당 참조 테이블의 속성 값이 삭제, 변경된 경우 취해야 할 옵션들 설정
    - [,CONSTRAINT 제약조건명] [CHECK 조건식]);
- **CREATE VIEW**
    - 뷰(가상 테이블)을 정의하는 명령문
    - CREATE VIEW 뷰이름(속성이름, …) AS SELECT문;
    - 예 ) CREATE VIEW 고객명단(이름, 주소) AS SELECT 이름, 주소 FROM 고객 WHERE 주소=’서울시’;
- **CREATE INDEX**
    - 인덱스(보조적인 순번)을 정의하는 명령문
    - CREATE INDEX 인덱스이름 ON 테이블이름 (속성이름 [ ASC | DESC ], …);
    - 예 ) CREATE INDEX 고객번호 ON 고객(고객번호 DESC);
- **ALTER TABLE**
    - 테이블에 대한 정의를 변경하는 명령문
    - ALTER TABLE 테이블이름 ADD 속성이름 데이터타입 [DEFAULT ‘기본값’]; 새로운 열의 추가
    - ALTER TABLE 테이블이름 ALTER 속성이름 [SET DEFUALT ‘기본값’]; 특정 속성의 변경
    - 예) ALTER TABLE 학생 ALTER 학번 VARCHAR(10) NOT NULL;
- **DROP**
    - 스키마, 도메인, 테이블, 뷰, 인덱스, 제약조건 등을 제거하는 명령문
    - DROP SCHEMA 스키마이름 [CASCADE | RESTRICT];
        - CASCADE : 참조하는 다른 모든 개체가 함께 제거됨
    - DROP DOMAIN 도메인이름 [CASCADE | RESTRICT];
        - RESTRICT : 참조하는 개체가 있는 경우 제거를 취소
    - DROP TABLE 테이블이름 [CASCADE | RESTRICT];
    - DROP VIEW 뷰이름 [CASCADE | RESTRICT];
    - DROP INDEX 인덱스이름 [CASCADE | RESTRICT];
    - DROP CONSTRAINT 제약조건이름;

### DCL

- 데이터 보안, 무결성, 회복, 병행 제어 등을 정의하는데 사용되는 언어
- DBA(데이베이스 관리자)가 데이터 관리를 목적으로 사용
- DCL의 종류
    - **COMMIT**
        - 명령으로 수행된 결과를 실제 물리적 디스크로 저장하고 조작 작업이 정상적으로 완료되었음을 알려줌
    - **ROLLBACK**
        - 데이터베이스 조작 작업이 비정상적으로 종료되었을 때 원래의 상태로 복구함
    - **GRANT**
        - 데이터베이스 사용자에게 사용 권한을 부여함
    - **REVOKE**
        - 데이터베이스 사용자의 사용 권한을 취소함

**사용자 등급 지정 및 해제**

 **CONNECT**

- 단순 사용자
- **GRANT**
    - GRANT 사용자 등급 TO 사용자 [ IDENTIFIED BY 암호 ];
    - REVOKE 사용자등급 FROM 사용자;
    - 예)  GRANT RESOURCE TO YOUNG;
    - 사용자 ID가 YOUNG인 사람에게 데이터베이스 생성 권한을 부여
    - GRANT 권한 ON 개체 TO 사용자 [WITH GRANT OPTION];
    - 권한의 종류 : ALL, SELECT, INSERT, DELETE, UPDATE, ALTER 등
- **REVOKE**
    - REVOKE

### DML

- 저장된 데이터를 실질적으로 관리하는데 사용되는 언어
- SELECT - 테이블에서 튜플을 검색
- INSERT - 테이블에서 새로운 튜플을 삽입
- DELETE - 테이블에서 튜플을 삭제
- UPDATE - 테이블에서 튜플의 내용을 갱신

### SELECT문 조건

**집합연산** 

- UNION  - 두 SELECT문의 조회 결과를 통합하여 모두 출력, 중복된 행은 한번만 출력(합집합)
- UNION ALL - 두 SELECT문의 조회 결과를 통합하여 모두 출력, 중복된 행도 그대로 출력(합집합)
- INTERSECT(두 SELECT문의 조회 결과 중 공통된 행만 출력 (교집합)
- EXCEPT - 첫번째 SELECT문의 조회 결과에서 두 번째  SELECT 문의 조회 결과를 제외한 행을 출력 (차집합)

## SQL 관련 개념 정리

### DBMS 접속

응용 시스템을 이용하여 DBMS에 접근하는 것 

- 응용 시스템은 사용자로부터 매개변수를 전달받아 SQL을 실행하고 DBMS로부터 전달받은 결괄르 사용자에게 전달하는 매개체 역활을 수행
- 웹 응용 프로그램은 웹 응용 시스템(웹서버, WAS)를 통해 DBMS에 접근

**DBSM접속기술이란?**

DBMS에 접근하기 위해 사용하는 API 또는 API의 사용을 편리하게 도와주는 프레임워크

JDBC(JAVA DATABASE CONNECTIVITY)

- 자바 언어로 데이터베이스에 접속할 때 사용하는 표준 API
- 접속대상 DBMS에 대한 드라이버 필요

ODBC(OPEN DATABASE OCNNECTIVITY)

- 언어와 상관없이 데이터베이스에 접근하기 위한 표준 API

MYBATIS

- SQL MAPPING 기반 오픈 소스 접속 프레임워크
- SQL 문장을 분리하여 XML파일을 만들어 사용

**동적 SQL(Dynamic SQL)이란?**

조건에 따라 SQL구문을 동적으로 변경하여 처리할 수 있는 SQL처리 방식

- 사용자로부터 SQL의 일부 또는 전부를 입력 받아 실행할 수 있음
- 정적 SQL에 비해 속도는 느리지만 상황에 따라 다양한 조건을 첨가하는 등 유연한 개발이 가능함

### SQL 테스트

SQL이 작성 의도에 맞게 원하는 기능을 수행하는지 검증하는 과정

- 단문 SQL
    - 코드를 직접 실행한 후 결과를 확인하는 것으로 간단히 테스트가 가능함
- 단문 SQL 테스트
    - DDL, DML, DCL이 포함되어 있는 SQL과 TCL을 테스트 하는 것으로 직접 실행하여 결과물을 확인함 TCL(Transaction Control Language)은 Commit등이 있음
    - DDL로 작성된 개체 : DESCRIBE 명령어를 이용하여 속성, 자료형, 옵션 등을 확인할 수 있음
    - DML로 변경된 데이터 : SELECT문으로 데이터의 정상적인 변경 여부를 확인할 수 있음
    - DCL로 설정된 사용자 권한 : 사용자 권한 정보가 저장된 테이블을 조회하여 확인할 수 있음
- 절차형 SQL
    - 테스트 전에 생성을 통한 구문 오류나 참조 오류의 존재여부를 확인할 수 있음
- 절차형 SQL 테스트
    - 프로시저, 사용자 정의 함수, 트리거 등의 절차형 SQL은 디버깅을 통해 적합성 여부를 검증하고 실행을 통해 결과를 확인함
    - 오류 및 경고 메시지가 상세히 출력되지 않아 SHOW 명령어를 통해 오류 내용을 확인해야 함
    - 예 ) SHOW ERRORS;
    - 데이터베이스에 변화를 줄 수 있는 SQL문은 주석으로 처리하고 출력문을 이용하여 확인함
    - 디버깅이 완료되면 출력문을 삭제하고 주석 기호를 삭제한 후 절차형 SQL을 실행하여 결과를 검토함

### ORM

객체지향 프로그래밍의 객체와 관계형 데이터베이스의 데이터를 연결하는 기술

- 객체지향 프로그래밍에서 사용할 수 있는 가상의 객체지향 데이터베이스를 만들어 프로그래밍 코드와 데이터를 연결함
- 생성된 가상의 객체지향 데이터베이스는 프로그래밍 코드 또는 데이터베이스와 독립되어 있어 재사용 및 유지보수가 용이

**ORM 프레임워크란?**

ORM을 구현하기 위한 구조와 구현을 위해 필요한 여러 기능들을 제공하는 소프트웨어를 의미

ORM 프레임워크의 종류

- JAVA : JPA, Hibernate, EclipseLink, DataNucleus, Ebean 등
- C++ : ODB, QxOrm 등
- PYTHON : Django, SQLAlchemy, Storm등
- .NET : Nhibernate , DatabaseObjects , Dapper 등
- PHP : doctrine, Propel, RedBean

**ORM의 한계**

- 프레임워크가 자동으로 SQL을 작성하기 때문에 의도대로 SQL이 작성되었는지를 확인해 봐야 함
- 객체지향적인 사용을 고려하여 설계된 데이터베이스가 아닌 경우 프로젝트가 거대해질수록 ORM기술을 적용하기 어려움
- ORM을 고려하지 않은 데이터베이스를 ORM에 적합하게 변환하려면 많은 시간과 노력이 필요함

### 쿼리 성능 최적화

데이터 입/출력 애플리케이션의 성능 향상을 위해 SQL코드를 최적화하는 것

- APM(Application Performance Management/Monitoring) 도구를 사용하여 최적화 할 쿼리를 선정함
- 최적화 대상 쿼리에 대해 옵티마이저가 수립한 실행 계획을 검토하고 SQL코드와 인덱스를 재구성함

**옵티마이저란?**

작성된 SQL이 효율적으로 수행되도록 최적의 경로를 찾아주는 모듈

옵티마이저는 두 종류가 있음

- RBO(Rule Based Optimizer)
    - 데이터베이스 관리자가 사전에 정의해둔 규칙에 따라 경로를 검색
    - 성능 기준은 개발자의 SQL 숙련도임
    - 실행 계획 예측이 쉬움
    - 개발자의 규칙 이해도, 규칙의 효율성 등을 고려해야 함
- CBO(Cost Based Optimizer)
    - 입/출력 속도, CPU 사용량, 블록 개수, 개체의 속성, 튜플 개수 등을 종합하여 최적의 경로를 검색
    - 성능 기준은 옵티마이저의 예측 성능임
    - 예측이 복잡함
    - 비용 산출 공식의 정확성을 고려해야 함
    

**실행계획**

DBMS의 옵티마이저가 수립한 SQL코드의 실행 절차와 방법

- 실행 계획은 EXPLAIN 명령어를 통해 확인이 가능함
- 실행 계획에는 요구사항들을 처리하기 위한 연산 순서가 적혀 있음

**쿼리 성능 최적화 방법**

- SQL코드 재구성 방법
    - WHERE절 추가 또는 WHERE절에 연산자 사용 제한 등
- 인덱스 재구성 방법
    - 조회되는 속성과 조건을 고려하여 인덱스 구성
    - 인덱스 추가 및 기존 인덱스 열 순서 변경
    - IOT(index-Organized Table) 구성 고려
    - 불필요한 인덱스 제거
