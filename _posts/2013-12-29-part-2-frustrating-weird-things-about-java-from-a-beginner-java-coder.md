---
layout: post
title: "Part 2: Frustrating Weird Things About Java From a Beginner Java Coder"
description: ""
category: ""
tags: ["java","beginner"]
---
{% include JB/setup %}

The learning and frustration continues as I learn more beginner Java this week. I come from a Python background, a high-level dynamic language that had OO features implemented as an after-thought. The road to learning the OO language Java has been not quite as easy as it should be. This blog post as well as the previous one details some of those pain points in my learning process.

I learned some interesting facts about Java:
* Every object inherits from the Object class, which contains in-built methods such as clone(), equals(), finalize(),hasCode(), toString().
* Java has in-built decorators such as @Override, which is a shortcut for over-ride a method from a parent class. You should not override variables, but instead override methods.
* Learning interfaces at Java: packages and how to import them, how to make worldwide unique package names.
* The differences between the abstract class inheritance vs. the interface class inheritance and in what cases you should use each. Abstract class inheritance for specifying NATURE of the object, while interface class inheritance is for specifying CAPABILITY of object. Many stackoverflow discussions have been written just on this topic itself.
* The eternal pains of Comparison Equality.
    The “==” doesn’t  work like it should work in Java. But, NO, it does not! Instead, we have to use the “equals” method. So I tried that to compare two perfectly identical new objects with the same attributes. The result was stilll False. GAH. Lastly, what ultimately worked was to use the hashCode and equala() generator in Java creates @Override decorator function. Subsequently, this mess of code is automatically created for me after right-clicking Source —>Generate hashCode and Equals():

```
@Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((name == null) ? 0 : name.hashCode());
        return result;
    }
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null) return false;
        if (getClass() != obj.getClass()) return false;
        Person other = (Person) obj;
        if (name == null) {
            if (other.name != null) return false;
        } else if (!name.equals(other.name)) return false;
        return true;
    }
All that just to compare two objects to see if they are the same. Then, I use the equals method in a class called “App’, just like before:
public class App {
    public static void main(String[] args) {
        Person person1 = new Person(8 ,"Bob");
        Person person2 = new Person(8,"Bob");
        System.out.println(person1.equals(person2));
    }
}
```

And it finally returned “true”.

```java
The “==” works fine for comparing two integers, but it doesn’t work for doubles. The “==” points to the same object for integers, but points to 2 different objects if they’re doubles. What a pain. Here’s the example:
      Integer num1 = 6;
      Integer num2 = 6;
      System.out.println(num1 == num2); // prints true
      Double value1 = 7.2;
      Double value2 = 7.2;
      System.out.println(value1 == value2); //prints false
```

So, how do you get the double values to be compared as true? The solutions is to use the equals method. Instead of “System.out.println(value1 == value2);”, use “System.out.println(value1.equals(value2));”

Then, the world is turned upside-down again when you try to compare two identical strings using “==”. Gah.

More frustrations to follow in Part 3.