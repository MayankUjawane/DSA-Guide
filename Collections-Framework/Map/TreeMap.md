# TreeMap
>Java TreeMap class is a **red-black tree** based implementation. By default, TreeMap keeps its entries **sorted** according to the natural ordering of its **keys** or 
>using a comparator if provided by the user at construction time. For an integer, natural ordering would mean ascending order and for Strings, alphabetical order.
>
>The important points about Java TreeMap class are:
>
>* Java TreeMap contains values based on the key.
>* Java TreeMap contains only **unique elements**.
>* Java TreeMap cannot have a null key but can have multiple null values.
>* Java TreeMap keeps entries sorted.
>* Java TreeMap provides **log(n)** time cost for the containsKey, get, put and remove operations.

### TreeMap time complexity    
>* Read   : O(log n)
>* Search : O(log n)
>* Update : O(log n)
>* Delete : O(log n)
>* Add    : O(log n)

### Methods of TreeMap
```java
class TreeMap {
    Map<String, Integer> treeMap = new TreeMap<>();

    //For adding elements we use put method
    treeMap.put("One", 1);
    treeMap.put("Two", 2);
    treeMap.put("Three", 3);
    treeMap.put("Four", 4);
    treeMap.put("Five", 5);

    //To remove any element we use remove method
    treeMap.remove("Three");

    //As name suggests putIfAbsent method will insert the value if key "Two" is not present
    treeMap.putIfAbsent("Two", 23);
    
    //containsKey method tells that the key is present or not
    if(!treeMap.containsKey("Two")) {
        treeMap.put("Two", 23);
    }

    //Map.Entry interface in Java provides certain methods to access the entry in the Map.
    //entrySet() method declared by the Map interface returns a Set containing the map entries.
    for (Map.Entry<String, Integer> e: treeMap.entrySet()) {
        System.out.println(e);
        System.out.println(e.getKey());
        System.out.println(e.getValue());
    }

    //keySet method gives the keys of Map
    for (String key: treeMap.keySet()) {
        System.out.println(key);
    }

    //values method gives the values of Map
    for(Integer value: treeMap.values()) {
        System.out.println(value);
    }
}
```

### Custom Sorting in TreeMap     
>If we're not satisfied with the natural ordering of TreeMap, we can also define our own rule for ordering by means of a comparator during construction of a tree map
```java
TreeMap<Integer, String> treeMap = new TreeMap<>(Comparator.reverseOrder());
```

A hash map does not guarantee the order of keys stored and specifically does not guarantee that this order will remain the same over time, but a tree map guarantees that 
the keys will always be sorted according to the specified order.
