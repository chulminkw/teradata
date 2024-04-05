# Teradata Studio

### Teradata Studio 개요

- Teradata Stuido 기동
- 오른쪽 하단의 Administation/Query Developement/Data Transfer 의 주제별 메뉴가 있음.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled.png)

- 왼쪽 Navigator에서 Create New Connection Profile 아이콘 클릭.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%201.png)

- Connection Profile Types에 Teradata를 선택하고 Name 에 Express_VM_dbc 를 입력하고 Next 선택

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%202.png)

- Database Server Name에 Express VM 서버의 IP ADDRESS를, User Name에 dbc를 Password에 dbc 입력, Save Password 체크 후 Test Connection 선택하여 제대로 접속이 되는지 확인 후 Finish 선택.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%203.png)

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%204.png)

- 제대로 접속이 안될 경우 ip address가 vm ipaddress와 맞는지 ifconfig 명령어로 확인. /etc/init.d/tpa stop , /etc/init.d/tpa start  명령어로 Teradata Database Initiator service 재기동도 시도.
- Connection Profile 이 왼쪽 메뉴에 생성됨을 확인

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%205.png)

- 오른쪽 상단 메뉴에서 Query Development 탭을 선택

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%206.png)

- 왼쪽 메뉴의 아이콘을 클릭하여 Database Object가 보이도록 Unfold

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%207.png)

- Query Development 창은 크게 SQL Editor, Teradata Result Set Viewer, Teradata SQL History로 구성됨.
- SQL Editor는 수행하려는 SQL을 작성하며, 오른쪽의 초록색 화살표 수행 버튼을 누르면 작성한 SQL의 수행 결과가 Teradata Result Set Viewer에 나타남. 그리고 해당 SQL이 정상적으로 수행 되었는지는 Teradata SQL History에서 알 수 있음.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%208.png)

- 초록색 화살표 버튼은 개별 SQL 문장을 수행하는 Execute as Individual Statements와 SQL Editor 상에 나열되어 있는 모든 SQL을 다 수행하는 Execute ALL 로 구성되어 있음. 수행하려는 개별 SQL 문장 위에 커서를 올려 놓거나 해당 SQL 문장을 Drag로 선택한 후 Execute as Indivisual Statements를 수행하면 선택된 SQL 문장만 수행됨.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%209.png)

### SQL Editor 사용

- 실습용 DB 생성. 이름은 HR로 부여.

```sql
CREATE DATABASE HR
FROM DBC
AS PERM = 20e6     -- 20 MB of permanent space
   SPOOL = 10e6     -- 10 MB of spool space
;
```

- 실습용 User hr_user 생성. Default database는 hr 설정하고 hr DB의 모든 권한을 hr_user 에게 할당.

```sql
CREATE USER hr_user FROM dbc
AS
PASSWORD = "hr_user", -- Replace <YourPasswordHere> with a secure password
PERMANENT = 20e6,               -- Allocation of 10 MB of permanent space
SPOOL = 10e6,                    -- Allocation of 5 MB of spool space
TEMPORARY = 5e6,                -- Allocation of 5 MB of temporary space
DEFAULT DATABASE = hr;

GRANT ALL ON hr TO hr_user WITH GRANT OPTION;
```

- hr_user 사용자로 새로운 Connection Profile을 생성.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2010.png)

- Connection Profile Types를 Teradata로 선택하고 Name을 Express_VM_hr_user로 입력하고 Next 선택

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2011.png)

- Database Server Name에 Express VM IP ADDRESS를 , User Name에 hr_user, Password에 hr_user를 입력한 뒤 Test Connection으로 정상 접속이 되는지 확인한 후 Finish hr_user 용 Connection Profile 생성.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2012.png)

- 왼쪽 Navigator에 새롭게 생성한 Expresss_VM_hr_user가 있음을 확인

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2013.png)

- HR DB를 클릭하여 Unfold하여 HR DB내의 오브젝트 디렉토리 아이콘 확인.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2014.png)

- SQL Editor 탭의 x 를 클릭하여 기존 SQL Editor 창을 종료.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2015.png)

- 오른쪽 상단의 Query Development가 선택되었는지 확인 후 File 메뉴에서 New SQL Editor 선택

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2016.png)

- 새로운 SQL Editor는 Connection Profile이 Express_VM_hr_user 임을 확인.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2017.png)

- 실습에 사용할 테이블 생성.

```sql
-- hr.dept definition
-- DROP TABLE hr.dept;
CREATE TABLE hr.dept (
	deptno integer NOT NULL,
	dname varchar(14) NULL,
	loc varchar(13) NULL,
	description varchar(100) NULL,
	PRIMARY KEY (deptno)
);

-- hr.emp definition
-- DROP TABLE hr.emp;
CREATE TABLE hr.emp (
	empno integer NOT NULL,
	ename varchar(10) NULL,
	job varchar(9) NULL,
	mgr numeric(4) NULL,
	hiredate date NULL,
	sal numeric(7, 2) NULL,
	comm numeric(7, 2) NULL,
	deptno int NULL,
	PRIMARY KEY (empno)
);
```

- insert 로 데이터 입력

```sql
INSERT INTO hr.dept (deptno,dname,loc) VALUES (10,'ACCOUNTING','NEW YORK');
INSERT INTO hr.dept (deptno,dname,loc) VALUES (20,'RESEARCH','DALLAS');
INSERT INTO hr.dept (deptno,dname,loc) VALUES (30,'SALES','CHICAGO');
INSERT INTO hr.dept (deptno,dname,loc) VALUES (40,'OPERATIONS','BOSTON');
	 
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES (7369,'SMITH','CLERK',7902,'1980-12-17',800.00,NULL,20);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7499,'ALLEN','SALESMAN',7698,'1981-02-20',1600.00,300.00,30);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7521,'WARD','SALESMAN',7698,'1981-02-22',1250.00,500.00,30);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7566,'JONES','MANAGER',7839,'1981-04-02',2975.00,NULL,20);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7654,'MARTIN','SALESMAN',7698,'1981-09-28',1250.00,1400.00,30);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7698,'BLAKE','MANAGER',7839,'1981-05-01',2850.00,NULL,30);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7782,'CLARK','MANAGER',7839,'1981-06-09',2450.00,NULL,10);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7839,'KING','PRESIDENT',NULL,'1981-11-17',5000.00,NULL,10);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7844,'TURNER','SALESMAN',7698,'1981-09-08',1500.00,0.00,30);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7900,'JAMES','CLERK',7698,'1981-12-03',950.00,NULL,30);

INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES (7902,'FORD','ANALYST',7566,'1981-12-03',3000.00,NULL,20);
INSERT INTO hr.emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) VALUES 	 (7934,'MILLER','CLERK',7782,'1982-01-23',1300.00,NULL,10);

commit;
```

- Table 생성 후 HR DB를 왼쪽 Navigator에서 생성후 오른쪽 마우스 클릭하여 Refresh 선택하면 생성된 Table이 Navigator에 보임

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2018.png)

### Administration 사용

- 오른쪽 상단의 Administration 탭을 선택하고, 왼쪽 Natigator 메뉴의 Databases를 선택 및 오른쪽 버튼을 누르고 Show Databases 메뉴를 선택하면 오른쪽 Object List Viewer에 현 Database들의 목록이 모두 표시됨.

![Untitled](Teradata%20Studio%207083e76d0add4b2a83fba4eb99faa5c2/Untitled%2019.png)