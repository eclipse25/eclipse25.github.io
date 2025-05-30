---
layout: post
title: "SQL DDL, DML, DCL, TCL 기본 쿼리"
categories: [Database]
tags: [Data, Database, SQL]
---

# SQL 기본 명령어 4가지 - DDL, DML, DCL, TCL

## **데이터 정의어(DDL)**

테이블 생성, 열 추가, 열 데이터 타입 변경, 테이블명 변경, 테이블 삭제<br>
**CREATE, ALTER, DROP** <br>

- Practice 데이터베이스 생성, 사용하기

  ```sql
  CREATE DATABASE Practice;
  USE Practice;
  ```

- 회원 테이블 생성

  - 열 이름을 먼저 쓰고 뒤에 데이터 타입 작성
  - 테이블은 각 열마다 반드시 1가지 데이터 타입으로 정의
    - 대표적인 데이터 형식: 숫자형, 문자형, 날짜형
  - 테이블에서 각 열마다 제약 조건 정의 가능
  - PK(Primary Key): 중복되어 나타날 수 없는 단일 값, NOT NULL

  ```sql
  CREATE TABLE 회원 (
  회원번호 INT PRIMARY KEY,     -- 제약조건: PRIMARY KEY
  이름 VARCHAR(20),
  가입일자 DATE NOT NULL,       -- 제약조건: NOT NULL
  수신동의 BIT
  );
  ```

- 회원 테이블 조회하기

  ```sql
  SELECT *
  FROM 회원;

  SELECT * FROM 회원; --한 줄도 가능
  ```

- 테이블에 열 추가하기

  ```sql
  ALTER TABLE 회원 ADD 성별 VARCHAR(2); -- 성별 열 추가
  ```

- 열 데이터 타입 변경하기

  ```sql
  ALTER TABLE 회원 MODIFY 성별 VARCHAR(20);
  ```

- 열 이름 변경하기

  ```sql
  ALTER TABLE 회원 CHANGE 성별 성 VARCHAR(2); -- 성별 -> 성 으로 열 이름 변경
  ```

- 테이블 이름 변경하기

  ```sql
  ALTER TABLE 회원 RENAME 회원정보; -- 회원 -> 회원정보로 테이블 이름 변경
  ```

- 테이블 삭제하기

  ```sql
  DROP TABLE 회원정보;
  ```

## **데이터 조작어(DML)**

테이블 삽입, 조회, 수정, 삭제<br>
**SELECT, INSERT, UPDATE, DELETE** <br>

| 회원번호 | 이름        | 가입일자 | 수신동의 |
| -------- | ----------- | -------- | -------- |
| INT      | VARCHAR(20) | DATE     | BIT      |

- 데이터 삽입하기

  ```sql
  INSERT INTO 회원정보 VALUES (1001, '이익준', '2023-09-01', 1);
  INSERT INTO 회원정보 VALUES (1002, '채송화', '2023-09-02', 0);
  INSERT INTO 회원정보 VALUES (1003, '김준완', '2023-09-03', 1);
  INSERT INTO 회원정보 VALUES (1004, '안정원', '2023-09-04', 0);
  ```

- PRIMARY KEY 제약 조건을 위반하는 경우

  ```sql
  INSERT INTO 회원정보 VALUES (1004, '양석형', '2023-09-05', 1); --에러, 중복 저장 불가
  ```

- NOT NULL 제약 조건을 위반하는 경우

  ```sql
  INSERT INTO 회원정보 VALUES (1005, '양석형', NULL, 1); -- 에러, 저장 불가
  ```

- 데이터 타입 제약 조건을 위반하는 경우

  ```sql
  INSERT INTO 회원정보 VALUES (1005, '양석형', 1, 1); --문자열이 아닌 숫자라서 저장 불가
  ```

- 데이터 조회하기

  ```sql
  SELECT * FROM 회원정보; -- 테이블의 모든 열 조회
  SELECT 회원번호, 이름 FROM 회원정보; -- 특정 열 조회
  SELECT 회원번호, 이름 AS 성명 FROM 회원정보; -- 특정 열 이름을 변경하여 조회
  ```

- 데이터 수정하기

  - 수정 전 데이터 수정, 삭제 제한 설정 해제

    - MySQL_Workbench (Edit → Preferences → SQL Editor → Other → Safe updates 체크박스 해제)

  - 열의 모든 데이터 수정

    ```sql
    UPDATE 회원정보 SET 수신동의 = 0;
    ```

  - 특정 조건 데이터 수정

    ```sql
    UPDATE 회원정보 SET 수신동의 = 1 WHERE 이름 = '채송화';
    ```

- 데이터 삭제

  - 특정 데이터 삭제

    ```sql
    DELETE FROM 회원정보 WHERE 이름 = '이익준';
    ```

  - 모든 데이터 삭제

    ```sql
    DELETE FROM 회원정보;
    ```

## **데이터 제어어(DCL)**

사용자 확인, 사용자 추가 및 삭제, 권한 부여 및 삭제<br>
데이터베이스 관리자(DBA)가 특정 사용자에게 데이터 접근 권한 부여, 제거할 때 사용<br>
**GRANT, REVOKE** <br>

- 사용자 목록 확인하기

  ```sql
  SELECT * FROM USER;
  ```

- 사용자 추가하기

  ```sql
  CREATE USER 'TEST1'@LOCALHOST IDENTIFIED BY 'TEST2'; # 'TEST1'은 ID, 'TEST2'는 비밀번호
  ```

- 사용자 비밀번호 변경하기

  ```sql
  SET PASSWORD FOR 'TEST2' @LOCALHOST = '1234';
  ```

- 권한 부여 및 제거

  - 권한 종류: CREATE, ALTER, DROP, INSERT, DELETE, UPDATE, SELECT 등

  - 특정 권한 부여

    ```sql
    GRANT SELECT, DELETE ON PRACTICE.회원정보 TO 'TEST1'@LOCALHOST;
    ```

  - 특정 권한 제거

    ```sql
    REVOKE DELETE ON PRACTICE.회원정보 FROM 'TEST1'@LOCALHOST;
    ```

  - 모든 권한 부여

    ```sql
    GRANT ALL ON PRACTICE.회원정보 TO 'TEST1'@LOCALHOST;
    ```

  - 모든 권한 제거

    ```sql
    REVOKE ALL ON PRACTICE.회원정보 FROM 'TEST1'@LOCALHOST;
    ```

- 사용자 삭제

  ```sql
  DROP USER 'TEST1'@LOCALHOST;
  ```

## **트랜잭선 제어어(TCL)**

데이터 조작어 명령어 실행, 취소, 임시저장<br>
데이터의 일관성을 유지하기 위해 사용되며, 명령어의 실행을 관리한다.<br>
**BEGIN, COMMIT, ROLLBACK**

- 트랜잭션 시작

  ```sql
  BEGIN;
  ```

- 데이터 삽입하고 확인하기

  ```sql
  INSERT INTO 회원정보 VALUES (1001, '이익준', '2023-09-01', 1);

  SELECT * FROM 회원정보; -- 삽입 확인
  ```

- 취소하기

  ```sql
  ROLLBACK;
  ```

- 데이터 삽입 후 트랜잭션 취소 확인하기

  ```sql
  INSERT INTO 회원정보 (회원번호, 이름, 가입일자, 수신동의) VALUES (1001, '이익준', '2023-09-01', 1);
  SELECT * FROM 회원정보; -- 삽입된 데이터 확인
  ROLLBACK; -- 트랜잭션 취소
  SELECT * FROM 회원정보; -- 취소 후 데이터 확인
  ```

- 실행하기

  ```sql
  COMMIT;
  ```

- SAVEPOINT와 ROLLBACK 사용하기

  - 트랜잭션 중에 여러 작업을 수행한 후, 특정 지점으로 돌아가고 싶을 때 SAVEPOINT를 사용한다.

  ```sql
  BEGIN;
  INSERT INTO 회원정보 VALUES (1002, '채송화', '2023-09-02', 0);
  SAVEPOINT SP1; -- 첫 번째 저장 지점 설정
  UPDATE 회원정보 SET 이름 = '김준완' WHERE 회원번호 = 1002;
  SAVEPOINT SP2; -- 두 번째 저장 지점 설정
  ROLLBACK TO SP1; -- 첫 번째 저장 지점으로 롤백
  COMMIT; -- 변경사항 확정
  ```
