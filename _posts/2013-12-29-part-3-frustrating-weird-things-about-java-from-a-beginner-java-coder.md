---
layout: post
title: "Part 3: Frustrating Weird Things About Java From a Beginner Java Coder"
description: ""
category: "java"
---
{% include JB/setup %}

Here’s a summary of basic hasmap or dictionary operations in Java. You have to first declare a dictionary like so:

```java
HashMap<Integer, String> map = new HashMap();
```

Then, you can add keys and their associated values into the dictionary like so:
```java
        map.put(5, "Five");
        map.put(6, "Six");
        map.put(6,"hello");
        map.put(7, "Seven");
        map.put(8, "Eight");
        map.put(9, "Nine");
        map.put(10, "Ten");
```

And you can get a value using a dictionary’s key:
```java
    String text = map.get(6); //get key 6
    System.out.println(text); //prints out that value "Six"
```

The expression for iterating over a dictionary in Java is totally weird and makes no sense at all. To iterate over a dictionary, you do the following:
```java
 for (Map.Entry<Integer, String> entry:map.entrySet()) {
     //OMG. Why is this syntax so weird?
            int key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + " value:" + value);
        }
```
