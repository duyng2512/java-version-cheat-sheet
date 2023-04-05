# Java 9 Overview
Java 9 release on 21 September, 2017
 with the following new feature and enhancements: notibly the introduction of **modular system and reactive interface**

| Feature List                                                             |
|--------------------------------------------------------------------------|
| [Java 9 REPL (JShell)](#java-9-REPL-(JShell))           |
| [Factory Methods for Immutable List, Set, Map and Map.Entry](#factory-methods-for-immutable-list-set-map-and-map.entry)           |
| [Modular](#modular)           |
| [Reactive stream](#reactive-stream)           |
| [Stream API improvement](#stream-api-improvement)           |
| [Removal of Dinamond](#remove-of-dinamond)           |



## Java 9 REPL (JShell)
Similar to python shell feature

```java
G:\>jshell
|  Welcome to JShell -- Version 9-ea
|  For an introduction type: /help intro


jshell> int a = 10
a ==> 10

jshell> System.out.println("a value = " + a )
a value = 10

```

## Factory Methods for Immutable List, Set, Map and Map.Entry

Using factory method will create of immutable object.

```java
List immutableList = List.of("one","two","three");
Map nonemptyImmutableMap = Map.of(1, "one", 2, "two", 3, "three")

```

## Modular

```java
module com.foo.bar { }
```

## Reactive stream

```java
java.util.concurrent.Flow
java.util.concurrent.Flow.Publisher
java.util.concurrent.Flow.Subscriber
java.util.concurrent.Flow.Processor
```

## Stream API improvement
- **takeWhile**: loop through stream until an predicate is hit:

```java
Stream.of(1,2,3,4,5,6,7,8,9,10).takeWhile(i -> i < 5 )
                 .forEach(System.out::println);
1
2
3
4
```

- **dropWhile**: constrast of **takeWhile**, remove the stream until an predicate is hit

```java
Stream.of(1,2,3,4,5,6,7,8,9,10).dropWhile(i -> i > 5 )
                 .forEach(System.out::println);
5
6
7
8
9
10
```