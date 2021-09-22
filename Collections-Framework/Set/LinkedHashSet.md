# LinkedHashSet
>The LinkedHashSet is an ordered version of HashSet that maintains a doubly-linked List across all elements. When the iteration order is needed to be maintained this 
>class is used. When iterating through a HashSet the order is unpredictable, while a LinkedHashSet lets us iterate through the elements in the order in which they were inserted.
>
>The important points about Java LinkedHashSet class are:
>
>* LinkedHashSet class contains **unique** elements only and **permits nulls** like HashSet.
>* LinkedHashSet class maintains **insertion order**. 

### LinkedHashSet Time Complexity    
>* Add   : O(1)
>* Remove : O(1)
>* Contains : O(1)
>* Size : O(1)

### Methods of LinkedHashSet
```java
class LinkedHashSet {
    LinkedHashSet<String> set = new LinkedHashSet();    

    //For adding elements we use add method
    set.add("Ravi");  
    set.add("Vijay");  
    set.add("Ajay");  
  
    //Traversing elements  
    Iterator<String> itr = set.iterator();  
    while(itr.hasNext()){  
       System.out.println(itr.next());  
    }    
  
    set.add("Sumit");  
    System.out.println("An initial list of elements: " + set + " " + set.size());  
  
    //to check if an element is present
    set.contains("Ravi");
  
    //Removing specific element from LinkedHashSet  
    set.remove("Ravi");  
    
    LinkedHashSet<String> set1 = new LinkedHashSet<String>();  
    set1.add("Ajay");  
    set1.add("Gaurav");  
    set.addAll(set1);    
  
    //Removing all the new elements from LinkedHashSet  
    set.removeAll(set1);  
  
    //Removing elements on the basis of specified condition  
    set.removeIf(str -> str.contains("Vijay"));    
  
    //Removing all the elements available in the set  
    set.clear();  
  
  
    //Java LinkedHashSet from another Collection
    ArrayList<String> list = new ArrayList<String>();  
    list.add("Ravi");  
    list.add("Vijay");  
    list.add("Ajay");  

    LinkedHashSet<String> set2 = new LinkedHashSet(list);  
    set2.add("Gaurav");  
    Iterator<String> i = set2.iterator();  
    while(i.hasNext()) {  
        System.out.println(i.next());  
    } 
}
```

### Initialize LinkedHashSet with Values
* **Using Another Collection Instance**
>We can pass an existing instance of another collection to initialize the Set.
```java
Set<String> set = new LinkedHashSet<>(Arrays.asList("a", "b", "c"));
```

* **Using Anonymous Class**
>Note the use of double curly braces is technically very **expensive** as it creates an anonymous class each time it's called.
```java
Set<String> set = new LinkedHashSet<String>(){{
    add("a");
    add("b");
    add("c");
}};
```

* **Using Collections Utility Method Since Java 5**
>The Java's Collections utility class provides the method named **singleton** to create a Set with a **single element**. 
>The Set instance created with the singleton method is **immutable** meaning that we cannot add more values to it.
```java
Set<String> set = Collections.singleton("a");
```

* **Using Stream Since Java 8**
>With the introduction of Stream API in Java 8, we can use **Stream with Collectors**.
```java
Set<String> set = Stream.of("a", "b", "c").collect(Collectors.toCollection(LinkedHashSet::new));
```
----
