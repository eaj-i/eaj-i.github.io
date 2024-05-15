---
layout: post
categories: Database
title: "[DB] programmmers 문제풀이 - car rental company"
date: 2023-09-09
permalink: /database/programmers/04
tags:
---
* content
{: toc}





# Lv1. 특정 옵션이 포함된 자동차 리스트 구하기
네비게이션' 옵션이 포함된 자동차 리스트 출력 (자동차 ID를 기준으로 내림차순 정렬)

```sql
SELECT *
from car_rental_company_car
where options like '%네비게이션%'
order by car_id desc;
```
  
# Lv1. 평균 일일 대여 요금 구하기
자동차 종류가 'SUV'인 자동차들의 평균 일일 대여 요금을 출력

```sql
SELECT round(avg(daily_fee)) as average_fee
from car_rental_company_car
group by car_type
having car_type='SUV';
```

# Lv2. 자동차 평균 대여 기간 구하기
평균 대여 기간이 7일 이상인 자동차들의 자동차 ID와 평균 대여 기간 리스트 출력
(평균 대여 기간은 소수점 두번째 자리에서 반올림, 결과는 평균 대여 기간을 기준으로 내림차순 정렬, 평균 대여 기간이 같으면 자동차 ID를 기준으로 내림차순 정렬)

```sql
select car_id, round(avg(datediff(end_date,start_date)+1),1) average_duration
from car_rental_company_rental_history
group by car_id
having avg(datediff(end_date,start_date)+1) >=7
order by average_duration desc, car_id desc;
```


# Lv2. 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기
'통풍시트', '열선시트', '가죽시트' 중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지 출력
(자동차 수에 대한 컬럼명은 `CARS`로 지정하고, 결과는 자동차 종류를 기준으로 오름차순 정렬)

```sql
SELECT car_type, count(car_id) cars
from car_rental_company_car
where options like '%시트%'
group by car_type
order by car_type
```


# Lv3. 대여 기록이 존재하는 자동차 리스트 구하기
자동차 종류가 '세단'인 자동차들 중 10월에 대여를 시작한 기록이 있는 자동차 ID 리스트를 출력
( 자동차 ID 리스트는 중복이 없어야 하며, 자동차 ID를 기준으로 내림차순 정렬)

```sql
SELECT distinct R.car_id
from car_rental_company_rental_history H join car_rental_company_car R
on R.car_id = H.car_id
where R.car_type='세단' and month(start_date) = 10
order by R.car_id desc;
```


  

  



  

