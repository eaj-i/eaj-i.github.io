---
layout: post
categories: Database
title: "[DB] programmmers 문제풀이 - animal shelter (1)"
date: 2023-09-06
permalink: /database/programmers/02
tags:
---
* content
{: toc}






# Lv1. 모든 레코드 조회하기

```sql
SELECT *
from animal_ins
order by animal_id;
```
  

# Lv1. 동물의 아이디와 이름
동물 보호소에 들어온 모든 동물의 아이디와 이름을 ANIMAL_ID순으로 조회

```sql
SELECT animal_id, name
from animal_ins
order by animal_id;
```
  

# Lv1. 아픈 동물 찾기
동물 보호소에 들어온 동물 중 아픈 동물의 아이디와 이름을 조회

```sql
SELECT animal_id, name
from animal_ins
where intake_condition = 'sick';
```



# Lv1. 어린 동물 찾기
동물 보호소에 들어온 동물 중 젊은 동물의 아이디와 이름을 조회

```sql
SELECT animal_id, name
from animal_ins
where intake_condition != 'aged';
```


# Lv1. 이름이 있는 동물의 아이디
동물 보호소에 들어온 동물 중, 이름이 있는 동물의 ID를 조회

```sql
SELECT animal_id
from animal_ins
where name is not null
order by animal_id;
```
  

# Lv1. 이름이 없는 동물의 아이디
동물 보호소에 들어온 동물 중, 이름이 없는 채로 들어온 동물의 ID를 조회

```sql
SELECT animal_id
from animal_ins
where name is null
order by animal_id;
```
  

# Lv1. 역순 정렬하기
동물 보호소에 들어온 모든 동물의 이름과 보호 시작일을 조회
단, ANIMAL_ID 역순으로

```sql
SELECT name, datetime
from animal_ins
order by animal_id desc;

```

# Lv1. 여러 기준으로 정렬하기
동물 보호소에 들어온 모든 동물의 아이디와 이름, 보호 시작일을 이름 순으로 조회
 단, 이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저

```sql
SELECT animal_id, name, datetime
from animal_ins
order by name, datetime desc;
```

# Lv1. 상위 n개 레코드

```sql
SELECT name
from animal_ins
where datetime = (select min(datetime)
                  from animal_ins)  
order by datetime ;
```

# Lv1. 최댓값 구하기
가장 최근에 들어온 동물은 언제 들어왔는지 조회

```sql
SELECT max(datetime) as 시간
from animal_ins
order by datetime;
```
  

# Lv2. 최솟값 구하기
동물 보호소에 가장 먼저 들어온 동물은 언제 들어왔는지 조회

```sql
SELECT min(datetime) 시간
from animal_ins;
```

# Lv2. 동물 수 구하기
동물 보호소에 동물이 몇 마리 들어왔는지 조회

```sql
SELECT count(animal_id) count
from animal_ins;
```


# Lv2. 동명 동물 수 찾기
동물 보호소에 들어온 동물 이름 중 두 번 이상 쓰인 이름과 해당 이름이 쓰인 횟수를 조회

```sql
SELECT name, count(animal_id) count
from animal_ins
where name is not null
group by name
having count(animal_id)>=2
order by name;
```


# Lv2. 이름에 el이 들어가는 동물 찾기

```sql
SELECT animal_id, name
from animal_ins
where lower(name) like lower('%el%')
and animal_type = 'Dog'
order by name;
```

# Lv2. 입양 시각 구하기(1)
 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회

```sql
SELECT hour(datetime) hour, count(animal_id) count
from animal_outs
group by hour(datetime)
having hour>=9 and hour<20
order by hour;
```

# Lv2. 루시와 엘라 찾기
동물 보호소에 들어온 동물 중 이름이 Lucy, Ella, Pickle, Rogan, Sabrina, Mitty인 동물의 아이디와 이름, 성별 및 중성화 여부를 아이디 순으로조회

```sql
SELECT animal_id, name, sex_upon_intake
from animal_ins
where name in ("Lucy", "Ella", "Pickle", "Rogan", "Sabrina", "Mitty");
```
  
# Lv2. 중복 제거하기

동물 보호소에 들어온 동물의 이름은 몇 개인지 조회 (이름이 NULL인 경우는 집계하지 않으며 중복되는 이름은 하나로 침)
```sql
SELECT count(distinct name) count
from animal_ins;
```
  

# Lv2. DATETIME에서 DATE로 형 변환
`ANIMAL_INS` 테이블에 등록된 모든 레코드에 대해, 각 동물의 아이디와 이름, 들어온 날짜[1](https://school.programmers.co.kr/learn/courses/30/lessons/59414#fn1)를 조회

```sql
SELECT animal_id, name, date_format(datetime, '%Y-%m-%d') as 날짜
from animal_ins
order by animal_id;
```
  

# Lv2. 중성화 여부 파악하기
동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회

```sql
SELECT animal_id, name,
	case when sex_upon_intake
		not like 'Intact%'
		then 'O'
	else 'X'
	end '중성화'
from animal_ins
order by animal_id;
```
  

# Lv2. 고양이와 개는 몇 마리 있을까
동물 보호소에 들어온 동물 중 고양이와 개가 각각 몇 마리인지 조회

```sql
SELECT animal_type, count(animal_type) count
from animal_ins
group by animal_type
order by animal_type;
```


# Lv3. 오랜 기간 보호한 동물(1)
아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회

```sql
SELECT name, datetime
from animal_ins I
where I.animal_id not in (select O.animal_id from animal_outs O)
order by I.datetime
limit 3
```
  


# Lv2. NULL 처리하기
동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회 (이름이 없는 동물의 이름은 "No name"으로 표시)

```sql
SELECT animal_type, 
	case
		when name is null
		then 'No name'
	else name
	end as name, sex_upon_intake
from animal_ins;
```
  
