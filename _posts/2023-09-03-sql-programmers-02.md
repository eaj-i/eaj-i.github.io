---
layout: post
categories: Database
title: "[DB] programmmers 문제풀이 - 아이스크림 가게 관련"
date: 2023-09-06
permalink: /database/programmers/02
tags:
---
* content
{: toc}



```sql
# 모든 레코드 조회하기

SELECT *
from animal_ins
order by animal_id;

  

# 동물의 아이디와 이름
SELECT animal_id, name
from animal_ins
order by animal_id;

  

#이름이 있는 동물의 아이디
SELECT animal_id
from animal_ins
where name is not null
order by animal_id;

  

#이름이 없는 동물의 아이디
SELECT animal_id
from animal_ins
where name is null
order by animal_id;

  

# 역순 정렬하기
SELECT name, datetime
from animal_ins
order by animal_id desc;

  

# 아픈 동물 찾기
SELECT animal_id, name
from animal_ins
where intake_condition = 'sick';

  

# 어린 동물 찾기
SELECT animal_id, name
from animal_ins
where intake_condition != 'aged';

  

# 여러 기준으로 정렬하기

SELECT animal_id, name, datetime

from animal_ins

order by name, datetime desc;

  

# 최댓값 구하기

SELECT max(datetime) as 시간

from animal_ins

order by datetime;

  

#상위 n개 레코드

SELECT name

from animal_ins

where datetime = (select min(datetime)

                  from animal_ins)  

order by datetime ;

  

# 동물 수 구하기

SELECT count(animal_id) count

from animal_ins;

  

# 최솟값 구하기

SELECT min(datetime) 시간

from animal_ins;

  

# 루시와 엘라 찾기

SELECT animal_id, name, sex_upon_intake

from animal_ins

where name in ("Lucy", "Ella", "Pickle", "Rogan", "Sabrina", "Mitty");

  

# 동명 동물 수 찾기

SELECT name, count(animal_id) count

from animal_ins

where name is not null

group by name

having count(animal_id)>=2

order by name;

  

# 입양 시각 구하기(1)

SELECT hour(datetime) hour, count(animal_id) count

from animal_outs

group by hour(datetime)

having hour>=9 and hour<20

order by hour;

  

# 중복 제거하기

SELECT count(distinct name) count

from animal_ins;

  

# 이름에 el이 들어가는 동물 찾기

SELECT animal_id, name

from animal_ins

where lower(name) like lower('%el%')

    and animal_type = 'Dog'

order by name;

  

# DATETIME에서 DATE로 형 변환

SELECT animal_id, name, date_format(datetime, '%Y-%m-%d') as 날짜

from animal_ins

order by animal_id;

  

# 중성화 여부 파악하기

SELECT animal_id, name,

    case when sex_upon_intake

        not like 'Intact%'

        then 'O'

        else 'X'

        end '중성화'

from animal_ins

order by animal_id;

  

# 고양이와 개는 몇 마리 있을까

SELECT animal_type, count(animal_type) count

from animal_ins

group by animal_type

order by animal_type;

  

# 보호소에서 중성화한 동물

SELECT O.animal_id, O.animal_type, O.name

from animal_ins I join animal_outs O on I.animal_id = O.animal_id

where substr(I.sex_upon_intake,1,2) != substr(O.sex_upon_outcome,1,2);

  

# 없어진 기록 찾기

SELECT O.animal_id, O.name

from animal_ins I right join animal_outs O

on I.animal_id = O.animal_id

where I.animal_id is null

order by I.animal_id;

  

# 있었는데요 없었습니다

SELECT I.animal_id, I.name

from animal_ins I

where I.datetime >

    (select O.datetime

    from animal_outs O

    where I.animal_id=O.animal_id)

order by datetime;

  

# NULL 처리하기

SELECT animal_type, case

                        when name is null

                        then 'No name'

                        else name

                        end as name, sex_upon_intake

from animal_ins;

  

# 오랜 기간 보호한 동물(1)

SELECT name, datetime

from animal_ins I

where I.animal_id not in (select O.animal_id from animal_outs O)

order by I.datetime

limit 3
```