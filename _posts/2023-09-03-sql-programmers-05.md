---
layout: post
categories: Database
title: "[DB] programmmers 문제풀이 - on/offline shopping mall"
date: 2023-09-09
permalink: /database/programmers/05
tags:
---
* content
{: toc}

<!--more-->


# Lv1. 가장 비싼 상품 구하기
 판매 중인 상품 중 가장 높은 판매가를 출력
 
```sql
SELECT max(price) as max_price
from product;
```


# Lv2. 상품 별 오프라인 매출 구하기
상품코드 별 매출액(판매가 * 판매량) 합계를 출력 
(매출액을 기준으로 내림차순 정렬, 매출액이 같다면 상품코드를 기준으로 오름차순 정렬)
  
```sql
SELECT P.product_code, sum(P.price*O.sales_amount) sales
from product P join offline_sale O
on P.product_id = O.product_id
group by P.product_code
order by sales desc, P.product_code;
```

# Lv4. 년, 월, 성별 별 상품 구매 회원 수 구하기
년, 월, 성별 별로 상품을 구매한 회원수를 집계 (년, 월, 성별을 기준으로 오름차순 정렬, 성별 정보가 없는 경우 결과에서 제외)

```sql
SELECT year(O.sales_date) year, month(O.sales_date) month, U.gender, count(distinct O.user_id) users
from user_info U join online_sale O
on U.user_id = O.user_id
where U.gender is not null
group by year, month, U.gender
order by year, month, U.gender;
```
  



  

# Lv2. 카테고리 별 상품 개수 구하기
상품 카테고리 코드(`PRODUCT_CODE` 앞 2자리) 별 상품 개수를 출력 
(상품 카테고리 코드를 기준으로 오름차순 정렬)

```sql
SELECT substr(product_code, 1, 2) category, count(product_code) products
from product
group by category
order by product_code;
```

# 가격대 별 상품 개수 구하기

SELECT case when price < 10000 then '0'

            when price < 20000 then '10000'

            when price < 30000 then '20000'

            when price < 40000 then '30000'

            when price < 50000 then '40000'

            when price < 60000 then '50000'

            when price < 70000 then '60000'

            when price < 80000 then '70000'

            when price < 90000 then '80000'

            else  '90000' end price_group, count(product_id) products

from product

group by price_group

order by price_group;

  

# 년, 월, 성별 별 상품 구매 회원 수 구하기

SELECT year(O.sales_date) year, month(O.sales_date) month, U.gender, count(distinct O.user_id) users

from user_info U join online_sale O

on U.user_id = O.user_id

where U.gender is not null

group by year, month, U.gender

order by year, month, U.gender;

  

# 상품 별 오프라인 매출 구하기

  

SELECT P.product_code, sum(P.price*O.sales_amount) sales

from product P join offline_sale O

on P.product_id = O.product_id

group by P.product_code

order by sales desc, P.product_code;

