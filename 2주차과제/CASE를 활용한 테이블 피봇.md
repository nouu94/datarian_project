# 데이터 분석을 위한 중급 SQL - CASE를 활용한 테이블 피봇

<br>

<br>

## 목적

SQL의 테이블 피봇에 대한 정의와 이것을 왜 사용하는지에 대해서 상기시키고자 해당 글을 작성하였다. 

<br>

<br>

## pivot table?

pivot의 영어 사전 뜻은 다음과 같다. 

* 회전하거나 균형을 이룬느 것을 지지하는 고정점 
* 특정 상황에서 가장 중요한 사람이나 사물 

<br>

<br>

**피벗테이블(pivot table)**

**기존 테이블에 여러 데이터 중에서 자신이 원하는 데이터만을 가지고 원하는 행과 열에 데이터를 배치해서 새로운 보고서를 만드는 기능**

<br>

즉, pivot table의 pivot은 영어사전 뜻으로 두번째인 특정 상황에서 가장 중요한 사람이나 사물을 가리키는 것으로 해석될 수 있다.

<br>

<br>

## GROUP BY vs SELECT CASE 테이블 피봇

<br>

### 실습

![products_table](D:\데이터리안숙제\2주차과제\case\products_table.png)

<br>

수업에 진행했던 대로 w3schools에 있는 Products 테이블에서 실습을 진행함. 

<br>

<br>

**GROUP BY 를 이용한 쿼리**

```mysql
SELECT categoryid, AVG(price) AS category_avg_price
FROM Products
GROUP BY categoryid;
```

<br>

**결과**

![products_group_by_result](D:\데이터리안숙제\2주차과제\case\products_group_by_result.png)

<br>

<br>

<br>

<br>

**SELECT CASE 테이블 피봇을 이용한 쿼리**

```mysql
SELECT AVG(CASE WHEN categoryid = 1 THEN price ELSE NULL END) AS category1_avg_price, AVG(CASE WHEN categoryid = 2 THEN price ELSE NULL END) AS category2_avg_price, AVG(CASE WHEN categoryid = 3 THEN price ELSE NULL END) AS category3_avg_price, AVG(CASE WHEN categoryid = 4 THEN price ELSE NULL END) AS category4_avg_price, AVG(CASE WHEN categoryid = 5 THEN price ELSE NULL END) AS category5_avg_price, AVG(CASE WHEN categoryid = 6 THEN price ELSE NULL END) AS category6_avg_price, AVG(CASE WHEN categoryid = 7 THEN price ELSE NULL END) AS category7_avg_price, AVG(CASE WHEN categoryid = 8 THEN price ELSE NULL END) AS category8_avg_price

FROM Products;
```

<br>

**결과**

![category_avg_price_result](D:\데이터리안숙제\2주차과제\case\category_avg_price_result.png)

<br>

### 공통점

GROUP BY와 SELECT CASE 테이블 피봇의 공통점은 기존에 구성되어 있는 하나의 COLUMN을 중심으로 수치 데이터가 있는 COLUMN의 결과를 확인하기 위해 사용됩니다. 

<br>

<br>

즉! 그룹핑을 할 카테고리 열, 수치 데이터를 가진 열 **두개의 열**을 이용하여 테이블을 재정립하는 것이죠. 

<br>

<br>

Products 테이블을 예로 들자면 다음의 열을 선택한 것이군요. 

![products_gg](D:\데이터리안숙제\2주차과제\case\products_gg.png)

<br>

### 차이점 

 쿼리문을 작성 테이블 결과의 차이겠네요.  

![products_group_by_result](D:\데이터리안숙제\2주차과제\case\products_group_by_result.png)

아시다시피 GROUP BY 키워드를 작성하면 categoryID를 기준으로 GROUP BY를 합니다. **그러므로 categoryID의 갯수만큼 행(row)의 갯수가 나오겠네요.** 

<br>

<br>

![category_avg_price_result](D:\데이터리안숙제\2주차과제\case\category_avg_price_result.png)

하지만 SELECT CASE 테이블 피봇은 반대로 categoryID + AVG(price)를 결합하여 SELECT에 새롭게 정의한 categoryX_avg_price라는 열의 갯수만큼 평균 가격을 정의합니다. **그러므로 기존 categoryID + AVG(price)를 결합한 새로운 열인 category_avg_price 라는 8개의 열이 탄생합니다.** 

<br>

<br>

이것이 GROUP BY와 SELECT CASE를 이용한 테이블 pivot의 가장 큰 차이점이라고 생각합니다. 여러가지 다른 차이점도 분명히 있겠지만 본질은 이것이며, 월요일 수업 전 해당 차이점만 이해한다면 수업을 따라가는데 도움이 많이 될 것 같아 작성합니다.
