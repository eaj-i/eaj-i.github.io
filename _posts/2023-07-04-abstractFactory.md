---
layout: post
categories: Java
title: (DesignPattern) AbstractFactory
date: 2023-07-03
permalink: /designpattern/abstract-factory
tags:
  - designpattern
  - 생성패턴
---
*content
{:toc}





> 관련성을 갖는 객체들 또는 독립적인 객체들의 집합을 생성할 수 있는 인터페이스를 제공하는 생성 패턴




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