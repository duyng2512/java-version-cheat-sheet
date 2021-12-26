<style type="text/css">
  body{
  font-family: "Lucida Console", "Courier New", monospace;
  padding: 3em;
}
</style>

# Java 5 Overview
Java 5 release on September 2004, with the following new feature and enhancements:

* Generic
* Enhanced for loop
* Auto boxing and unboxing
* Enum
* Varargs


## Generic
- Java 6 introduce the use of **_Generic_**, using **_Generic_** offer multiple advantages that we will discus this the section bellow.

- In the nutshell, __Generic__ allow **class, interface and method** to be parameterized. For example, consider this dead-simple function:

```java
    static void printInfo(String value){
        System.out.println("Input value is " + value);
        System.out.println("Type of value is " + value.getClass());
    }

```
- Above function simply print the value and the type of input, however we have to specify the type of first argument is __String__, what if input of this function is __int__ or __short__ ?

- One solutions is to use __Object__:
```java
    static void printInfoPrimitive(Object value){
        System.out.println("Input value is " + value);
        System.out.println("Type of value is " + value.getClass());
    }
```

- Or use __Generic__:
```java
    static <E> void printInfo(E value){
        System.out.println("Input value is " + value);
        System.out.println("Type of value is " + value.getClass());
    }
```

- However **Object** is not a good solution when we want to specify argument type is a sub type of __Number__ for example. But with __Generic__ this problems can be solve easily:

```java
    static <E extends Number> void printInfo(E  value){
        System.out.println("Input value is " + value);
        System.out.println("Type of value is " + value.getClass());
    }
```

- The advantages of __Generic__ including:

1. **Stronger type check**: Generic allow compiler applies strong type checking at compile time if the code violates type safety. Checking code at compiled time is easier then run time. 

2. **Elimination of casting**, for example:
```java
/* Non generic code  */
void codeSample(){
    List array = new ArrayList();
    array.add("Hello");
    String value = (String) array.get(0);
}


/* Generic code  */
void codeSample(){
    List<String> array = new ArrayList();
    array.add("Hello");
    String value = array.get(0); // No need to cast here
}

```

3. Allow programmer to write generic code, for example we can have a look at function __add__ of class **java.util.ArrayList** of standard java util package.

```java
    public boolean add(E e) {
        modCount++;
        add(e, elementData, size);
        return true;
    }
```

- We can see in this example, the **add** function don't need to specify every possible type of element to be added, we only need to specify when declare the type of our object
```java
List<String> array = new ArrayList();
```

## Subtyping and wildcards
- If class or interface A extends or implements from class or interface B, then A is Sub type of B, for example:

* Integer is a subtype of Number
* Double is a subtype of Number
* ArrayList<E> is a subtype of List<E>
* List<E> is a subtype of Collection<E>
* Collection<E> is a subtype of Iterable<E>

With the help of generic, we can add constraint to our generic. 

1. For example, we want generic type to be only **sub type of List**.
```java
    static <E extends List<?>> void iterateThroughList(E array){
        for (Object element : array){
            System.out.println(element);
        }
    }
```
Then only implementation of interface __List__ can be used here, for example ArrayList, LinkedList, ... Other type will caused a compiled time error:
```java
List<String> list = new ArrayList<>();
int[] arr = new int[]{1, 2, 3};

iterateThroughList(list); // This is valid code
iterateThroughList(arr); // This will caused compiled time error

```
The keyword __extends__ specify we want to use sub type for generic.

2. In another hand, the keyword __super__ allow us to specify that generic have to be super of a class or interface. For example, this is a util function Collections.copy in standard java.util package:

```java
public static <T> void copy(List<? super T> dest, List<? extends T> src) {};
```

The function indicate that only super type of T is allow to be dest, while subtype of T allow to be source:

```java
List<Integer> integerList = new ArrayList<>(Arrays.asList(1, 2, 3));
List<Number> numberList = new ArrayList<>(Arrays.asList(0, 0, 0));
Collections.copy(numberList, integerList);
```

This code is valid because Number is super type of Integer.

3. Wild card generic, meaning we don't care the type of generic at all, for example:

```java
public boolean removeAll(Collection<?> c) {}
```

The above function remove all elements of collection, thus we don't care about the type of collection.

## Enhanced for loop
Java 5 introduces new language syntax for looping over arrays and collections using for (aka “For-Each” loop.

```java
for (type var: collection){
    // functionality with var
}
```

So instead of this pre version 5:
```java

String[] stringList = new String[]{"A", "B", "C"};
    for (int i = 0; i < stringList.length; i++) {
        System.out.println(stringList[i]);
    }
```

Turn to this
```java
for (String i: stringList) {
    System.out.println(i);
}
```


## Auto boxing and unboxing

**Auto boxing** occurred when java automatically convert a **primitive** (for example int) to its **wrapper class** (Integer), for example:

```java

List<Integer> li = new ArrayList<>();
for (int i = 1; i < 50; i += 2)
    li.add(i); // Autoboxing happen here

```

**Auto boxing** make it convenience for developer, because we do not need to need to explicitly convert to Wrapper class.
```java

List<Integer> li = new ArrayList<>();
for (int i = 1; i < 50; i += 2)
    li.add(Integer.valueOf(i)); // No need to do this

```

**Unboxing** occurred when java automatically convert **a wrapper (for example Integer)** to its primitive type **(int)**.

```java

public static int sum (List<Integer> ints) {
    int s = 0;
    for (int n : ints) { s += n; }
    return s;
}
```


## Enum

- **Enum** introduce as a convenience way to group constant, enum can instantiate as a class, and also have fields and method like a class.

```java
public enum Direction {
    SOUTH, WEST, EAST, NORTH;
}

public static void main(String[] args) {
        Direction direction = Direction.EAST;
        System.out.println(direction);
}
```

- **Enum** support function and field as a normal class:
```java
public enum Direction {
    SOUTH ("S"),
    WEST ("W"),
    EAST ("E"),
    NORTH("N");

    private final String shortcut;
    Direction(String s) {
        this.shortcut = s;
    }

    public String getShortcut() {
        return shortcut;
    }
}

public static void main(String[] args) {
    Direction direction = Direction.EAST;
    System.out.println(direction.getShortcut()); // Return "E"
}

```


## Varargs
Varargs create a convenient way to create function with unknown number arguments or to replace array type arguments, for example:
```java
public void doSomethingFunc(String[] list ){
    for (String i : list){
        // Do some thing with i
    }
}

/* Can be replace with: */
public void doSomethingFunc(String... list){
    for (String i : list){
        // Do some thing with i
    }
}
```