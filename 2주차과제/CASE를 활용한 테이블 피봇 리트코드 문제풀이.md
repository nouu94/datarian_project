# 데이터 분석을 위한 중급 SQL - CASE를 활용한 테이블 피봇 리트코드 문제풀이

<br>

<br>

##  Reformat Department Table

| Column Name | Type    |
| ----------- | ------- |
| id          | int     |
| revenue     | int     |
| month       | varchar |

테이블 명 : Department 

테이블의 주요 열과 타입은 위와 같다. 부서 테이블은 각 달에 대한 각각의 부서의 수익 정보를 가지고 있다. month열의 주요 값은 다음과 같다. ["Jan", "Feb", "Mar"..., "Dec"]<br>

각 월에 대한 부서 ID 열과 수익 열이 있도록 테이블을 다시 포맷하는 SQL 쿼리를 작성하세요.

<br>

기존 테이블

| id   | revenue | month |
| ---- | ------- | ----- |
| 1    | 8000    | Jan   |
| 2    | 9000    | Jan   |
| 3    | 10000   | Feb   |
| 1    | 7000    | Feb   |
| 1    | 6000    | Mar   |

<br>

**우리가 만들어야 할 테이블** 

| id   | Jan_Revenue | Feb_Revenue | Mar_Revenue | ...  | Dec_Revenue |
| ---- | ----------- | ----------- | ----------- | ---- | ----------- |
| 1    | 8000        | 7000        | 6000        | ...  | null        |
| 2    | 9000        | null        | null        | ...  | null        |
| 3    | null        | 10000       | null        | ...  | null        |

<br>

<br>

## 나의 풀이

```mysql
SELECT SUM(CASE WHEN month = 'Jan' THEN revenue ELSE NULL END) AS Jan_Revenue
     , SUM(CASE WHEN month = 'Feb' THEN revenue ELSE NULL END) AS Feb_Revenue
     , SUM(CASE WHEN month = 'Mar' THEN revenue ELSE NULL END) AS Mar_Revenue      , SUM(CASE WHEN month = 'Apr' THEN revenue ELSE NULL END) AS Apr_Revenue
     , SUM(CASE WHEN month = 'May' THEN revenue ELSE NULL END) AS May_Revenue
     , SUM(CASE WHEN month = 'Jun' THEN revenue ELSE NULL END) AS Jun_Revenue
     , SUM(CASE WHEN month = 'Jul' THEN revenue ELSE NULL END) AS Jul_Revenue
     , SUM(CASE WHEN month = 'Aug' THEN revenue ELSE NULL END) AS Aug_Revenue
     , SUM(CASE WHEN month = 'Sep' THEN revenue ELSE NULL END) AS Sep_Revenue
     , SUM(CASE WHEN month = 'Oct' THEN revenue ELSE NULL END) AS Oct_Revenue
     , SUM(CASE WHEN month = 'Nov' THEN revenue ELSE NULL END) AS Nov_Revenue
     , SUM(CASE WHEN month = 'Dec' THEN revenue ELSE NULL END) AS Dec_Revenue
FROM Department;
```

해당 문제에 대해서 부서 id 열을 그룹핑 하는 과정을 완성해내지 못함.

<br>

<br>

<br>

<br>

## 선미님의 답안

```mysql
SELECT id
     , SUM(CASE WHEN month = 'Jan' THEN revenue ELSE NULL END) AS Jan_Revenue
     , SUM(CASE WHEN month = 'Feb' THEN revenue ELSE NULL END) AS Feb_Revenue
     , SUM(CASE WHEN month = 'Mar' THEN revenue ELSE NULL END) AS Mar_Revenue
     , SUM(CASE WHEN month = 'Apr' THEN revenue ELSE NULL END) AS Apr_Revenue
     , SUM(CASE WHEN month = 'May' THEN revenue ELSE NULL END) AS May_Revenue
     , SUM(CASE WHEN month = 'Jun' THEN revenue ELSE NULL END) AS Jun_Revenue
     , SUM(CASE WHEN month = 'Jul' THEN revenue ELSE NULL END) AS Jul_Revenue
     , SUM(CASE WHEN month = 'Aug' THEN revenue ELSE NULL END) AS Aug_Revenue
     , SUM(CASE WHEN month = 'Sep' THEN revenue ELSE NULL END) AS Sep_Revenue
     , SUM(CASE WHEN month = 'Oct' THEN revenue ELSE NULL END) AS Oct_Revenue
     , SUM(CASE WHEN month = 'Nov' THEN revenue ELSE NULL END) AS Nov_Revenue
     , SUM(CASE WHEN month = 'Dec' THEN revenue ELSE NULL END) AS Dec_Revenue
FROM Department
GROUP BY id;
```

<br>

<br>

<br>

<br>

## 깨달은 점

SELECT CASE 테이블 피봇과 GROUP BY를 결합하여 기존 id 컬럼과 month + revenue를 결합한 새로운 컬럼을 만들어 테이블 피봇하는 방법을 인지한 좋은 경험이 되었음. 향후 월요일에 수업이 예정된 US E-Commerce Records 2020 데이터 셋을 기반으로 RFM 분석을 할 때 테이블 피봇에 대해 수월하게 수업을 따라 갈 수 있다는 믿음이 생김.