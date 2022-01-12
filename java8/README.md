# Java 8 Overview
Java 8 release on March 2014 with the following new feature and enhancements:

| Feature List                                                             |
|--------------------------------------------------------------------------|
| [Default and static methods in Interfaces](#default-and-static-methods-in-interfaces)           |
| [Java Time API](#java-time-api)               |
| [Java IO improvements](#java-io-improvements) |
| [Concurrency API improvements](#concurrency-api-improvements)                                 |
| [Collection API improvements](#collection-api-improvements)                                   |
| [forEach() method in Iterable interface](#foreach-method-in-iterable-interface)                                       |
| [Functional Interfaces and Lambda Expressions](#functional-interfaces-and-lambda-expressions)                         |
| [Java Stream API for Bulk Data Operations on Collections](#java-stream-api-for-bulk-data-operations-on-collections)   |

## Default and static methods in Interfaces
- In java 8, method in interface can have **default** implementation, in stead of force class that implement them to do so. This feature is added for ensure backward compatibility.

- Consider the example below, we have interface **Alert** and class **ControlPanel** implement them :
```java
interface Alert {
    void alarm();
}

class ControlPanel implements Alert {
    @Override
    public void alarm() {
        System.out.println("ACTUNG !");
    }
}
```
- Let assume after reconsidering, owner of **Alert** interface would like to add a new method call **dismiss**:
```java
interface Alert {
    void alarm();
    void dismiss();
}

class ControlPanel implements Alert { // Compile fail
    @Override
    public void alarm() {
        System.out.println("ACTUNG !");
    }
}
```
- Above code will not compile because **ControlPanel** not implement method **dismiss** yet. In order to don't force client code to implement every single method we can use **default** method in interface.
```java
interface Alert {
    void alarm();
    default void dismiss(){
        System.out.println("Dismiss");
    }
}

class ControlPanel implements Alert {
    @Override
    public void alarm() {
        System.out.println("ACTUNG !");
    }
}
```
- This code new work because method **dismiss** now have an implementation, if client code don't intentionally override this method, the default implementation will be used.

- **Note**: If a class implements 2 interfaces and all of them have a default common method than the class have to override and implement the default method itself.

- In addition to declaring default methods in interfaces, Java 8 also allows us to define and implement **static** methods in interfaces. Access this method by using name interface + method name.

```java
public interface Arlam {
    static printArlamMessage(){
        System.out.println("Arlam !");
    }
}

Arlam.printArlamMessage(); // print Arlam !
```

## Java Time API


## Java IO improvements

## Concurrency API improvements

## Collection API improvements

## forEach method in Iterable interface

## Functional Interfaces and Lambda Expressions

## Java Stream API for Bulk Data Operations on Collections