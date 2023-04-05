# Java 10 Overview
Java 10 release on March 20, 2018 with the following new feature and enhancements: notibly the introduction of **var keyword and container aware flag**

| Feature List                                                             |
|--------------------------------------------------------------------------|
| [var keyword](#var-key-word)           |
| [Container awareneess](#container-awareness)           |

## Var keyword

Java 10 relase new **var** keyword for short interpretation

```java

public void func() {
    var x = 10;
}

```
- **var** only can use as local variable in function, it can not be null, not be declared, and not be property.


## Container awareness
- Now JVM can aware of number of cores and memory size inside a container
