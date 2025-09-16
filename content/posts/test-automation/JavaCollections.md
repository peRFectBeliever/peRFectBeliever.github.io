
+++
authors = ["Devendran Nehru"]
title = "Java Collections - Complete Guide"
date = "2025-09-16"
description = "Java Collections One Stop Solution"
tags = [
    "SDET",
    "automation",
    "java",
]
categories = [
    "QA",
    "Automation",
]
series = ["Programming Basics"]
+++

# Collections Framework

#### Why we need Collection Framework required?
Before Collection Framework (or before JDK 1.2) was introduced, the standard methods for grouping Java objects (or collections) were **Arrays or Vectors, or Hash tables**. All of these collections had **no common interface**.
Those objects 

Generics, Functional Interfaces and Streams enhanced the usability of Collection interface in java

### Core Collection Interfaces
These interfaces define the fundamental behavior of different types of collections. 
**Collection: ** The root interface of the collection hierarchy, representing a group of objects. It extends the Iterable interface. 
**Set** Represents a collection that does not allow duplicate elements. 
**List** Represents an ordered collection (a sequence) that allows duplicate elements. 
**Queue** Represents a collection used for holding elements prior to processing. It typically stores elements in a FIFO (First-In, First-Out) order. 
**Deque** (Double-Ended Queue): Allows insertion and deletion of elements at both ends, providing more flexible operation than a standard queue. 
Interfaces for Ordered Data

### Interfaces for sorted or ordered data structures

**SortedSet**: A Set that additionally maintains its elements in sorted order. 
**NavigableSet**: A SortedSet that provides methods to navigate within the set, such as retrieving elements closest to a given key. 
**SortedMap**: A Map that also maintains its key-value pairs in sorted order based on the keys. 
**NavigableMap**: A SortedMap that provides methods for efficient navigation of the key-value pairs. 

### The Map Interface
This interface **does not extend the Collection interface** but represents a distinct entity in the framework. 
Map: Represents an object that maps keys to values. Each key in a Map must be unique.


![](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*qgcrVwo8qzF4muOQ-kKB8A.jpeg)

---
### List Interface

In Java, a List is an **ordered collection of elements** that **allows duplicates** and provides methods for interacting with elements based on their position (index). You cannot directly create a  `List`  object because  `List`  is an interface. Instead, you instantiate a class that implements the  `List`  interface. The most common implementations are  `ArrayList`  and  `LinkedList`.

Creating a  `List`  in Java

Here's how to create different types of  `List`  objects:

-   **Using  `ArrayList`  (most common and versatile):**

    ```
    List<String> fruits = new ArrayList<>(); // Creates an empty ArrayList of Strings
    
    ```
    You can also initialize it with values:
    ```
    List<String> fruits = new ArrayList<>(Arrays.asList("Apple", "Banana"));
    
    ```

-   **Using  `LinkedList`  (for frequent insertions/deletions at the ends):**

    ```
    List<String> names = new LinkedList<>(); // Creates an empty LinkedList of Strings
    
    ```
    
-   **Using  `Arrays.asList()`  (for fixed-size lists backed by an array):**

    ```
    List<String> colors = Arrays.asList("Red", "Green", "Blue"); // Creates a fixed-size list
    
    ```

    
    Note that the list created by  `Arrays.asList()`  is **mutable in terms of modifying existing elements**, but you cannot add or remove elements after creation.
-   **Using  `List.of()`  (Java 9+, for immutable lists):**

    ```
    List<String> immutableList = List.of("One", "Two", "Three"); // Creates an immutable list
    
    ```

#### Differences between  `ArrayList`  and  `LinkedList`

The choice between  `ArrayList`  and  `LinkedList`  depends on your specific use case and the operations you need to perform frequently.

| Feature| ArrayList|LinkedList|
|--|--|--|
| Underlying Data Structure |Uses a dynamic array |Uses a doubly linked list|
|Random Access (getting elements by index)|Faster (O(1) time complexity) because elements are stored contiguously in memory and can be accessed directly.|Slower (O(n) time complexity) as it requires traversing the list from the beginning or end to reach the desired element.|
|Insertion and Deletion|Slower, especially in the middle of the list, as elements need to be shifted to make or fill gaps (O(n) time complexity).|Faster, especially for insertions and deletions at the beginning or end of the list, as it only requires updating pointers (O(1) time complexity).|
|Memory Usage|Can have lower memory overhead if the initial capacity is chosen carefully. However, resizing can lead to temporary memory spikes.|Has higher memory overhead per element due to storing references to the previous and next nodes|
|Use Cases|Best suited for scenarios where fast random access is crucial, and insertions/deletions are infrequent, like accessing elements in a log file.|Better suited for scenarios with frequent insertions/deletions at the beginning or end of the list, like implementing queues or stacks.|
----


What is cache locality?
**Cache locality** (also called **locality of reference**) is a concept from **computer architecture** and **memory performance**. It refers to how well a program's memory access pattern matches the way the **CPU cache** works.
There are two main types:

**1. Spatial Locality**
If a program accesses a memory location, it's likely to access **nearby memory locations** soon. Example:

     for  (int i =  0; i < array.length; i++)  {
    sum += array[i];
    }

Because array elements are **stored contiguously**, accessing  `array[i]`  benefits from spatial locality.

**2. Temporal Locality**
If a program accesses a memory location, it's likely to access the  **same location again**  soon. Example:

    for  (int i =  0; i <  1000; i++)  {
     doSomething(counter);
    }

Accessing the variable  `counter`  repeatedly benefits from temporal locality.
 

**ArrayList vs LinkedList and Cache Locality**

  

![](https://img-c.udemycdn.com/redactor/raw/article_lecture/2025-09-10_08-19-26-896b5761382c955db9e8a877d4f3463f.png)


**CPU cache** is a small, fast memory close to the processor. It loads blocks of memory (like 64 bytes at a time). If elements are **stored together** (as in an  `ArrayList`), the cache brings them in all at once, making future accesses **very fast**.

With a  `LinkedList`, the nodes are **not contiguous** — each node is a separate object pointing to another. So:

-   Accessing one node doesn't help you access the next
    
-   More **cache misses**
    
-   **Slower traversal and iteration**

Most used methods in List Interface:
- add(E element) - Adds the specified element to the end of the list.
    
- addAll(Collection<? extends E> c) - Adds all elements of the specified collection to the end of the list.
    
- remove(Object o) - Removes the first occurrence of the specified element from the list.
    
- remove(int index) - Removes the element at the specified position in the list.
    
- get(int index) - Returns the element at the specified position in the list.
    
- set(int index, E element) - Replaces the element at the specified position in the list with the specified element.
    
- indexOf(Object o) - Returns the index of the first occurrence of the specified element in the list.
    
-  contains(Object o) - Returns true if the list contains the specified element.
    
- size() - Returns the number of elements in the list.
    
-  isEmpty() - Returns true if the list contains no elements.
    
- clear() - Removes all elements from the list.
    
- toArray() - Returns an array containing all the elements in the list.
    
-  subList(int fromIndex, int toIndex) - Returns a view of the portion of the list between the specified fromIndex, inclusive, and toIndex, exclusive.
    
- addAll(int index, Collection<? extends E> c) - Inserts all elements of the specified collection into the list, starting at the specified position.
    
-  iterator() - Returns an iterator over the elements in the list.
    
-  sort(Comparator<? super E> c) - Sorts the elements of the list according to the specified comparator.
    
-  replaceAll(UnaryOperator<E> operator) - Replaces each element of the list with the result of applying the given operator.
    
-  forEach(Consumer<? super E> action) - Performs the given action for each element of the list until all elements have been processed or the action throws an exception.

**Vectors:**
The main difference is that  **ArrayList is not synchronized and faster**, while **Vector is synchronized (thread-safe), slower, and a legacy class**. ArrayList increases its capacity by 50%, whereas Vector doubles its capacity when it exceeds its current size. In most cases, ArrayList is preferred for single-threaded applications due to better performance, while Vector is used only when thread-safety is crucial for multi-threaded environments.

**Stack**
stack operates LIFO principle
Following operation are offered

 - *push(e)* - to add elements on top of stack 
 - *pop()* - retrieve element on top of stack 
 - *peek()* -  just view element without removing it from top of stack

---
### Queue
The Queue interface follows the **First-In, First-Out (FIFO)** principle. It extends the Collection interface and provides specific methods for managing elements at the head (front) and tail (rear) of the queue. 

#### summary of the core methods in the Queue interface:
|Operation| Method |Returns| Throws Exception | Description|
|--|--|--|--|--|
|Insert|add(E e)|True|If the queue has a capacity restriction and cannot add the element, it throws an IllegalStateException.|Inserts the specified element into end of the queue(tail)|
||offer(E e) |True (or) False| No| Preferred way to insert for bounded queues. returns false if unable|
|Remove |remove()|head element|Yes, NoSuchElementException if empty) |Retrieves and removes the head of the queue|
||poll()|head element or `null`|No |preferred over remove() when dealing with potentially empty queues.|
|Examine|element()|head element|Yes, NoSuchElementException if empty)|Retrieves, but does not remove, the head of the queue|
||peek()|head element or `null`|No| Retrieves, but does not remove, the head of the queue|

**Key Characteristics:**
FIFO (First-In, First-Out): Elements are processed in the order they were added (with exceptions like PriorityQueue).
Interface: Queue is an interface and cannot be directly instantiated. Implementations like LinkedList, PriorityQueue, and ArrayDeque provide concrete queue functionality.
**Head and Tail**: Elements are typically added at the tail and removed from the head.

##### 

### References

[Collection vs Collections in Java with Example - GeeksforGeeks](https://www.geeksforgeeks.org/java/collection-vs-collections-in-java-with-example/)
