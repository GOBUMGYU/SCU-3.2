# SQL일반

# SQL정의

### SQL(Structured Query Language)

구조화 질의어, 관계형 데이터베이스 관리 시스템의 데이터를 관리하기 위하여 설계된 특수 목적의 프로그래밍 언어

### ISO/IEC9075

국제 표준화 기구(ISO)와 미국 표준 협회(ANSI)에서 통합/개정한 것 SQL에 대한 국제 표준으로 활용되고 있음

## SQL 관련 용어 정리

### 테이블

단일 주제에 관해 행과 열로 구성되는 정보 모음

- 설계단계 - 릴레이션
- 조작/검색 시 - 테이블

### 튜플(row)

특정 인스턴스에 관한 정보들의 모임

### 속성(Column)

어떤 개체를 표현하고 저장하기 위한 속성

한 릴레이션에 들어 있는 속성의 수를(’차수’)라고 함

### 릴레이션 인스턴스

데이터 개체를 구성하고 있는 속성들에 데이터 타입이 정의되어 구체적인 값을 가지고 있는 것

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/204d8f58-9156-45d0-8c8a-980c6aff89f7/Untitled.png)

# DDL 개요

### DDL(DATA Define Language, 데이터 정의어)

DB의 구조, 데이터 형식, 접근 방식 등을 DB를 구축하거나 수정할 목적으로 사용하는언어 DDL의 결과는 데이터 사전(Data Dictionary)라는 특별한 파일에 여러 개의 테이블로 저장됨

## DDL의 유형

### CREATE

SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 정의

<aside>
💡 CREATE SCHEMA - 스키마를 정의하는 명령문

- CREATE SCHEMA 스키마이름 QUTHORIZATION 사용자명;
- CREATE SCHEMA 학교 AUTHORIZATION 홍길동;
    - 소유권자의 ID가 홍길동인 스키마  학교를 정의하는 명령문
</aside>

<aside>
💡 CREATE DOMAIN - 도메인을 정의하는 명령문

- CREATE DOMAIN 도메인이름 데이터타입 [DEFAULT 기본값] [CONSTRAINT 제약조건명 CHECK(범위값)];
- CREATE DOMAIN GRADE CHAR(1) [DEFAULT ’B’] [CONSTRAINT TEST CHECK(VALUE IN(’A’,’B’))];
    - 정의된 도메인의 이름이 GRADE이고 문자를 1개 가질 수 있는 데이터 타입
    - 도메인 GRADE가 지정된 속성값은 기본값으로 ‘B’를 가진다.
    - 해당 도메인으로 지정한 속성에는 ‘A’,’B’ 둘중 하나의 값만을 저장할 수 있음
</aside>

<aside>
💡 CREATE TABLE - 테이블을 정의하는 명령문

- CREATE TABLE 테이블이름 (속성이름 데이터타입 [DEFAULT 기본값] [NOT NULL] [기타 추가 참조속성]…);
- 테이블의 추가 참조 속성
    - PRIMARY KEY
        - 기본키로 사용할 속성 지정, 중복 X
        - NULL일 수 없음
    - UNIQUE
        - 대체키로 사용할 속성을 지정
        - 중복된 값을 가질 수 없음
    - FOREIGN KEY ~ REFERENCES ~
        - 외래키로 사용할 속성을 지정
            - ON DELETE
                - 참조 테이브이 튜플이 삭제되었을 때 기본 테이블에 취해야 할 사항을 지정
            - ON UPDATE
                - 참조 테이블의 참조 속성 값이 변경되었을 때 기본 테이블에 취해야 할 사항을 지정
    - CREATE TABLE 학생 (이름 VARCHAR(15) NOT NULL, 학번 CHAR(8), 전공 CHAR(5), 생년월일 DATE, PRIMARY KEY(전공) REFERENCES 학과(학과코드) ONDELETE SET NULL);
</aside>

<aside>
💡 CREATE VIEW - 뷰를 정의하는 명령문

- 하나 이상의 기본 테이블로부터 유도되는 가상 테이블 실제로는 데이터가 저장되는 것은 아님
- CREATE VIEW 뷰이름[속성이름, …] AS SELECT문;
- CREATE VIEW 서울고객(성명,전화번호) AS SELECT 성명,전화번호 FROM 고객 WHERE 주소 = ‘서울시’;
    - 고객 테이블에서 주소가 서울시인 고객들의 성명과 전화번호를 서울고객이라는 이름의 뷰로 정의
</aside>

<aside>
💡 CREATE INDEX - 인덱스를 정의하는 명령문

- 검색 시간을 단축시키기 위해 만든 보조적인 데이터구조
- CREATE [UNIQUE] INDEX 인덱스이름 ON 테이블이름 [속성명 ASC | DESC)];
- CREATE UNIQUE INDEX 고객번호_idx ON 고객(고객번호 DESC);
    - 고객 테이블에서 UNIQUE한 특성을 갖는 고객번호 속성에 대해 내림차순으로 정렬하여 고개번호_idx라는 이름으로 인덱스를 정의
</aside>

### ALTER

<aside>
💡 ALTER TABLE - 테이블을 변경하는 명령문

- 새로운 속성을 추가할 때 사용
    - ALTER TABLE 테이블이름 ADD 속성이름 데이터타입 [DEFAULT 기본값];
    - ALTER TABLE 학생 ADD 학년 VARCHAR(3);
        - 학생 테이블에 최대 3문자까지 저장할 수 있는 학년 속성을 추가
- 기존 속성을 변경할 때 사용
    - ALTER TABLE 테이블 이름 ALTER 속성이름 데이터 타입 [SET DEFAULT 기본값];
    - ALTER TABLE 학생 ALTER 학번 VARCHAR(10) NOT NULL;
        - 학생 테이블의 학번 필드의 데이터 타입과 크기를 VARCHAR(10)으로 변경하고 NULL값이 입력되지 않도록 변경
- 기존 속성을 삭제할 때 사용
    - ALTER TABLE 테이블이름 DROP COLUMN 속성이름 [CASCADE];
</aside>

### DROP

SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 삭제

<aside>
💡 스키마 , 도메인, 기본 테이블, 뷰 테이블, 인덱스, 제약 조건 등을 제거

- DROP SCHEMA 스키마이름 [CASCADE | RESTRICT];
- DROP DOMAIN 도메인이름 [CASCADE | RESTRICT];
- DROP TABLE 테이블이름 [CASCADE | RESTRICT];
- DROP VIEW 뷰이름  [CASCADE | RESTRICT];
- DROP INDEX 인덱스이름 [CASCADE | RESTRICT];
- DROP TABLE 학생 CASCADE;
    - 학생 테이블을 제거하되 학생 테이블을 참조하는 모든 데이터를 함께 제거
- DROP CONSTRAINT 제약조건이름;
    - CASCADE
        - 제거할 요소를 참조하는 다른 모든 개체를 함께 제거
    - RESTRICT
        - 다른 개체가 제거할 요소를 참조 중일 때는 제거를 취소
</aside>

# DCL 개요

### DCL(Data Control Language, 데이터 제어어)

데이터의 보안, 무결성, 회복, 병행 제어 등을 정의하는데 사용하는 언어 데이터베이스 관리자가 데이터 관리를 목적으로 상요함

## DCL의 종류

### Commit

<aside>
💡 명령에 의해 수행된 결과를 실제 물리적 디스크로 저장

- 트랜잭션이 수행된 내용을 데이터베이스에 반영하는 명령어
- Auto Commit 기능이 설정되어 있는 경우  DML문이 성공적으로 완료되었을 때 자동으로 COMMIT 할 수 있음
</aside>

### ROLLBACK

<aside>
💡 작업이 비정상적으로 종료된 경우 원상태로 복구

- 변경되었거나 COMMIT되지 않은 모든 내용들을 취소하고 데이터베이스를 이전 상태로 되돌리는 명령
- 일부 변경된 내용만 데이터베이스에 반영되게 되면 비일관성 상태가 발생할 수 있어 일부분만 완료된 트랜잭션은 롤백 되어야 함
</aside>

### GRANT

<aside>
💡 사용자에게 데이터베이스 사용 권한을 부여

- GRANT 사용자등급 TO 사용자ID [IDENTIFIED BY 암호];
</aside>

### REVOKE

<aside>
💡 데이터베이스 사용자의 권한을 취소

- REVOKE 사용자등급 FROM 사용자ID;
</aside>

## 사용자 등급의 종류

### DBA(데이터 베이스 관리자)

### RESOURCE(데이터베이스 및 테이블 생성 가능자)

### CONNECT(단순 사용자)

## 권한부여 권한 관련

### 권한의 종류

ALL, SELECT, INSERT, DELETE, UPDATE, ALTER

- GRANT 권한 ON 개체 TO 사용자ID [WITH GRANT OPTION];
- REVOKE [GRANT OPTION FOR] 권한 ON 개체 FROM 사용자 ID;
- WITH GRANT OPTION
    - 부여 받은 권한을 다른 사용자에게 부여할 수 있는 권한
- GRANT OPTION FOR
    - 다른 사용자에게 권한을 부여할 수 있는 권한을 취소
- CASCADE
    - 권한 취소 시 권한을 부여 받았던 사용자가 다른 사용자에게 부여한 권한도 취소

### Commit/RollBack

**SAVEPOINT**

- 트랜잭션 내에 ROLLBACK할 위치인 저장점을 지정하는 명령

<aside>
💡 저장점을 지정할 때에는 이름을 부여함

저장점 이전까지의 처리 내용이 모두 취소됨
SAVEPOINT SP;
DELETE FROM 학생 WHERE 학번 = 1122;
ROLLBACK SP;

</aside>

# DML 개요

### DML(Data Manipulation Language, 데이터 조작어)

저장된 데이터를 실질적으로 관리하는데 사용되는 언어

### INSERT

대응하는 속성과 데이터는 개수와 데이터 유형이 일치해야 함

모든 속성을 사용하는 경우 속성명 생략가능

SELECT 문을 사용하여 다른 테이블의 검색 결과를 삽입할 수 있음

<aside>
💡 INSERT INTO 테이블이름 (속성1,속성2,…) VALUES (데이터1,데이터2,…);

INSERT INTO 학생(이름, 학과) VALUES(’이영준’,’컴퓨터공학’);
학생 테이블에 이름과 학과 속성에 지정된 값으로 튜플을 추가함

</aside>

### DELETE FROM

- 기본 테이블에 있는 튜플들 중에서 특정 튜플을 삭제
- WHERE 부분이 생략된 경우 해당 테이블의 모든 튜플이 삭제됨
- DROP은 테이블 자체가 삭제되는 것이고 DELETE는 테이블의 구조는 남아있음

<aside>
💡 DELETE FROM 테이블이름 [WHERE 조건];

DELETE FROM 학생 WHERE 이름 = ‘이영준’;
학생 테이블에서 이름 속성값이 이영준인 튜플을 삭제

</aside>

### UPDATE SET

- 특정 튜플의 내용을 변경할 때 사용
- WHERE부분이 생략된 경우 테이블내의 전체 튜플의 해당 속성 값이 갱신

<aside>
💡 UPDATE 테이블이름 SET 속성명=데이터 [WHERE 조건];

UPDATE 학생 SET 주소=’종로구’ WHERE 이름=’김범수’;
학생 테이블에서 이름이 김범수인 튜플의 주소 속성의 값을 종로구로 변경

</aside>
