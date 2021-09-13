# LinkedHashMap
>Java LinkedHashMap class is ***Hashtable*** and ***Linked list*** implementation of the Map interface, with predictable ***iteration order***. 
>It inherits HashMap class and implements the Map interface.
>
>The important points about Java LinkedHashMap class are:
>
>* Java LinkedHashMap contains **unique elements**.
>* Java LinkedHashMap may have one null key and multiple null values.
>* Java LinkedHashMap maintains **insertion order**.
>* Java LinkedHashMap provides **O(1)** time cost for the containsKey, get, put and remove operations.

### LinkedHashMap time complexity    
>* Read   : O(1)
>* Search : O(1)
>* Update : O(1)
>* Delete : O(1)
>* Add    : O(1)

### Methods of LinkedHashMap
```java
class LinkedHashMap {
    // Create an empty linkedHashMap by declaring object of string and integer type
    Map<String, Integer> linkedHashMap = new LinkedHashMap<>();

    //For adding elements we use put method
    linkedHashMap.put("One", 1);
    linkedHashMap.put("Two", 2);
    linkedHashMap.put("Three", 3);
    linkedHashMap.put("Four", 4);
    linkedHashMap.put("Five", 5);

    //Print size of the LinkedHashMap
    System.out.println("Size of linkedHashMap is:- " + linkedHashMap.size());

    //Printing elements in object of LinkedHashMap
    System.out.println(linkedHashMap);
  
    //To remove any element we use remove method
    linkedHashMap.remove("Three");

    //As name suggests putIfAbsent method will insert the value if key "Two" is not present
    linkedHashMap.putIfAbsent("Two", 23);
    
    //Checking if a key is present and if not present, add key and value.
    if(!linkedHashMap.containsKey("Two")) {
        linkedHashMap.put("Two", 23);
    }
  
    //to check if a value is present in the map, we can use the containsValue() method
    linkedHashMap.containsValue(1);

    //Map.Entry interface in Java provides certain methods to access the entry in the Map.
    //entrySet() method declared by the Map interface returns a Set containing the map entries.
    //Iterate the map using for-each loop
    for (Map.Entry<String, Integer> e: linkedHashMap.entrySet()) {
        System.out.println(e);
        System.out.println(e.getKey());
        System.out.println(e.getValue());
    }
  
    //The forEach method is the functional-style way to iterate over all elements in the map:
    linkedHashMap.forEach( (key, value) -> {
        System.out.println("Key: " + key + " Value: " + value);
    });

    //keySet method gives the keys of Map
    for (String key: linkedHashMap.keySet()) {
        System.out.println(key);
    }

    //values method gives the values of Map
    for(Integer value: linkedHashMap.values()) {
        System.out.println(value);
    }
}
```

### Initialize LinkedHashMap with Values
>There is no built-in syntax for specifically initializing maps. However, you can take advantage of a special syntax known as **double brace initialization**. 
```java
Map<String, Integer> linkedHashMap = new LinkedHashMap<String, Integer>() {{
    put("one", 1); 
    put("two", 2);
}};
```
