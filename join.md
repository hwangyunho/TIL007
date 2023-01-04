-- Q1. 사원의 이름과 사원이 속한 부서이름을 출력하자.(INNER JOIN = 일반적인 JOIN)
USE MY_EMP;
-- ANSI
SELECT ENAME, DNAME
FROM EMP INNER JOIN DEPT USING(DEPTNO);

-- MYSQL
SELECT ENAME, DNAME
FROM MY_EMP, MY_DEPT
WHERE MY_EMP.DEPTNO = MY_DEPT.DEPTNO;

-- Q2. Q1번의 전체 컬럼을 리턴해서 출력 해보자. 
SELECT *
FROM MY_EMP JOIN MY_DEPT USING(DEPTNO);

-- Q3. 간단한 테이블을 생성해서 JOIN을 생각해보자.
CREATE TABLE X(
 X1 VARCHAR(5),
 X2 VARCHAR(5)
 );
CREATE TABLE Y(
 Y1 VARCHAR(5),
 Y2 VARCHAR(5)
 );

INSERT INTO X VALUES ('A', 'D');

INSERT INTO Y VALUES ('A', '1');
INSERT INTO Y VALUES ('B', '2');
INSERT INTO Y VALUES ('C', '3');
INSERT INTO Y VALUES (NULL, '1');

SELECT * FROM X;
SELECT * FROM Y;
/*
	X1		X2		Y1		Y2
    A		D		A		1
					B		2
					C		3
					NULL	1
*/
SELECT *
FROM X, Y
WHERE X1 = Y1;

SELECT *
FROM X JOIN Y ON X1 = Y1 ;

-- Q4. 주종 관계를 이용한 조인을 출력 해보자.
SELECT *
FROM X RIGHT OUTER JOIN Y
ON X1 = Y1 ;                    -- Y 주 테이블, X 종 테이블

SELECT *
FROM X LEFT OUTER JOIN Y
ON X1 = Y1 ;					-- X 주 테이블, Y 종 테이블

-- SELECT *
-- FROM X FULL OUTER JOIN Y
-- ON X1 = Y1 ;					-- ANSI에 있음 FULL = LEFT + RIGHT

-- Q5. 급여 등급 테이블을 작성해 보자.
CREATE TABLE SALGRADE(
	GRADE INT,
    LOSAL INT,
    HISAL INT
);
 
insert into salgrade values (1, 700, 1200);
insert into salgrade values (2, 1201, 1400);
insert into salgrade values (3, 1401, 2000);
insert into salgrade values (4, 2001, 3000);
insert into salgrade values (5, 3001, 9999);
 
 -- Q6. NONEQUI JOIN
 --  각 사원의 이름과 월급 그리고 그 사원의 급여등급을 출력해보자.
SELECT ENAME, SAL, GRADE
FROM MY_EMP JOIN SALGRADE ON (SAL  BETWEEN LOSAL AND HISAL);
 
 -- Q7. 각 사원의 이름과 월급, 급여등급, 부서이름을 출력 해보자.
 --  테이블 제약사항이 있는것을 선 조인, 나머지를 후 조인
 SELECT ENAME, SAL, GRADE, DNAME
 FROM MY_EMP JOIN MY_DEPT USING(DEPTNO) 
	JOIN SALGRADE ON (SAL BETWEEN LOSAL AND HISAL);
 
 -- Q8. SELF JOIN : 테이블 하나에 같은 값을 가진 컬럼을 조인하는 것
 -- 테이블에 별칭 지정 후 조인
 --  사원의 번호와 이름, 관리자의 번호와 이름을 출력해보자.
 --   사원의 MGR = 관리자의 EMPNO
SELECT 사원.EMPNO, 사원.ENAME, 관리자.EMPNO, 관리자.ENAME
FROM MY_EMP AS 사원 LEFT OUTER JOIN MY_EMP AS 관리자 ON 사원.MGR = 관리자.EMPNO;

-- 1) CREATE TABLE로 새 테이블 만들기
-- 2) CREATE TABLE에서 기본 키 (PRIMARY KEY) 제약 조건 지정
-- 3) CREATE TABLE에서 고유 키(UNIQUE KEY) 제약 조건 지정
-- 4) CREATE TABLE에서 검사 (CHECK) 제약 조건 지정
-- 5) CREATE TABLE에서 열에 기본값 지정
-- 6) CREATE TABLE에서 외래 키 (FOREIGN KEY) 제약 조건 지정

CREATE DATABASE  STUDENTS;
USE STUDENTS;

--  << 학생 정보를 유지하기 위한 students 테이블 생성 >>- 
/*
student_id: 레코드 ID(정수 유형) : INT
student_number: 학생 번호(최대 10자리 문자열 유형) : VARCHAR
first_name: 아래 이름(최대 50자리 문자열 유형) : VARCHAR
last_name: 이름(최대 50자리 문자열 유형) : VARCHAR
middle_name: 중간 이름(최대 50자리 문자열 유형) : VARCHAR
birthday: 생일(날짜형) : DATE
gender: 성별(문자열 형식으로 M: 남성, F: 여성) : ENUM
paid_flag : 수업료를 지불했는지 여부 플래그 (BOOL 형식으로 FALSE (0) : 미결제, TRUE (1) : 지불됨) : BOOL
*/
-- 1. CREATE TABLE로 새 테이블 만들기
CREATE TABLE students( 
	student_id 		INT				NOT NULL,
    student_number 	VARCHAR(10)		NOT NULL,
    first_name 		VARCHAR(50) 	NOT NULL,
    last_name 		VARCHAR(50) 	NOT NULL,
    middle_name 	VARCHAR(50) 	NULL,
    birthday 		DATE 			NOT NULL,
    gender 			ENUM('M', 'F') 	NOT NULL,
    paid_flag 		BOOL			NOT NULL
);
DESC students;
INSERT INTO students VALUES(1,1,1,1,1,NOW(),'M',TRUE);
INSERT INTO students VALUES(1,1,1,1,1,NOW(),'F',FALSE);
SELECT * FROM STUDENTS;

-- 2. CREATE TABLE에서 기본 키 (PRIMARY KEY)제약 조건 지정 _식별키
--  테이블당 하나의 컬럼만 지정 할 수 있다. null값 불가능
CREATE TABLE students02( 
	student_id 		INT				NOT NULL,
    student_number 	VARCHAR(10)		NOT NULL,
    first_name 		VARCHAR(50) 	NOT NULL,
    last_name 		VARCHAR(50) 	NOT NULL,
    middle_name 	VARCHAR(50) 	NULL,
    birthday 		DATE 			NOT NULL,
    gender 			ENUM('M', 'F') 	NOT NULL,
    paid_flag 		BOOL			NOT NULL,
    PRIMARY KEY ( student_id )
);  
DESC students02;
INSERT INTO students02 VALUES(4,1,1,1,1,NOW(),'M',TRUE);
INSERT INTO students02 VALUES(2,1,1,1,1,NOW(),'F',FALSE);
INSERT INTO students02 VALUES(null,1,1,1,1,NOW(),'F',FALSE);
SELECT * FROM STUDENTS02;

CREATE TABLE students03(
	student_id		INT ,
    student_number 	VARCHAR(10),
    PRIMARY KEY (student_id)
);

DESC students03;

CREATE TABLE students04(
	student_id		INT 		AUTO_INCREMENT,
    student_number 	VARCHAR(10),
    PRIMARY KEY (student_id)
);

DESC students04;

INSERT INTO students04 VALUES(NULL,1);
INSERT INTO students04 VALUES(12,NULL);
INSERT INTO students04 VALUES(NULL,NULL);
INSERT INTO students04(student_number) VALUES(NULL);

SELECT * FROM students04;

DROP TABLE students05;
CREATE TABLE students05(
	student_id		INT 		 AUTO_INCREMENT,
    student_number 	VARCHAR(10) default 'ABC',
    PRIMARY KEY (student_id, student_number )
);
DESC students05;
INSERT INTO students05 VALUES(1,1);
INSERT INTO students05 VALUES(1,2);
INSERT INTO students05 VALUES(2,1);
INSERT INTO students05 VALUES(2,2);
SELECT * FROM students05;
INSERT INTO students05 VALUES(NULL,NULL);

-- 3) CREATE TABLE에서 고유 키(UNIQUE KEY) 제약 조건 지정
-- 4) CREATE TABLE에서 검사 (CHECK) 제약 조건 지정
DROP TABLE students06;
CREATE TABLE students06(
	student_id		INT 		 ,
    student_number 	VARCHAR(10)  ,
    birthday 		date		,
    unique key (student_id),
    check (birthday >= '2000-01-01')
);
desc students06;
INSERT INTO students06(student_id, birthday) VALUES(1, now());
INSERT INTO students06(student_id, birthday) VALUES(2, now());
INSERT INTO students06(student_id, birthday) VALUES(3, '1999-09-09');
SELECT * FROM students06;

-- 6) CREATE TABLE에서 외래 키 (FOREIGN KEY) 제약 조건 지정
-- FOREIGN KEY(자신의 테이블 컬럼명) REFERENCES 다른테이블 명(다른 테이블의 컬럼명)

DROP TABLE students05;
CREATE TABLE students05(
	student_id		INT 		 AUTO_INCREMENT,
    student_number 	VARCHAR(10) default 'ABC',
    PRIMARY KEY (student_id)
);
DESC students05;
INSERT INTO students05 VALUES(1,1);
INSERT INTO students05 VALUES(2,2);
SELECT * FROM students05;

-- 현재 STUDENT_MY테이블의 STUDENT_ID를 STUDENTS05의 STUDENT_ID로 참조
CREATE TABLE student_my (
	student_id INT NOT NULL,
    FOREIGN KEY (student_id) REFERENCES students05 (student_id)
    );
DESC student_my;
INSERT INTO student_my VALUES(7);
INSERT INTO student_my VALUES(1);
SELECT * FROM student_my;

-- 제약 조건 확인
select * from information_schema.table_constraints
where table_name = 'students06';

select * from information_schema.table_constraints
where table_name = 'students05';

select * from information_schema.table_constraints
where table_name = 'student_my';

-- 07. 제약 조건을 삭제 해보자
select * from information_schema.table_constraints
where table_name = 'students04'; 

alter table students04 drop PRIMARY KEY;
-- 08. 제약 조건을 추가 해보자
select * from information_schema.table_constraints
where table_name = 'students04'; 

alter table students03 ADD CONSTRAINT PRIMARY KEY(student_id);

-- 13.1.9
CREATE TABLE t1 (a INTEGER, b CHAR(10));
ALTER TABLE t1 RENAME t2;
ALTER TABLE t2 MODIFY a TINYINT NOT NULL, CHANGE b c CHAR(20);
ALTER TABLE t2 ADD d TIMESTAMP;
ALTER TABLE t2 ADD INDEX (d), ADD UNIQUE (a);
ALTER TABLE t2 DROP COLUMN c;

desc t2;
SELECT * FROM t2;