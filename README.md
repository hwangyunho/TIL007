# TIL007

## 서브쿼리

***

* SINGLE ROW SUBQUERY 서브쿼리의 결과가 1개의 ROW인 경우
> * '>, <, =, >=, <=' 등의 단일 값 비교연산자
* WHERE 문의 조건에 넣음

***

## MULTI ROW SUBQUERY  
* 서브쿼리의 결과가 여러 ROW인 경우
> * 'IN, NOT IN, >ANY, <ANY, >ALL, <ALL ' 등의 연산자 사용
* ALL / ANY : 앞에 비교 연산자를 사용

***

## MULTI COLUMN SUBQUERY
  * SELECT 문
  * FROM 문
  * WHERE 문(컬럼) (
                    서브쿼리
                            )
  * AND (컬럼)     (
                    서브쿼리
                            )
