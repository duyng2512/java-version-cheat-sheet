# Java 7 Overview
Java 7 release on July 7, 2011 with the following new feature and enhancements:

| Feature List                                                             |
|--------------------------------------------------------------------------|
| [Binary Literals](#binary-literals)                                   |
| [Strings in switch Statements](#strings-in-switch-statements)               |
| [Try-with-resources Statement](#try-with-resources-statement) |
| [Catching Multiple Exception Types and Rethrowing Exceptions with Improved Type Checking](#catching-multiple-exception-types-and-rethrowing-exceptions-with-improved-type-checking)|
| [Underscores in Numeric Literals](#underscores-in-numeric-literals)                                   |
| [Type Inference for Generic Instance Creation](#type-inference-for-generic-instance-creation)                                   |
| [Improved Compiler Warnings and Errors When Using Non-Reifiable Formal Parameters with Varargs Methods](#improved-compiler-warnings-and-errors-when-using-non-reifiable-formal-parameters-with-varargs-methods) |

### Binary Literals
In Java SE 7, the integral types (byte, short, int, and long) can also be expressed using the binary number system. To specify a binary literal, add the prefix **0b or 0B** to the number.

```java

byte aByte = (byte)0b00100001;
short aShort = (short)0b1010000101000101;
int anInt = 0b10100001010001011010000101000101;
long aLong = 0b1010000101000101101000010100010110100001010001011010000101000101L;

```

### Strings in switch Statements
In the JDK 7 release, you can use a String object in the expression of a switch statement:

```java
switch (dayOfWeekArg) {
         case "Monday":
             typeOfDay = "Start of work week";
             break;
         case "Tuesday":
         case "Wednesday":
         case "Thursday":
             typeOfDay = "Midweek";
             break;
         case "Friday":
             typeOfDay = "End of work week";
             break;
         case "Saturday":
         case "Sunday":
             typeOfDay = "Weekend";
             break;
         default:
             throw new IllegalArgumentException("Invalid day of the week: " + dayOfWeekArg);
     }
```

### Try with resources Statement
The try-with-resources statement is a try statement that declares one or more resources. A resource is as an object that must be closed after the program is finished with it. The try-with-resources statement ensures that each resource is closed at the end of the statement. Any object that implements java.lang.AutoCloseable, which includes all objects which implement java.io.Closeable, can be used as a resource.

```java
try (Statement stmt = con.createStatement()) {

      ResultSet rs = stmt.executeQuery(query);

      while (rs.next()) {
        String coffeeName = rs.getString("COF_NAME");
        int supplierID = rs.getInt("SUP_ID");
        float price = rs.getFloat("PRICE");
        int sales = rs.getInt("SALES");
        int total = rs.getInt("TOTAL");
        System.out.println(coffeeName + ", " + supplierID + ", " + price +
                           ", " + sales + ", " + total);
      }

    } catch (SQLException e) {
      JDBCTutorialUtilities.printSQLException(e);
    }
```

### Catching Multiple Exception Types and Rethrowing Exceptions with Improved Type Checking
In Java SE 7 and later, a single catch block can handle more than one type of exception. This feature can reduce code duplication and lessen the temptation to catch an overly broad exception.

```java
/* Before Java 7 */
catch (IOException ex) {
     logger.log(ex);
     throw ex;
catch (SQLException ex) {
     logger.log(ex);
     throw ex;
}

/* After Java 7 */
catch (IOException | SQLException ex) {
    logger.log(ex);
    throw ex;
}
```

### Underscores in Numeric Literals
Java 7 allow underscore in Numeric literals for better readability.

```java
long creditCardNumber = 1234_5678_9012_3456L;
long socialSecurityNumber = 999_99_9999L;
float pi = 	3.14_15F;
long hexBytes = 0xFF_EC_DE_5E;
long hexWords = 0xCAFE_BABE;
long maxLong = 0x7fff_ffff_ffff_ffffL;
byte nybbles = 0b0010_0101;
long bytes = 0b11010010_01101001_10010100_10010010;
```

### Type Inference for Generic Instance Creation
```java
Map<String, List<String>> myMap = new HashMap<String, List<String>>(); // Before java 7
/* In java 7 we can replace constructor generic with empty set of type parameter */
Map<String, List<String>> myMap = new HashMap<>(); // After java 7
```

### Improved Compiler Warnings and Errors When Using Non-Reifiable Formal Parameters with Varargs Methods