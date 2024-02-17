## 그룹함수 ROLL UP용례
* 그룹함수 중 가장 많이 쓰이는 함수는 ROLL UP 과 GROUPING SET 이다.  
* 이 중 ROLL UP 을 사용했을 때 서브쿼가 생기는 부분을 자세히 확인해보자  

### 기본 테이블 내용
  
SELECT job,deptno  
FROM EMP e   

![캡처](https://github.com/DogFooter/SQL/assets/106423370/ca9f6e74-bb90-404e-8f9c-1bd160ccfeb0)  

### 일부 컬럼(DEPTNO)만 ROLL UP을 적용시켰을 때 출력 예
   
SELECT job,deptno,sum(sal) AS sum_sal  
FROM EMP e   
GROUP BY job,ROLLUP (deptno)  

![캡처1](https://github.com/DogFooter/SQL/assets/106423370/ab1b0699-3039-4140-92ff-7cb5c14d8a04)  

- 결과 :  DEPTNO에 대한 **SUBTOTAL 생성**. job과 deptno에 대한 **TOTAL 미생성**  
  
### 모든 컬럼(DEPTNO,JOB)을 ROLL UP을 적용시켰을 때 출력 예  
  
SELECT job,deptno,sum(sal) AS sum_sal  
FROM EMP e   
GROUP BY ROLLUP (job,deptno)  
  
![캡처3](https://github.com/DogFooter/SQL/assets/106423370/f0d69d27-1d7f-4637-beae-81089038f4ad)  

- 결과 : ROLLUP 함수의 2번쨰 인자인 DEPTNO에 대한 **SUBTOTAL** 및 job과 deptno에 대한 **TOTAL 모두 생성**  

### 모든 컬럼(DEPTNO,JOB)을 하나의 컬럼으로 묶어서 ROLL UP을 적용시켰을 때 출력 예    
    
SELECT job,deptno,sum(sal) AS sum_sal    
FROM EMP e   
GROUP BY ROLLUP ((job,deptno))  
  
![캡처2](https://github.com/DogFooter/SQL/assets/106423370/7829ab19-7e1a-402b-8fe8-ecc77fcc6b3b)  

- 결과 : job과 deptno 각 개별에 대한 SUBTOTAL 미생성, job과 deptno에 대한 **TOTAL만 생성**   
