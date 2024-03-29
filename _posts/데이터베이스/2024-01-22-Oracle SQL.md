---
layout: post
title: "SQL - Oracle SQL 계층형 쿼리"
categories: [데이터베이스]
tags: [Data, Database, SQL]
---

## Oracle SQL

### 개념

- Oracle Database에서 사용되는 SQL 언어의 확장 버전이다.
- 표준 SQL 기능에 추가로 고급 기능과 Oracle 특유의 확장 기능을 포함한다.

### 기능

- 데이터 정의 언어(DDL), 데이터 조작 언어(DML), 데이터 제어 언어(DCL), 트랜잭션 제어 언어(TCL)
- 파티셔닝, 복제, 대용량 데이터 처리를 위한 병렬 처리, 고급 분석 함수, 공간 및 그래프 데이터 처리 등의 고급 기능을 지원한다.
- PL/SQL(Procedural Language/SQL)을 지원함으로써 SQL에 절차적 프로그래밍 기능을 추가하여 복잡한 비즈니스 로직을 데이터베이스 서버 내에서 실행할 수 있게 한다.

## Oracle 쿼리

### 계층형 쿼리(CONNECT BY, START WITH)

- 기본 개념

  - 계층적 쿼리는 데이터를 트리 구조로 표현하고자 할 때 사용된다.
    - 계층적 쿼리(Hierarchical Query): 트리 구조로 이루어진 데이터를 조회하는 쿼리
    - 트리 구조(Tree Structure): 데이터가 부모-자식 관계로 이루어진 계층적 구조
  - Oracle SQL에서는 `CONNECT BY`와 `START WITH` 절을 사용하여 이런 종류의 쿼리를 작성한다.
    - START WITH 절: 트리의 어디서 시작할지 결정한다. 보통 가장 상위의 부모 노드에서 시작한다.
    - CONNECT BY 절: 부모와 자식 간의 관계를 정의한다. PRIOR 키워드는 부모 노드를 가리키는 데 사용된다.

- 예시(SQLD 45회 단답형 4번)

  | C1  | C2   | C3  |
  | --- | ---- | --- |
  | 1   | NULL | A   |
  | 2   | 1    | B   |
  | 3   | 1    | C   |
  | 4   | 2    | D   |

  ```sql
  SELECT C1, C2, C3
  FROM SQLD44
      CONNECT BY PRIOR C1 = C2
            START WITH C1 = 1
      ORDER SIBLINGS BY C1 DESC;
  ```

  - 계층형 쿼리 결과에서 C3의 2번째 값은? → C
    - 이 쿼리는 C1을 기준으로 계층적 구조를 만들고, 같은 부모를 가진 노드들(C3의 값)을 C1 값에 따라 내림차순으로 정렬한다. C1=1에서 시작하므로 최상위 노드는 A이다.
    - CONNECT BY PRIOR C1 = C2를 사용하여 계층을 구성한다.
      - 부모 행의 C1 값이 현재 행의 C2 값과 일치해야 한다는 뜻이다.
      - C1=2(B)와 C1=3(C)는 C1=1(A)의 자식이다.
      - C1=4(D)는 C1=2(B)의 자식이다.
    - ORDER SIBLINGS BY C1 DESC에 따라, 같은 부모를 가진 노드들은 C1 값이 큰 순서대로 정렬된다.
    - C3의 값에 따른 순서는 다음과 같다: A, C, B, D
