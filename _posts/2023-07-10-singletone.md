---
layout: post
categories: Java
title: (DesignPattern) Singletone
date: 2023-07-10
permalink: /designpattern/singletone
tags:
  - designpattern
  - 생성패턴
---
*content
{:toc}
<!--more-->

> 단 하나의 인스턴스를 보장하는 패턴



![](https://www.plantuml.com/plantuml/png/SoWkIImgAStDuKhEIImkLWZEp4lFIIt9pwlcukJKBORnK3WQca2kTdfgYMSUK7TUSYf8e9RB8JKl1MWG0000)
# Singleton

```java
public class Singleton{
	private static Singleton singleton = new Singleton();
	private Singleton(){
		System.out.println("only one");
	}
	public static Singleton getInstance(){
		return singleton;	
	}
}

```

# Main

```java
public class Main {
	public static void main(String[] args){
		Singleton instance1 = Singleton.getInstance();
		Singleton instance2 = Singleton.getInstance();

		System.out.println(instaince1 == instance2); //true
	}
}
```


# 장점

- 외부에서 생성할 수 없다.
- 고정된 영역에 미리 할당한다.
- 고정된 영역에 할당하기에 메모리를 낭비하지 않는다.
- JVM이 종료되기 전까지 계속 사용할 수 있다.