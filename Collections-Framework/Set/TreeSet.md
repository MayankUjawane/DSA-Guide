# TreeSet
>TreeSet is one of the most important implementations of the **SortedSet interface** in Java that uses a **Tree** for storage. 
>The **ordering** of the elements is **maintained** by a set using their **natural ordering** whether or not an explicit comparator is provided.
>This implementation provides guaranteed **log(n)** time cost for the basic operations (add, remove and contains).
>
>In TreeSet, objects are **sorted** and stored in **ascending order** according to their natural order. 
>The TreeSet uses a self-balancing binary search tree, more specifically a **Red-Black tree**.
>
>The important points about Java TreeSet class are:
>
>* TreeSet class contains **unique elements** only like HashSet.
>* TreeSet class doesn't allow **null element**.
>* TreeSet doesn't preserve the insertion order of the elements. It maintains **ascending order** or **natural ordering**.
>* TreeSet provides **O(log n)** time cost for the add, remove, and contains.

### TreeSet time complexity    
>* Add   : O(log n)
>* Remove : O(log n)
>* Contains : O(log n)
>* Size : O(1)

### Methods of TreeSet
```java
class TreeSet {
    TreeSet<String> set = new TreeSet();    

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
  
    //Removing specific element from TreeSet  
    set.remove("Ravi");  
    
    TreeSet<String> set1 = new TreeSet<String>();  
    set1.add("Ajay");  
    set1.add("Gaurav");  
    set.addAll(set1);    
  
    //Removing all the new elements from TreeSet  
    set.removeAll(set1);  
  
    //Removing elements on the basis of specified condition  
    set.removeIf(str -> str.contains("Vijay"));    
  
    //Removing all the elements available in the set  
    set.clear();  
  
  
    //Java TreeSet from another Collection
    ArrayList<String> list = new ArrayList<String>();  
    list.add("Ravi");  
    list.add("Vijay");  
    list.add("Ajay");  

    TreeSet<String> set2 = new TreeSet(list);  
    set2.add("Gaurav");  
    Iterator<String> i = set2.iterator();  
    while(i.hasNext()) {  
        System.out.println(i.next());  
    } 
}
```

### Initialize TreeSet with Values
* **Using Another Collection Instance**
>We can pass an existing instance of another collection to initialize the Set.
```java
Set<String> set = new TreeSet<>(Arrays.asList("a", "b", "c"));
```

* **Using Anonymous Class**
>Note the use of double curly braces is technically very **expensive** as it creates an anonymous class each time it's called.
```java
Set<String> set = new TreeSet<String>(){{
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
Stream<String> stream = Stream.of("a", "b", "c");
Set<String> set = stream.collect(Collectors.toCollection(TreeSet::new));
```
----
