---
layout: post
categories: Database
title: "[DB] programmmers 문제풀이 - animal shelter (2)"
date: 2023-09-06
permalink: /database/programmers/03
tags:
  - programmers
---
* content
{: toc}





# Lv3. 오랜 기간 보호한 동물(1)
아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회

```sql
SELECT name, datetime
from animal_ins I
where I.animal_id not in (select O.animal_id from animal_outs O)
order by I.datetime
limit 3
```
  

# Lv3. 없어진 기록 찾기
입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 ID와 이름을 ID 순으로 조회

```sql
SELECT O.animal_id, O.name
from animal_ins I right join animal_outs O
on I.animal_id = O.animal_id
where I.animal_id is null
order by I.animal_id;
```


# Lv3. 있었는데요 없었습니다
보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회

```sql
SELECT I.animal_id, I.name
from animal_ins I
where I.datetime >
	(select O.datetime
	from animal_outs O
	where I.animal_id=O.animal_id)
order by datetime;
```
  

# Lv4. 보호소에서 중성화한 동물

```sql
SELECT O.animal_id, O.animal_type, O.name
from animal_ins I join animal_outs O on I.animal_id = O.animal_id
where substr(I.sex_upon_intake,1,2) != substr(O.sex_upon_outcome,1,2);
```
  

