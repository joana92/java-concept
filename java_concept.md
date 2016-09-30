# Java Concept Questions

Contents:

- [Keywords & data type](#Keywords)
- [Concepts](#Concepts)
- [OOP](#OOP)
- [Collections](#Collections)
- [Threading, Lock](#Thread)
- [Memory & Garbage Collection](#java memory & garbage)
- [application](#application)


## Object Oriented

+ treat the word as a combination of class
+ model organized around objects rather than actions and data rather than logic
+ based on the concept of "objects"
+ contain data in the form of fields(attributes)
+ code in the form of procedures(methods)
+ object's procedures can access and modify the data fields of the associated object

<a name="Keywords"/>

## Java Keywords

+ Primitive Data Type

  | data type | number of bytes | range |
  | -------- | ---------------- | --------------------------- |
  | int    |         32 bits 4 bytes        |         [-2^31, 2^32-1]      |
  | long   |         8 bytes            |         [-2^63, 2^63-1]          |
  | float  |         4 bytes            |          [-Float.MAX_VALUE, Float.MAX_VALUE], Float.MAX_VALUE= 2^128-1 |
  | double|         8 bytes            |     Double.MAX_VALUE = 2^1024 -1 |  
  
  int and long can be describled by 2^n, because one is 32 bits and another is 64 bits. However, float and double can not be describled in this way, because they use  IEEE 754 standar.
  
+ Refrence Data Type
  
+ Access modifiers

  | modifier | access in same package | access in different package |
  | -------- | ---------------------- | --------------------------- |
  | private  |         no             |          no                 |
  | public   |         yes            |         yes                 |
  | default  |         yes            |          no                 |
  | protected|         yes            |     only if extend class    |  
  
+ `final` keyword
  - can be assigned to variable, method, class, object
  - if assigned
    - variable: behave like a constant and cannot change value
    - method: cannot be overridden in its child class
    - class: no other class can extend it
    - object: only instantiated once

+ `synchronized` keyword
   - provide lock on the object and prevent race condition
   - can be applied to static/non-static methods or block of code
   - only one thread at a time can access synchronized methods
   - if multiple threads, need to wait for execution complete
   
+ `volatile` keyword
   - volatile variable stored in main memory
   - every thread can access 
   - local copy updated from main memory
   - has performance issues
   
+ `static` variable
   - everything declared as `static` is related to class not object
   - multiple objects of a class share the same instance of static variable
   
+ `static` method
   - can be accessed without creating the objects
   - use class name to access static method
   - static method can only access static variables and not local or global non-static variable: because if the class is not instantiated and therefore the variables are not initialized and cannot be accessed from a static method
   - static method can only call static methods and not non-static methods
   - non-static methods can call static methods
   
+ `static` class
  - class cannot be declared as static
  - class is static if all variables and methods are static and constructor is private, so the only way to access is to use class name 

+ `throw` keyword
  - throw exception manually
  - used when program fails the condition and wants to give warning
  - throw the exception from a method to the calling method
  - calling method can decide to handle exception or throw to its calling method

  
  
<a name="Concepts"/>

## Concepts
+ object vs. class
  - an object is an instance of a class
    + object refers to an actual instance of a class
    + every object must belong to a class
    + objects are created and then destroyed, only live in the program for limited time
  - objects have a lifespan but classes do not
    + properties of objects can change while they live

+ `private constructor`
  - two main features
    - a class with private constructor cannot be inherited 
    - we cannot create a object od the class with private constructor
    - we donot want to create the instance of the class for protection
  
+ `static` and `instance` method
   - instance method
     - belong to the instance of a class and require the instance before it can be called
     - dynamic binding
     - JVM selects the method to invoke based on the type of object reference, known at run time 
   - static method
     - belong to the class itself
     - static binding 
     - JVM selects the method to invoke based on the actual class of the object, known at compile time
     
+ `abstract` class and `interface`
   - abstract class
     + contain at least one abstract method
     + can contain numbers of concrete methods
     + variable can be `public`, `private`,`protected`, `default`, or constants
     + a class can only extend one abstract class
     + not compulsory to implement all methods
     + if want to add a new feature, simply implement in the abstract class and call it from subclass
   - interface
     + only contain abstract methods
     + variable is by default `public final`, only has constants
     + a class can implement multiple interfaces
     + compulsory to implement all methods
     + if want to add a new feature, need to implement the method in all classes implementing the interface
     
+ `instanceof` and `isInstance(Object obj)`
   - `instacneof` is a keyword but `isInstance()` is a method
   - `instanceof` check whether the object is type of particular class or subclass
   - `isInstance()` only used to identify if object is of a particular class
   
+ pass by value and pass by reference
  - Java only supports pass by value, actual value is passed
  - Java passes the references by value, the pointer to the object is passed as value
  - references passed to the method are actually copies of the original references
  
+ `==` and `equals()`
  - `==` is used to compare the references of the objects
  - `equals()` can compare the values of two objects
  
+ `StringBuffer` vs `StringBuild` vs `String`
  - `StringBuffer` is synchronized but `StringBuild` is not
  - `String` is an immutable object which means the value cannot be changed where as `StringBuffer` is mutable. 
  - `StringBuffer` and `StringBuilder` classes are used when there is a necessity to make a lot of modifications to Strings of characters.
  
+ `final`, `finally`,`finalize()`
  - `final`: a final variable acts like constant, a final method cannot be overridden, a final class is immutable
  - `finally`: handles exception, clean up after try block
  - `finalize()`: method helps in garbage collection, invoked before an object is discarded by the garbage collector, allowing it to clean up its state
  
+ static block and init block
  - static block is loaded when class is loaded by JVM for the first time
  - init block is loaded every time the class is loaded
+ object reflections
  - provide a way to get reflective information of class and object
  - perform operations such as
    + get information about methods and fields present inside the class at runtime
    + get a new instance of a class
    + get and set object fields directly by getting field reference, regardless what the access modifier is
  - advantage
    + help in observing or manipulating runtime behavior
    + help in debugging or testing programs
    + can call method by name when we do not know the method in advance  
+ explain why java main function is `public static void main(String[]args)`
  - public is a Aceessor Modifer. It means the main() function can be called from anywhere.
  - static make the main() function can be called without instanlizing this class
  - void mean the return type of main() function. main function return void(nothing)
  - main is the keyword searched by JVM as the start of the application
  - args is the paprameter for the main function
  
  
<a name="OOP"/>

## OOP
+ polymorphism
  - define more than one function with the same name
  - compile time polymorphism(overloading) and runtime polymorphism(overriding)
  - method override: a class method has same name and signature as a method in parent class, JVM determines the proper method to call at runtime
  - method overloading: method with same name but different signature, determined at compile time
  
+ inheritance
  - allow a child class to inherit some properties from its parent class
  - use `extends` keyword
  - only public and protected access modifiers can be accessed in child class
  
+ multiple inheritance
  - _*Java does not support multiple inheritance*_ (Java can only inherite one class but it can implement multi-interfaces)
  - diamond problem
  - use of multiple interfaces (or extend a class and implement some interfaces)
  
    ```
      interface A{
         add();
      }
      interface B{
         add();
      }
      class C implements A,B{
         add();
      }
     ```
+ abstraction
  - convert real world objects in terms of class
  - Different between `abstract class` and `concrete class`
  
+ encapsulation
  - achieved by combining the methods and attribute into a class
  - class acting like a container encapsulation the properties
  - hide how things work and expose the user requests
  

<a name="Collections"/>

## Collections
+ ArrayList and vector
  - synchronization
    + ArrayList is not thread-safe but vector is 
    + each method in vector class is surrounded by a synchronized block
  - data growth
    + both use arrays to store contents
    + enlarge array if not enough space
  - performance
    + vector is slower than arraylist because of thread-safe
    
+ Sort objects in lists
  - implement Comparable interface for the object class and override compareTo() method
  - if object class is a jar file, create Comparator and override compare() method
  - call Collection.sort()
  
+ HashMap and HashTable
  - HashMap is not synchronized but HashTable is
  - use Iterator for HashMap(fail-safe) and enumerator for Hashtable(not fail-safe)
  - HashMap allows null values and only one null key; Hashtable does not allow null key or null value
  
+ List interface
  - ArrayList
    + resizable array implementation
    + dynamic size
    + not thread-safe
    + time compelxity: contains,delete (O(n)); others (O(1))
  - Vector
    + ArrayList implementation
    + thread-safe
  - LinkedList
    + also implements Queue interface
    + FIFO
    + faster for insertion and deletion
    + Time complexity: get, contain(O(n)); others (O(1))
  
+ Arrays and ArrayList
  - arrays are fixed size but ArrayLists are dynamic
  - elements in the array list can be added or removed at runtime
  - array contains elements of same type but arraylist can contain elements of different type
  
+ ArrayList and LinkedList
  - both fast in insertion, inserting into arraylist and into first position of linkedlist takes O(1) time
  - random lookup (get, set)in ArrayList is fast, but slow for LinkedList. It needs to move point in linkedlist.
  - remove is slow for ArrayList(elements need to be shifted) but fast for LinkedList
  
  Follow up: a sorted numbers, do binary search, which one is faster? arraylist or linkedlist?
  Answer: ArrayList, because it is faster in random get a element at certain index.
  Follow up: which one is better if I need frequenctly add or remove elements?
  Answer: LinkedList, because elements need to be shifted in arraylist, which means it will cost lots of time in moving and coping element. In linkedlist, cost in adding an element is fixed.
  
    
+ Set interface
  - SortedSet
    + interface extends Set
    + allow data to be sorted
    + all elements inserted must implement Comparator or Comparable interface
  - TreeSet
    + implementation of SortedSet interface
    + O(logn) time for add, remove, contains operations
    + not synchronized
  - HashSet
    + implements Set interface
    + back up by hash table
    + no guarantee on constant order
    + allow null element
    + O(1) time for add,remove,contains
    + O(h/n) for next
    

+ Advantage of iterator
   - used when no clue about object type
   - iterator allows updates
   
+ Preferred declaration
  - `List<String> list = new ArrayList<String>()` not `ArrayList<String> list = new ArrayList<String>()`
  - because function may take List as parameter
  - more flexible
  
+ Iterator access and index access
  - insert,update,or delete is faster for iterator access for elements in between the structure
  - insert,update,or delete is faster for index access for elements at the end
  - search is fast for index access
  

<a name="Thread" />

## Threading

+ Thread vs. Process
  - definition
    + process: executing instance of an application
    + thread: a path of execution within a process
  - relationship
    + a process can contain multiple threads
    + thread considered as lightweight process
  - comparison
    + thread for small tasks, process for heavy tasks
    + thread within the same process share the same address space(allow threads to read and write data to the same structures and variables, allow communication between threads), but different processes do not
    + threads are easier to create than processes because they do not require a separate address space
    + multi-threading: be careful that threads share structures that should be modified by one thread at a time
    + processes are independent of each other
    
+ Lock, DeadLock
    - When one thread wants to obtain access to an object, it requires a lock for that object.
    - DeadLock: occus when two or more threads are bocked, each waiting for a resouce held by the other thread/threads. 
    - When this happens, there is no possibility of the threads ever making forward progress unless some outside agent takes action to break deadlock
  - What will hanpend if too many locks in program?
  
<a name="java memory & garbage" />

## java memory & garbage

+ java memory management

Normally, java memory include: register, heap, stack.
Stack: primitive data type, object reference(objects live in stack, the references are stored in stack)
Heap: store the producted data by "new"
The speed in stack is faster than heap. The data stored in stack could be shared
  - objects live in heap, and mehods and local variables live in stack. 
  - object reference variables live on the stack but as a reference to the object(???)
+ Garbage Collection
  - aims to collect unreachable objects in heap
  - all objects are garbage-collectable on the heap
  - local bariables are declared inside a method. They are temporary. They only live as long as the method is on the stack

<a name="application" />

## java in industry application

+ difference between different Java version

  

  
