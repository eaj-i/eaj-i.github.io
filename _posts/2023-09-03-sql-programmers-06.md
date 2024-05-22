---
layout: post
categories: Database
title: "[DB] programmmers 문제풀이 - review site"
date: 2023-09-09
permalink: /database/programmers/05
tags:
  - programmers
---
* content
{: toc}





# Lv2. 3월에 태어난 여성 회원 목록 출력하기
생일이 3월인 여성 회원의 ID, 이름, 성별, 생년월일을 조회

```sql
SELECT member_id, member_name, gender , date_format(date_of_birth , '%Y-%m-%d') date_of_birth
from member_profile
where tlno is not null and gender = 'W' and month(date_of_birth) = '3'
order by member_id;
```


# Lv1. 나이 정보가 없는 회원 수 구하기
나이 정보가 없는 회원이 몇 명인지 출력

```sql
SELECT count(user_id) as users
from user_info
where age is null;
```
  

# Lv1. 조건에 맞는 회원수 구하기
2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원이 몇 명인지 출력

```sql
SELECT count(user_id)
from user_info
where age between 20 and 29
	and joined like '2021%';
```
  

  
