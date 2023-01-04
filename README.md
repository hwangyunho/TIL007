# TIL007

## 서브쿼리

***

### SINGLE ROW SUBQUERY 
* 서브쿼리의 결과가 1개의 ROW인 경우
> * '>, <, =, >=, <=' 등의 단일 값 비교연산자
* WHERE 문의 조건에 넣음

***

### MULTI ROW SUBQUERY  
* 서브쿼리의 결과가 여러 ROW인 경우
> * 'IN, NOT IN, >ANY, <ANY, >ALL, <ALL ' 등의 연산자 사용
* ALL / ANY : 앞에 비교 연산자를 사용

***

### MULTI COLUMN SUBQUERY
  * SELECT 문
  * FROM 문
  * WHERE 문(컬럼) (
                    서브쿼리
                            )
  * AND (컬럼)     (
                    서브쿼리
                            )

***

## 조인

***

* 테이블의 컬럼간에 공통 값(VALUE)을 추출하는 것
* USING(공통 컬럼)       ON(컬럼명이 다를 때)
* INNER JOIN = JOIN : 같은 값만 추출 / FALSE, NULL은 추출되지 않는다
* OUTER JOIN : 주종 관계/ 주 테이블은 전체 출력, 종 테이블은 같은 값만 출력
				-- LEFT OUTER JOIN / RIGHT OUTER JOIN
* CROSS JOIN : 비교 컬럼이 속한 모든 테이블을 출력

***

