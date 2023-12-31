## SECTION 1 데이터베이스의 기본

### 1. 엔터티

(1) 엔터티(Entity): 사람, 장소, 물건, 사건, 개념 등 여러 개의 속성을 지닌 명사

ex) 회원 - 이름, 아이디, 주소, 전화번호

(2) 존재 종속(existence dependency) 관계

- 강한 개체(strong entity): 다른 개체의 존재 여부를 결정하는 개체
- 약한 개체(weak entity): 다른 개체의 존재 여부에 종속적인 개체

### 2. 릴레이션

(1) 릴레이션(relation)

- 데이터베이스에서 정보를 구분하여 저장하는 기본 단위
- 하나의 엔터티에 관한 데이터를 저장한 것
- 관계형 데이터베이스 → 테이블, NoSQL 데이터베이스 → 컬렉션

(2) 테이블과 컬렉션

- 관계형 데이터베이스: 레코드(튜플)-테이블-데이터베이스
- NoSQL 데이터베이스: 도큐먼트-컬렉션-데이터베이스

### 3. 속성

- 속성(attribute): 릴레이션에서 관리하는 구체적이고 고유한 이름을 갖는 정보

### 4. 도메인

- 도메인(domain): 하나의 속성이 가질 수 있는 모든 값들의 집합
    
    ex) 성별(속성) - {남, 여}(도메인)
    

### 5. 필드와 레코드

(1) 레코드(튜플): 관계형 데이터베이스의 행

(2) 필드 타입

- 숫자 타입(TINYINT, INT, BIGINT)
- 날짜 타입(DATE, DATETIME, TIMESTAMP)
- 문자 타입(CHAR, VARCHAR, TEXT, BLOB, ENUM, SET)
    - CHAR: 고정 길이 문자열
    - VARCHAR: 가변 길이 문자열(데이터 바이트 + 길이 기록용 1바이트)
    - TEXT: 큰 문자열 저장
    - BLOB: 이미지, 동영상 등
    - ENUM: enum 리스트 중 하나만 선택
    - SET: 리스트 중 여러 개 선택

### 6. 관계

(1) 관계(relationship): 테이블 간 맺고 있는 의미있는 연관성 → 관계 화살표로 표시

<img width="504" alt="image" src="https://github.com/CS-STUDY-17/CS-Study/assets/77063375/deb4b67e-c417-494c-b257-e04307be8258">


(2) 관계의 유형

- 1:1 관계
- 1:N 관계
- N:M 관계

### 7. 키

(1) 키(key): 테이블에서 튜플들을 유일하게 구별하는 속성 또는 속성들의 집합

(2) 키의 특성

- 유일성(uniqueness): 하나의 테이블에서 모든 튜플은 서로 다른 키 값을 가져야함
- 최소성(minimality): 꼭 필요한 최소한의 속성들로만 키를 구성

(3) 키의 종류

- 수퍼키(super key): 유일성을 만족하는 속성 또는 속성 집합
- 후보키(candidate key): 유일성과 최소성을 만족하는 속성 또는 속성 집합
- 기본키(primary key): 후보키 중에서 기본으로 사용하기 위해 선택한 키
- 대체키(alternate key): 기본키로 선택되지 못한 후보 키
- 외래키(foreign key): 다른 테이블의 기본키를 참조하는 속성 또는 속성 집합

<br>
<br>

## SECTION 2 ERD와 정규화 과정

### 1. ERD란?

(1) **ERD(Entity Relationship Diagram)**: E-R 모델을 이용해 개념적 모델링의 결과를 그림으로 표현한 것

(2) ERD의 중요성

- 시스템 요구사항을 기반 작성한 ERD를 토대로 데이터베이스를 구축
- 디버깅 또는 비즈니스 프로세스 재설계가 필요한 경우에 설계도 역할을 담당

### 2. 정규화

(1) **이상(anomaly) 현상**: 불필요한 데이터 중복으로 인해 릴레이션에 대한 데이터 삽입, 수정, 삭제 연산을 수행할 때 발생할 수 있는 부작용

- 삽입 이상: 새 데이터를 삽입하기 위해 불필요한 데이터도 함께 삽입해야 하는 문제
- 갱신 이상: 중복 투플 중 일부만 변경하여 데이터가 불일치하게 되는 모순 문제
- 삭제 이상: 투플을 삭제하면 꼭 필요한 데이터까지 함께 삭제되는 데이터 손실의 문제

(2) **정규화**: 이상 현상이 발생하지 않도록 릴레이션을 관련 있는 속성들로만 구성하기 위해 릴레이션을 분해하는 과정

(3) **정규형(NF; Normal Form)**: 릴레이션이 정규화된 정도, 각 정규형마다 제약조건이 존재하며 정규형의 차수가 높아질수록 요구되는 제약조건이 많아지고 엄격해짐

<aside>
💡 정규형 원칙

- 무손실 분해
    - 릴레이션이 의미상 동등한 릴레이션으로 분해되어야 하고, 분해로 인한 정보 손실이 발생하지 않아야 함
    - 분해된 릴레이션들을 자연 조인하면 분해 전의 릴레이션으로 복원 가능해야 함
- 데이터 중복성 감소
- 분리의 원칙: 독립적인 관계는 별개의 릴레이션으로 표현해야 함
</aside>

- **제1정규형(1NF; First Normal Form)**: 릴레이션의 모든 속성이 더는 분해되지 않는 원자 값(atomic value)만 가짐 → 제 1 정규형을 만족해야 관계 데이터베이스의 릴레이션이 될 자격이 있음
- **제2정규형(2NF; Second Normal Form)**: 릴레이션이 제1정규형에 속하고, 기본키가 아닌 모든 속성이 기본키에 완전 함수 종속됨
    
    > 함수 종속
    > 
    > - 릴레이션 내의 모든 투플에서 하나의 X 값에 대한 Y 값이 항상 하나임
    > - X와 Y는 하나의 릴레이션을 구성하는 속성들의 부분 집합
    > - `X → Y`로 표현(X: 결정자, Y: 종속자)
    
    > 완전 함수 종속(FFD; Full Functional Dependency): 릴레이션 속성 집합 Y에서 집합 X에 함수적으로 종속되어 있지만, 속성 집합 X의 전체가 아닌 일부분에는 종속되지 않음
    > 
- **제3정규형(3NF; Third Normal Form)**: 릴레이션이 제2정규형에 속하고, 기본키가 아닌 모든 속성이 기본키에 이행적 함수 종속이 되지 않음
    
    > 이행적 함수 종속(transitive FD): 릴레이션을 구성하는 3개의 속성 집합 X, Y, Z에 대해 함수 종속 관계 `X → Y`와 `Y → Z` 가 존재하면 논리적으로 `X → Z`가 성립되는데, 이때 Z가 X에 이행적으로 함수 종속되었다고 함
    > 
- **보이스/코드 정규형(BCNF; Boyce/Codd Normal Form)**: 릴레이션의 함수 종속 관계에서 모든 결정자가 후보키가 되어야 함

<br>
<br>

## SECTION 3 트랜잭션과 무결성

### 1. 트랜잭션이란?

- 데이터베이스에서 하나의 논리적 기능을 수행하기 위한 작업의 단위
- 서로 분리될 수 없는 작업 단위
- 한꺼번에 수행되어야할 SQL문들의 집합

### 2. 트랜잭션의 특성(ACID)

(1) **원자성(Atomicity)**

- All or Nothing
    - 트랜잭션에 속한 모든 연산들이 모두 실행 완료 되거나 하나도 실행되지 않아야 함
    - 연산들이 부분적으로 실행되는 것은 허용되지 않음
    - 트랜잭션 수행 도중 장애가 발생한 경우
        - 장애 발생 전까지 실행된 연산 결과를 모두 취소해야 함 → nothing
        - 데이터베이스를 트랜잭션 작업 전 상태로 되돌려야 함

<aside>
💡 트랜잭션의 주요 연산

- commit 연산: 트랜잭션이 성공적으로 수행되었음을 선언(작업 완료)
    
    → commit 연산이 실행되면 트랜잭션의 수행 결과가 데이터베이스(disk)에 반영되고 일관된 상태를 지속적으로 유지하게 됨
    
- rollback 연산: 트랜잭션을 수행하는 데 실패했음을 선언(작업 취소)
    
    → rollback 연산이 실행되면 트랜잭션이 지금까지 실행한 연산의 결과가 취소되고 데이터베이스가 트랜잭션 수행 전의 일관된 상태로 되돌아감
    
</aside>

<aside>
💡 트랜잭션 전파
여러 트랜잭션 관련 메서드의 호출을 하나의 트랜잭션에 묶이도록 하는 것
ex) Spring - `@Transactional` 애너테이션

</aside>

(2) **일관성(Consistency)**: 트랜잭션이 성공적으로 수행된 후에도 데이터베이스가 일관된 상태를 유지해야 함

(3) **격리성(Isolation)**

- 수행 중인 트랜잭션이 완료될 때까지 다른 트랜잭션들이 중간 연산 결과에 접근할 수 없음
- 여러 트랜잭션이 동시에 수행되더라도 순서대로 하나씩 수행된 결과와 동일한 결과를 제공해야함
- 여러 개의 격리 수준으로 나뉘어 격리성을 보장
    - **SERIALIZABLE**: 트랜잭션을 순차적으로 진행시키고 여러 트랜잭션이 동시에 같은 행에 접근 불가 → 매우 엄격한 수준, 성능 낮음
    - **REPEATBLE_READ**: 하나의 트랜잭션이 수정한 행을 다른 트랜잭션이 수정은 불가하지만 새로운 행을 추가하는 것은 허용
    - **READ_COMMITED**: 커밋 완료된 데이터에 대해서만 조회를 허용하지만 어떤 트랜잭션이 접근한 행을 다른 트랜잭션이 수정하는 것을 허용
    - **READ_UNCOMMITED**: 하나의 트랜잭션이 커밋되기 이전에 다른 트랜잭션이 접근 가능 → 가장 낮은 격리수준, 성능 높음
    
    <img width="663" alt="image" src="https://github.com/CS-STUDY-17/CS-Study/assets/77063375/1c24f451-16e8-4f57-ba2c-aaa895fd3670">

    <br>
    <aside>
    💡 격리 수준에 따라 발생하는 현상
    
    - 팬텀 리드(phantom read): 한 트랜잭션 내에서 동일한 쿼리를 보냈을 때 해당 조회 결과가 다른 경우
    - 반복 가능하지 않은 조회(non-repeatable read): 한 트랜잭션 내의 같은 행에 두 번 이상 조회가 발생했을 때 그 값이 다른 경우
    - 더티 리드(dirty read): 한 트랜잭션이 실행 중일 때 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 행의 데이터를 읽는 경우
    </aside>

(4) **지속성(Durability)**: 트랜잭션이 성공적으로 완료된 후 데이터베이스에 반영한 수행 결과는 영구적이어야 함

### 3. 무결성

(1) 무결성이란?

- 데이터의 정확성, 일관성, 유효성을 유지하는 것
- 무결성이 유지되어야 데이터베이스에 신뢰가 생김

(2) 무결성의 종류

- **개체 무결성**: 기본키로 선택된 필드는 빈 값을 허용하지 않음
- **참조 무결성**: 서로 참조 관계에 있는 두 테이블의 데이터는 항상 일관된 값을 유지해야함
- **고유 무결성:** 특정 속성에 대해 고유한 값을 가지도록 조건이 주어진 경우 그 속성 값은 모두 고유한 값을 가짐
- **NULL 무결성**: 특정 속성 값에 NULL이 올 수 없다는 조건이 주어진 경우 그 속성 값은 NULL이 될 수 없음

<br>
<br>

## SECTION 4 데이터베이스의 종류

### 1. 관계형 데이터베이스

(1) 관계형 데이터베이스(RDBMS)란?

- 행과 열을 가지는 표 형식 데이터를 저장하는 형태의 데이터베이스
- SQL 언어를 사용하여 조작

(2) 종류

- MySQL
- PostgreSQL
- Oracle

### 2. NoSQL 데이터베이스

(1) NoSQL 데이터베이스란?: SQL을 사용하지 않는 데이터베이스

(2) 종류

- MongoDB
- redis
