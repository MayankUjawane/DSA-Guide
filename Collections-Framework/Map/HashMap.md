# HashMap
>HashMap<K, V> is a part of Java’s collection since Java 1.2. This class is found in java.util package. HashMap class extends AbstractMap class and implements Map interface. 
>It provides the basic implementation of the Map interface of Java. It stores the data in (Key, Value) pairs, and you can access them by an index of another type (e.g. an Integer). One object is used as a key (index) to another object (value). 
>If you try to insert the duplicate key, it will replace the element of the corresponding key.
>
>The important points about Java HashMap class are:
>
>* Java HashMap contains values based on the **unique keys**.
>* Java HashMap may have one null key and multiple null values.
>* Java HashMap maintains **no order**.
>* Java HashMap provides **O(1)** time cost for the containsKey, get, put and remove operations.
>* The initial default capacity of Java HashMap class is 16 with a load factor of 0.75.

### HashMap time complexity    
>* Read   : O(1)
>* Search : O(1)
>* Update : O(1)
>* Delete : O(1)
>* Add    : O(1)

### Methods of HashMap
```java
class HashMap {
    // Create an empty hash map by declaring object of string and integer type
    Map<String, Integer> hashMap = new TreeMap<>();

    //For adding elements we use put method
    hashMap.put("One", 1);
    hashMap.put("Two", 2);
    hashMap.put("Three", 3);
    hashMap.put("Four", 4);
    hashMap.put("Five", 5);

    //Print size of the HashMap
    System.out.println("Size of hashMap is:- " + hashMap.size());

    //Printing elements in object of HashMap
    System.out.println(hashMap);
  
    //To remove any element we use remove method
    hashMap.remove("Three");

    //As name suggests putIfAbsent method will insert the value if key "Two" is not present
    hashMap.putIfAbsent("Two", 23);
    
    //Checking if a key is present and if not present, add key and value.
    if(!hashMap.containsKey("Two")) {
        hashMap.put("Two", 23);
    }
  
    //to check if a value is present in the map, we can use the containsValue() method
    hashMap.containsValue(1);

    //Map.Entry interface in Java provides certain methods to access the entry in the Map.
    //entrySet() method declared by the Map interface returns a Set containing the map entries.
    //Iterate the map using for-each loop
    for (Map.Entry<String, Integer> e: hashMap.entrySet()) {
        System.out.println(e);
        System.out.println(e.getKey());
        System.out.println(e.getValue());
    }
  
    //The forEach method is the functional-style way to iterate over all elements in the map:
    hashMap.forEach( (key, value) -> {
        System.out.println("Key: " + key + " Value:" + value);
    });

    //keySet method gives the keys of Map
    for (String key: hashMap.keySet()) {
        System.out.println(key);
    }

    //values method gives the values of Map
    for(Integer value: hashMap.values()) {
        System.out.println(value);
    }
}
```

### Initialize TreeMap with Values
>There is no built-in syntax for specifically initializing maps. However, you can take advantage of a special syntax known as **double brace initialization**. 
```java
Map<String, Integer> hashMap = new HashMap<String, String>() {{
    put("one", 1); 
    put("two", 2);
}};
```
