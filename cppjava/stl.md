# C++ STL Quick Reference

## 1. Vector
```cpp
#include <vector>
vector<int> v = {1, 2, 3};
v.push_back(4); // Add O(1)
v.pop_back();   // Remove last O(1)
v.size();       // Size O(1)
v.clear();      // Remove all O(n)
v[0];           // Access O(1)
```

## 2. Set
```cpp
#include <set>
set<int> s = {1, 2, 3};
s.insert(4);    // O(log n)
s.erase(2);     // O(log n)
s.count(3);     // O(log n), 1 if present
s.find(1);      // O(log n), iterator to 1 or s.end()
```

## 3. Map
```cpp
#include <map>
map<int, int> m;
m[1] = 10;      // O(log n)
m[2] = 20;      // O(log n)
m.count(1);     // O(log n)
m.erase(2);     // O(log n)
m.find(1);      // O(log n), iterator
```

## 4. Unordered Set/Map
```cpp
#include <unordered_set>
#include <unordered_map>
unordered_set<int> us;
us.insert(5);   // O(1) avg

unordered_map<int, int> um;
um[3] = 30;     // O(1) avg
```

## 5. Stack
```cpp
#include <stack>
stack<int> st;
st.push(1);     // O(1)
st.top();       // O(1)
st.pop();       // O(1)
st.empty();     // O(1)
```

## 6. Queue
```cpp
#include <queue>
queue<int> q;
q.push(1);      // O(1)
q.front();      // O(1)
q.pop();        // O(1)
q.empty();      // O(1)
```

## 7. Priority Queue (Max-Heap)
```cpp
#include <queue>
priority_queue<int> pq;
pq.push(3);     // O(log n)
pq.top();       // O(1)
pq.pop();       // O(log n)
```

## 8. Deque
```cpp
#include <deque>
deque<int> dq;
dq.push_front(1); // O(1)
dq.push_back(2);  // O(1)
dq.pop_front();   // O(1)
dq.pop_back();    // O(1)
```

## 9. String
```cpp
#include <string>
string s = "abc";
s.size();        // O(1)
s.substr(1,2);   // O(2)
s.find('b');     // O(n)
```

## 10. Pair
```cpp
#include <utility>
pair<int, string> p = {1, "abc"};
p.first;   // 1, O(1)
p.second;  // "abc", O(1)
```

## 11. Min-Heap (Priority Queue with Pair)
```cpp
#include <queue>
#include <vector>
#include <utility>
// Min-heap for int
priority_queue<int, vector<int>, greater<int>> min_pq;
min_pq.push(5);      // O(log n)
min_pq.top();        // O(1)
min_pq.pop();        // O(log n)

// Min-heap for pair<int, int> (by first element)
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq_pair;
pq_pair.push({2, 100}); // O(log n)
pq_pair.push({1, 200}); // O(log n)
auto top = pq_pair.top(); // {1, 200}, O(1)
```

---

## When to Use Each STL Container

- **vector**: Use for dynamic arrays, fast access by index, and when you mostly add/remove at the end.
- **set**: Use for unique, ordered elements with fast search, insert, and erase (O(log n)).
- **unordered_set**: Use for unique, unordered elements with average O(1) insert/find/erase.
- **map**: Use for key-value pairs with unique, ordered keys and fast search/insert/erase (O(log n)).
- **unordered_map**: Use for key-value pairs with unique, unordered keys and average O(1) operations.
- **stack**: Use for LIFO (last-in, first-out) operations (e.g., DFS, undo functionality).
- **queue**: Use for FIFO (first-in, first-out) operations (e.g., BFS, task scheduling).
- **priority_queue**: Use for always retrieving the largest (max-heap) or smallest (min-heap) element efficiently (e.g., Dijkstra, top-K problems).
- **deque**: Use for fast insert/remove at both ends (e.g., sliding window problems).
- **string**: Use for text manipulation, substring search, and character access.
- **pair**: Use for returning two values from a function, or as a composite key/value in containers.
- **min-heap (priority_queue with greater)**: Use when you need to always access/remove the smallest element (e.g., scheduling, greedy algorithms, A* search).

**Tip:** Choose the container that matches your access pattern and performance needs. For interview code, prefer clarity and correctness over micro-optimizations.

## STL Container Time Complexities

| Container         | Insert      | Erase       | Find/Access | Notes                       |
|-------------------|-------------|-------------|-------------|-----------------------------|
| vector            | O(1) (end)  | O(1) (end)  | O(1)        | O(n) for insert/erase mid   |
| set               | O(log n)    | O(log n)    | O(log n)    | Red-black tree (ordered)    |
| unordered_set     | O(1) avg    | O(1) avg    | O(1) avg    | Hash table, O(n) worst      |
| map               | O(log n)    | O(log n)    | O(log n)    | Red-black tree (ordered)    |
| unordered_map     | O(1) avg    | O(1) avg    | O(1) avg    | Hash table, O(n) worst      |
| stack             | O(1)        | O(1)        | O(1)        | Uses vector/deque           |
| queue             | O(1)        | O(1)        | O(1)        | Uses deque                  |
| priority_queue    | O(log n)    | O(log n)    | O(1) (top)  | Binary heap                 |
| deque             | O(1) ends   | O(1) ends   | O(1)        | O(n) for mid ops            |
| string            | O(1) (end)  | O(1) (end)  | O(1)        | O(n) for insert/erase mid   |

**Note:**
- For `unordered_*`, worst case is O(n) due to hash collisions.
- For `vector`/`string`, insert/erase at middle is O(n).
- For `priority_queue`, only top element access is O(1); push/pop are O(log n).
- All containers support iteration: O(n).
