# Java 8 Overview
Java 8 release on March 2014 with the following new feature and enhancements:

| Feature List                                                             |
|--------------------------------------------------------------------------|
| [Default and static methods in Interfaces](#default-and-static-methods-in-interfaces)           |
| [Java Time API](#java-time-api)               |
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
- Java 8 introduce new time utility package **java.time** that handle the issue of the old **java.util** package such as:
    - Thread safety.
    - API design and convention.
    - Zone time.
    
- **LocalDate, LocalTime and LocalDateTime** time and date without a time zone base on ISO-8601 standard.

```java
static void testTime(){
        // construct LocalDate
        LocalDate date = LocalDate.of(2021, Month.APRIL, 10);
        printTime(date);
        // construct LocalDate from string
        LocalDate stringDate = LocalDate.parse("2022-01-12");
        printTime(stringDate);
        // tomorrow
        LocalDate tomorrow = LocalDate.now().plusDays(1);
        printTime(tomorrow);

        // now
        LocalTime now = LocalTime.now();
        // construct LocalTime
        LocalTime sixThirty = LocalTime.of(6, 30);
        // construct LocalTime from String
        LocalTime sixThirtyString = LocalTime.parse("06:30");
    }

    static void testZoneTime(){
        Set<String> allZoneIds = ZoneId.getAvailableZoneIds();
        for(String zoneId : allZoneIds.toArray(String[]::new)){
            System.out.println(zoneId);
        }

        ZoneId zoneId = ZoneId.of("Europe/Paris");
        ZonedDateTime zonedDateTime = ZonedDateTime.of(LocalDateTime.now(), zoneId);
    }

    static void testPeriod(){
        LocalDate initialDate = LocalDate.parse("2007-05-10");
        LocalDate finalDate = initialDate.plus(Period.ofDays(5));
        int days = Period.between(initialDate, finalDate).getDays();
        System.out.println("Period " + days);
    }

    static void testDuration(){
        LocalTime initialTime = LocalTime.parse("06:30");
        LocalTime finalTime = initialTime.plus(Duration.ofHours(5));
        long seconds = Duration.between(initialTime, finalTime).getSeconds();
        System.out.println("Duration " + seconds);
    }

    static void testConvertOldDate(){
        Date oldDate = new Date();
        LocalDate newDate = LocalDate.ofInstant(oldDate.toInstant(), ZoneId.systemDefault());
        System.out.println(newDate.toString());
    }
```

## forEach method in Iterable interface
- In java 8, class with **Iterable** interface can use **forEach(Consumer<? super T> action)** in order to perform any action for all elements of collections.

```java
    static void testForEach(){
        List<String> listString = new ArrayList<>(Arrays.asList("TCB", "ACB", "TPC"));
        listString.forEach(System.out::println);
        Set<String> setString = new HashSet<>(Arrays.asList("TCB", "ACB", "TPC"));
        setString.forEach(System.out::println);
    }   
```
## Functional Interfaces and Lambda Expressions

## Java Stream API for Bulk Data Operations on Collections