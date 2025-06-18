# Java Collections Quick Reference

## 1. ArrayList
```java
import java.util.ArrayList;
ArrayList<Integer> list = new ArrayList<>();
list.add(1);        // Add O(1)
list.remove(0);     // Remove by index O(n)
list.get(0);        // Access O(1)
list.size();        // Size O(1)
list.contains(1);   // O(n)
```

## 2. HashSet
```java
import java.util.HashSet;
HashSet<Integer> set = new HashSet<>();
set.add(2);         // O(1) avg
set.remove(2);      // O(1) avg
set.contains(2);    // O(1) avg
```

## 3. TreeSet
```java
import java.util.TreeSet;
TreeSet<Integer> tset = new TreeSet<>();
tset.add(3);        // O(log n)
tset.remove(3);     // O(log n)
tset.contains(3);   // O(log n)
tset.first();       // O(log n)
tset.last();        // O(log n)
```

## 4. HashMap
```java
import java.util.HashMap;
HashMap<Integer, String> map = new HashMap<>();
map.put(1, "a");   // O(1) avg
map.get(1);         // O(1) avg
map.remove(1);      // O(1) avg
map.containsKey(1); // O(1) avg

HashMap<String, Integer> frequencyMap = new HashMap<>();
// Adding elements (new and existing)
frequencyMap.put("apple", frequencyMap.getOrDefault("apple", 0) + 1);
frequencyMap.put("banana", frequencyMap.getOrDefault("banana", 0) + 1);
frequencyMap.put("apple", frequencyMap.getOrDefault("apple", 0) + 1);

// Checking frequency
int appleFrequency = frequencyMap.getOrDefault("apple", 0);

// Adding new element
frequencyMap.put("orange", frequencyMap.getOrDefault("orange", 0) + 1);

// Removing element
if (frequencyMap.containsKey("apple")) {
    frequencyMap.put("apple", frequencyMap.get("apple") - 1);
    if (frequencyMap.get("apple") == 0) {
        frequencyMap.remove("apple");
    }
}

// Checking sizes
int uniqueElementsCount = frequencyMap.size();
int totalElementsCount = frequencyMap.values().stream().mapToInt(Integer::intValue).sum();

// Checking existence
boolean hasBanana = frequencyMap.containsKey("banana");
boolean hasGrape = frequencyMap.containsKey("grape");

// 1️⃣ forEach + Lambda (Best for readability - Java 8+)
freqMap.forEach((key, value) -> 
    System.out.println(key + " → " + value)
);

// 2️⃣ EntrySet for-loop (Classic & efficient)
for (Map.Entry<String, Integer> entry : freqMap.entrySet()) {
    System.out.println(entry.getKey() + " → " + entry.getValue());
}

// 3️⃣ Stream API (Modern filtering/sorting)
freqMap.entrySet().stream()
        .sorted(Map.Entry.comparingByValue(Comparator.reverseOrder()))
        .forEach(entry -> 
            System.out.println(entry.getKey() + " → " + entry.getValue())
        );

// 4️⃣ KeySet iteration (When you only need keys)
for (String key : freqMap.keySet()) {
    System.out.println(key + " → " + freqMap.get(key));
}

// 5️⃣ Iterator (Safe for removal during iteration)
Iterator<Map.Entry<String, Integer>> it = freqMap.entrySet().iterator();
while (it.hasNext()) {
    Map.Entry<String, Integer> entry = it.next();
    if (entry.getValue() < 4) {  // Example condition
        it.remove();  // Safely remove low-frequency items
    }
}
```

## 5. TreeMap
```java
import java.util.TreeMap;
TreeMap<Integer, String> tmap = new TreeMap<>();
tmap.put(2, "b");   // O(log n)
tmap.get(2);         // O(log n)
tmap.remove(2);      // O(log n)
tmap.containsKey(2); // O(log n)
tmap.firstKey();     // O(log n)
tmap.lastKey();      // O(log n)
```

## 6. Stack
```java
import java.util.Stack;
Stack<Integer> st = new Stack<>();
st.push(1);         // O(1)
st.pop();           // O(1)
st.peek();          // O(1)
st.isEmpty();       // O(1)
```

## 7. Queue (LinkedList)
```java
import java.util.Queue;
import java.util.LinkedList;
Queue<Integer> q = new LinkedList<>();
q.offer(1);         // O(1)
q.poll();           // O(1)
q.peek();           // O(1)
q.isEmpty();        // O(1)
```

## 8. PriorityQueue (Min-Heap)
```java
import java.util.PriorityQueue;
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(2);        // O(log n)
pq.peek();          // O(1)
pq.poll();          // O(log n)

// Max-Heap
PriorityQueue<Integer> maxPq = new PriorityQueue<>(java.util.Collections.reverseOrder());
```

## 9. Deque
```java
import java.util.Deque;
import java.util.ArrayDeque;
Deque<Integer> dq = new ArrayDeque<>();
dq.addFirst(1);     // O(1)
dq.addLast(2);      // O(1)
dq.removeFirst();   // O(1)
dq.removeLast();    // O(1)
```

## 10. Pair (AbstractMap.SimpleEntry)
```java
import java.util.AbstractMap;
AbstractMap.SimpleEntry<Integer, String> p = new AbstractMap.SimpleEntry<>(1, "abc");
p.getKey();         // 1, O(1)
p.getValue();       // "abc", O(1)
```

---

## When to Use Each Java Collection

- **ArrayList**: Use for dynamic arrays, fast access by index, mostly add/remove at end.
- **HashSet**: Use for unique, unordered elements with fast operations.
- **TreeSet**: Use for unique, ordered elements (sorted set) with log n operations.
- **HashMap**: Use for key-value pairs with unique, unordered keys and fast operations.
- **TreeMap**: Use for key-value pairs with unique, ordered keys (sorted map).
- **Stack**: Use for LIFO (last-in, first-out) operations (e.g., DFS, undo functionality).
- **Queue (LinkedList)**: Use for FIFO (first-in, first-out) operations (e.g., BFS, task scheduling).
- **PriorityQueue**: Use for always retrieving the smallest (min-heap) or largest (max-heap) element efficiently.
- **Deque**: Use for fast insert/remove at both ends (e.g., sliding window problems).
- **Pair (SimpleEntry)**: Use for returning two values from a function or as a composite key/value in maps.

**Tip:** Choose the collection that matches your access pattern and performance needs. For interview code, prefer clarity and correctness over micro-optimizations.

## Java Collection Time Complexities

| Collection        | Insert      | Remove      | Find/Access | Notes                       |
|------------------|-------------|-------------|-------------|-----------------------------|
| ArrayList        | O(1) (end)  | O(n)        | O(1)        | O(n) for mid ops            |
| HashSet          | O(1) avg    | O(1) avg    | O(1) avg    | Hash table, O(n) worst      |
| TreeSet          | O(log n)    | O(log n)    | O(log n)    | Red-black tree (ordered)    |
| HashMap          | O(1) avg    | O(1) avg    | O(1) avg    | Hash table, O(n) worst      |
| TreeMap          | O(log n)    | O(log n)    | O(log n)    | Red-black tree (ordered)    |
| Stack            | O(1)        | O(1)        | O(1)        | Uses Vector                 |
| Queue (LinkedList)| O(1)       | O(1)        | O(1)        | Doubly-linked list          |
| PriorityQueue    | O(log n)    | O(log n)    | O(1) (peek) | Binary heap                 |
| Deque            | O(1) ends   | O(1) ends   | O(1)        | ArrayDeque recommended      |

**Note:**
- For `Hash*`, worst case is O(n) due to hash collisions.
- For `ArrayList`, insert/remove at middle is O(n).
- For `PriorityQueue`, only peek is O(1); offer/poll are O(log n).
- All collections support iteration: O(n).
