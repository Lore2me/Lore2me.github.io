---
layout: post
title: Immutability vs shallow Immutability
date: 2024-06-17 13:34 +0200
categories: [Knowledge, PCP, Programming, Coding]
tags: [pcp, programming, coding, immutability, shallow immutability, java]
description: "In this post we compare Immutability with Shallow Immutability"
---
# Immutability
Immutability is the concept of objects whose state cannot be modified after it is created.
This means that once an object is created, its state cannot be changed.
This is a very useful concept in programming because it helps to avoid bugs
and makes the code easier to understand and maintain.
It's very common in functional programming languages like Haskell, Clojure, and Scala.

The trix is that immutability is not every time possible, so we have to deal with shallow immutability.

Code example:
```java
public class Main {
    public static void main(String[] args) {
        String s = "Hello";
        System.out.println(s); // Hello
        s = s + " World";
        System.out.println(s); // Hello World
    }
}
```
This code generates a String s with the value "Hello",
then concatenates the value " World" to the string s. By the concatenation,
the value of s is a new object with the value "Hello World".
The original object "Hello" cannot be modified.

# Shallow Immutability
Shallow immutability is the concept of objects whose state can be modified, but only at the top level.
This means that you can change the properties of an object, but you cannot change the object itself.
This is a compromise between immutability and mutability, and it is beneficial in practice.
As an example in Java, the String class is immutable, but the StringBuilder class is shallowly immutable.
It Means that you can change the content of a StringBuilder object, but you cannot change the object itself.

Code example:
```java
public class Main {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        System.out.println(sb); // Hello
        sb.append(" World");
        System.out.println(sb); // Hello World
    }
}
```

# Conclusion
Immutability is a powerful concept that can help you write better code.
It makes your code easier to understand and maintain, and it can help you avoid bugs.
However, immutability is not always possible, so you may need to use shallow immutability instead.
