# HashSet
>The HashSet class implements the **Set interface**, backed by a **hash table** which is actually a **HashMap** instance. 
>No guarantee is made as to the **iteration order** of the set which means that the class does not guarantee the **constant order** of elements over time. 
>This class permits the null element. 
>The class also offers **constant time** performance for the basic operations like add, remove, contains, and size.
>
>The important points about Java HashMap class are:
>
>* HashSet stores the elements by using a mechanism called **hashing**.
>* HashSet contains **unique** elements only and **permits nulls**.
>* HashSet doesn't maintain the **insertion order**. Here, elements are inserted on the basis of their **hashcode**.
>* HashSet provides **O(1)** time cost for the add, remove, contains, and size.
>* HashSet is the best approach for **search operations**.
>* The initial default capacity of HashSet is 16, and the load factor is 0.75

### HashSet time complexity    
>* Read   : O(1)
>* Search : O(1)
>* Update : O(1)
>* Delete : O(1)
>* Add    : O(1)

### Methods of HashSet
```java
class HashSet {
    // Create an empty hash map by declaring object of string and integer type
    HashSet<String> set = new HashSet();    

    //For adding elements we use put method
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
  
    //Removing specific element from HashSet  
    set.remove("Ravi");  
    
    HashSet<String> set1=new HashSet<String>();  
    set1.add("Ajay");  
    set1.add("Gaurav");  
    set.addAll(set1);    
  
    //Removing all the new elements from HashSet  
    set.removeAll(set1);  
  
    //Removing elements on the basis of specified condition  
    set.removeIf(str -> str.contains("Vijay"));    
  
    //Removing all the elements available in the set  
    set.clear();  
  
  
    //Java HashSet from another Collection
    list.add("Ravi");  
    list.add("Vijay");  
    list.add("Ajay");  

    HashSet<String> set2 = new HashSet(list);  
    set2.add("Gaurav");  
    Iterator<String> i = set2.iterator();  
    while(i.hasNext()) {  
        System.out.println(i.next());  
    } 
}
```

### Initialize HashSet with Values
1. **Using Another Collection Instance**
>We can pass an existing instance of another collection to initialize the Set.
```java
Set<String> set = new HashSet<>(Arrays.asList("a", "b", "c"));
```

2. **Using Anonymous Class**
>Note the use of double curly braces is technically very **expensive** as it creates an anonymous class each time it's called.
```java
Set<String> set = new HashSet<String>(){{
    add("a");
    add("b");
    add("c");
}};
```

3. **Using Collections Utility Method Since Java 5**
>The Java's Collections utility class provides the method named **singleton** to create a Set with a **single element**. 
>The Set instance created with the singleton method is **immutable** meaning that we cannot add more values to it.
```java
Set<String> set = Collections.singleton("a");
```

4. **Using Stream Since Java 8**
>With the introduction of Stream API in Java 8, we can use **Stream with Collectors**.
```java
Set<String> set = Stream.of("a", "b", "c").collect(Collectors.toCollection(HashSet::new));
```
