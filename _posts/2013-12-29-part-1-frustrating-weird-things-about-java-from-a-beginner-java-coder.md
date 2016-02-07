---
layout: post
title: "Part 1: Frustrating Weird Things About Java From a Beginner Java Coder"
description: ""
category: "java"
---
{% include JB/setup %}

I’m currently learning Java at work. Going from a language like Python to a pure object-oriented langage like Java has been quite an adjustment to a different mode of thinking and coding. Java has a lot of quirks. Along my learning journey, I’m getting familiar with Eclipse shortcuts.

Here’s a summary of some strange aspects of Java that I’ve learned this week:  
"this" in #Java can be both used when calling a variable and when calling a constructor. The call to the constuctor using "this" must be placed at the very beginning inside the class that which you’re calling the constructor from.
The String is not 1 of the 8 native primitives. String is a class. 
New types of classes: public, private, etc.
Strings are IMMUTABLE. What?! Let me demonstrate string builder and string formatting: 

```java
// String Builder and String Formatting
// This is a VERY Inefficient program below.
String info =””;
info += "My name is Bob.";
info += ””;
info += "I am a builder.";
System.out.println(info);
```

This above is a BAD program. The variable `info` is set to an empty string and will be an empty string for the rest of its life in the program. Then, we’re making an empty string. Then, every time we assign `info`, we’re actually making a whole new string. Therefore, we're increasing space and using memory.
Thus, we have String Builders. Here’s a revised re-write of the above program:

```java
StringBuilder sb = new StringBuilder(””);
sb.append("My name is Sue.");
sb.append(" ");
sb.append("I am a lion tamer.");
System.out.println(sb.toString());
```

The whole point of String Builder is to give a memory-efficient way to build string text. The append method returns a reference to the string builder itself. It’s possible to use method chaining, which is far more efficient and clean. The best version is below:

```java
StringBuilder s = new StringBuilder();
s.append("My name is Roger.").append(””).append("I am a sky diver.");
System.out.println(s.toString());
```

That's all for String Builders.
