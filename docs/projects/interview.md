---
sidebar_label: "Intervie Questions"
sidebar_position: 1
tags: [.Net Core, C#, React, EF, Postgres]
---
# Interview Questions
## What is the difference between the readonly and const on C#

> readonly and cosnt are ways to declare properties that can not be updated but it has a diferent implementations.

> readonly can be declared without value and can be initiali on the contructor ex.

> const need to be declared and added the value in the same time

Initialization: A const variable must be initialized with a value at the time of declaration, whereas a readonly variable can be initialized either at the time of declaration or in a constructor.

Scope: const variables are implicitly static and have a global scope, which means they can be accessed from anywhere within the program. readonly variables, on the other hand, can have different values for each object instance and are not necessarily static.

Usage: const variables are used to represent values that are constant and known at compile time, such as mathematical constants or fixed string values. readonly variables are used to represent values that are not known at compile time, but are still constant for the lifetime of the object, such as configuration settings or runtime constants.

```csharp
public class MyClass
{
    public const int MyConstant = 100; // must be initialized here

    public readonly int MyReadonly;

    public MyClass(int value)
    {
        MyReadonly = value; // can be initialized in constructor
    }
}

```
## SOLID Principes

## Indexs on SQL 

## How optimized a Query 

## Entity Graph
## Async en C#


## SQL Joins
```sql

select T1.id  Group by (T2.id) whre
 inner join
// left t1 t2
// right t1 t2


//
```

## SQL GROUP BY
```sql

select T1.id  Group by (T2.id) whre
 inner join
// left t1 t2
// right t1 t2


//
```
## SQL max
## SQL 
## SQL and C# node js insert

