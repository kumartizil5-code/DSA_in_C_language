# 📘 Data Structures — Complete Interview Preparation Guide

> **Audience:** Freshers & early-career engineers targeting strong fundamentals  
> **Goal:** Interview-ready knowledge with deep conceptual clarity  
> **Style:** Revision-friendly, bullet-point-focused, no fluff

---

## 📌 Table of Contents

1. [Time Complexity Fundamentals](#-time-complexity-fundamentals)
2. [Array](#1--array)
3. [Stack](#2--stack)
4. [Queue](#3--queue)
5. [Singly Linked List](#4--singly-linked-list)
6. [Doubly Linked List](#5--doubly-linked-list)
7. [Circular Linked List](#6--circular-linked-list)
8. [Skip List](#7--skip-list)
9. [Hash Table](#8--hash-table)
10. [Binary Search Tree (BST)](#9--binary-search-tree-bst)
11. [Cartesian Tree](#10--cartesian-tree)
12. [B-Tree](#11--b-tree)
13. [Red-Black Tree](#12--red-black-tree)
14. [Splay Tree](#13--splay-tree)
15. [AVL Tree](#14--avl-tree)
16. [KD Tree](#15--kd-tree)
17. [Final Comparison Table](#-final-comparison-table)

---

## ⏱ Time Complexity Fundamentals

### Big-O, Big-Theta, Big-Omega — What They Actually Mean

Understanding these notations is non-negotiable in interviews. They describe how an algorithm scales as input size `n` grows.

---

### 🔹 Big-O (O) — Upper Bound / Worst Case

- Describes the **maximum** time an algorithm can take.
- "In the **worst** situation, the algorithm will not take **more** than this."
- Most commonly discussed in interviews.
- **Example:** Linear search on an array of `n` elements is `O(n)` — in the worst case, the target is at the last position or absent.

### 🔹 Big-Omega (Ω) — Lower Bound / Best Case

- Describes the **minimum** time an algorithm will take.
- "The algorithm will take **at least** this long."
- **Example:** Linear search is `Ω(1)` — in the best case, the target is the first element.

### 🔹 Big-Theta (Θ) — Tight Bound / Average Case (Both)

- Describes the **exact asymptotic behavior** — algorithm is both `O(f(n))` and `Ω(f(n))`.
- Means the function grows exactly at this rate in all cases.
- **Example:** Traversing all elements in an array is `Θ(n)` — always touches every element.

---

### Best, Average, Worst Case — Clear Distinction

| Case | Definition | Practical Meaning |
|---|---|---|
| **Best Case** | Most favourable input — algorithm finishes fastest | Rarely relied upon for performance guarantees |
| **Average Case** | Expected performance over all possible inputs | Most realistic measure; requires probabilistic analysis |
| **Worst Case** | Most unfavourable input — algorithm takes longest | Primary metric in system design and safety-critical systems |

#### Concrete Example — Binary Search

| Case | Condition | Complexity |
|---|---|---|
| Best | Target is the **middle element** | `O(1)` |
| Average | Target found after ~log n comparisons | `O(log n)` |
| Worst | Target is absent or at extreme end | `O(log n)` |

#### Common Complexity Classes (Fastest → Slowest)

```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!)
```

> **Interview Tip:** Always state which case you are referring to when you mention complexity. Saying "search is O(1)" without context is incomplete — an interviewer will ask "in which case?"

---
---

## 1. 📦 Array

### 🔹 Technical Definition

An **Array** is a contiguous, fixed-size (in most languages) sequential collection of elements of the same data type, stored in memory such that each element can be accessed in constant time via an integer index. The base address and element size determine the physical address of any element using: `address = base + (index × element_size)`.

---

### 🔹 Intuition / Core Idea

- Think of a **row of numbered lockers** — each locker has a unique number (index), and you can jump to any locker instantly.
- The power of arrays lies in **random access** — if you know the index, retrieval is `O(1)` regardless of size.
- Used when: you need fast indexed access, the size is known in advance, and cache performance matters.

---

### 🔹 Key Properties & Insights

- **Contiguous memory allocation** — all elements are stored side by side; enables CPU cache efficiency.
- **Zero-indexed** in most languages (index starts at 0).
- **Fixed size** in static arrays; dynamic arrays (like `ArrayList`, Python lists) resize by allocating a new larger block and copying elements.
- **Homogeneous** — all elements must be of the same type (in typed languages).
- **Random access** — any element reachable in O(1) via index.
- **Insertion/Deletion at middle** is expensive — requires shifting elements.
- Dynamic arrays typically **double in capacity** when full — amortized `O(1)` append.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Access by Index | O(1) | O(1) | O(1) |
| Search (Unsorted) | O(1) | O(n) | O(n) |
| Search (Sorted — Binary) | O(1) | O(log n) | O(log n) |
| Insert at End (Dynamic) | O(1) | O(1) amortized | O(n) (resize) |
| Insert at Beginning/Middle | O(n) | O(n) | O(n) |
| Delete at End | O(1) | O(1) | O(1) |
| Delete at Beginning/Middle | O(n) | O(n) | O(n) |
| Traversal | O(n) | O(n) | O(n) |

**Space Complexity:** `O(n)`

---

### 🔹 Verbal Explanation of Implementation Approach

- Allocate a block of contiguous memory of size `n × element_size` bytes.
- To **access** element at index `i`: compute `base_address + i × size_of_element`. This is direct memory addressing — no traversal needed.
- To **insert at index i**: shift all elements from index `i` to `n-1` one position to the right, then place the new element at `i`. Update the size counter.
- To **delete at index i**: shift all elements from index `i+1` to `n-1` one position to the left. Update the size counter. No memory is freed in-place for static arrays.
- For a **dynamic array**: maintain a `capacity` (allocated space) and `size` (used space). When `size == capacity`, allocate a new array of double the capacity, copy all elements, and release the old memory.
- **Binary search** on a sorted array: maintain `low`, `high`, `mid` pointers. At each step, compare target with `mid`. Eliminate the irrelevant half. Repeat until found or `low > high`.

---

### 🔹 Variations / Modifications

- **Static Array** — Fixed size, allocated at compile time (e.g., C-style arrays).
- **Dynamic Array** — Resizes automatically (e.g., `ArrayList` in Java, `vector` in C++, `list` in Python).
- **2D / Multidimensional Array** — Array of arrays; used for matrices, grids.
- **Circular Array** — Last element logically connects back to first; used in queues.
- **Sparse Array** — Mostly zero/null values; use a map instead to save memory.
- **Bit Array / Bitset** — Array where each element is a single bit; extremely memory-efficient for boolean flags.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(1) random access | Fixed size (static arrays) |
| Cache-friendly (spatial locality) | O(n) insert/delete in middle |
| Simple to implement | Resizing is costly (copy entire array) |
| Supports binary search if sorted | Memory waste if over-allocated |

---

### 🔹 Interview Tips

- **Common Questions:** Two Sum, Maximum Subarray (Kadane's), Rotate Array, Merge Intervals, Next Permutation, Trapping Rain Water.
- **Tricky Points:**
  - Off-by-one errors in index calculations — always double-check boundary conditions.
  - Difference between `null` array and empty array.
  - Amortized O(1) for dynamic array append — be ready to explain the doubling strategy.
  - Interviewer may ask: "Why is insertion at the beginning O(n) and not O(1)?" — Answer: all subsequent elements must shift.
- **Mistakes to Avoid:**
  - Forgetting to handle edge cases: empty array, single element, all elements the same.
  - Confusing index-based loops with value-based — be precise.
  - Not clarifying if array is sorted before choosing a search strategy.

---

### 🔹 Real-World Use Cases

- **Databases:** Row-store engines store records in contiguous arrays of bytes.
- **Image Processing:** Pixel data of an image is stored as a 2D/3D array.
- **CPU Cache Design:** Cache lines exploit array contiguity for prefetching.
- **NumPy / Scientific Computing:** Arrays are the foundation of vectorized operations.
- **Heap (Priority Queue):** Internally stored as an array with index-based parent/child relationships.

---
---

## 2. 📚 Stack

### 🔹 Technical Definition

A **Stack** is a linear, abstract data structure that follows the **LIFO (Last In, First Out)** principle — the most recently inserted element is the first to be removed. It supports two primary operations: `push` (insert at top) and `pop` (remove from top). Access to elements below the top is not directly permitted without removal.

---

### 🔹 Intuition / Core Idea

- Think of a **stack of plates** — you add a plate to the top and always remove from the top.
- The key insight is **ordered reversal** — a stack reverses the order of operations, which is why it's used in undo mechanisms, recursion, and expression parsing.
- Used when: you need to track state in a LIFO manner — function calls, backtracking, nested structures.

---

### 🔹 Key Properties & Insights

- **LIFO** (Last In, First Out) — fundamental ordering property.
- Only the **top** element is accessible at any time.
- Can be implemented using an **array** (faster, fixed capacity) or **linked list** (dynamic, no overflow).
- **Call stack** in computer architecture is the most ubiquitous example.
- A stack can be used to simulate recursion iteratively.
- **Monotonic stack** — a stack that maintains elements in strictly increasing or decreasing order; powerful pattern for interval/range problems.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Push (insert at top) | O(1) | O(1) | O(1) |
| Pop (remove from top) | O(1) | O(1) | O(1) |
| Peek / Top (view top) | O(1) | O(1) | O(1) |
| Search (arbitrary element) | O(1) | O(n) | O(n) |
| IsEmpty | O(1) | O(1) | O(1) |

**Space Complexity:** `O(n)`

---

### 🔹 Verbal Explanation of Implementation Approach

**Array-based Stack:**
- Maintain an array of fixed size and an integer `top` initialized to `-1`.
- **Push:** Increment `top`, place new element at `array[top]`. Check for overflow (`top == capacity - 1`).
- **Pop:** Return `array[top]`, decrement `top`. Check for underflow (`top == -1`).
- **Peek:** Return `array[top]` without modifying `top`.

**Linked List-based Stack:**
- Maintain a pointer `head` to the top of the stack (front of the linked list).
- **Push:** Create a new node, point it to the current `head`, update `head` to the new node. O(1).
- **Pop:** Store the value of `head`, update `head` to `head.next`, discard the old node. O(1).
- No overflow unless system runs out of memory.

---

### 🔹 Variations / Modifications

- **Min Stack / Max Stack** — Stack that also supports retrieving minimum/maximum in O(1) by maintaining a parallel auxiliary stack.
- **Monotonic Stack (Increasing/Decreasing)** — Maintains sorted order; used for "next greater element" type problems.
- **Two-Stack Queue** — Simulating a queue using two stacks.
- **Persistent Stack** — Functional/immutable version; useful in version control-style applications.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(1) push/pop/peek | No random access |
| Simple and intuitive | Fixed capacity in array-based implementation |
| Ideal for LIFO scenarios | Linear search for non-top elements |
| Memory efficient | Stack overflow in deep recursion |

---

### 🔹 Interview Tips

- **Common Questions:** Valid Parentheses, Next Greater Element, Largest Rectangle in Histogram, Evaluate Reverse Polish Notation, Min Stack, Daily Temperatures.
- **Tricky Points:**
  - Monotonic stack pattern — must understand when to use increasing vs decreasing.
  - Simulating recursion using an explicit stack to avoid stack overflow.
  - The "balanced parentheses" problem is the stack's canonical interview question.
- **Mistakes to Avoid:**
  - Not checking for underflow before popping.
  - Confusing LIFO with FIFO in rushed explanations — always state LIFO clearly.

---

### 🔹 Real-World Use Cases

- **Browser History:** Back button uses a stack of visited URLs.
- **Undo/Redo:** Text editors store states on a stack.
- **Function Call Stack:** Operating systems manage function invocations via a call stack.
- **Expression Parsing:** Compilers convert infix → postfix and evaluate expressions using stacks.
- **Depth-First Search (DFS):** Iterative DFS uses an explicit stack.
- **Syntax Checking:** IDEs validate bracket/brace matching using a stack.

---
---

## 3. 🚶 Queue

### 🔹 Technical Definition

A **Queue** is a linear abstract data structure following the **FIFO (First In, First Out)** principle — elements are inserted at the **rear (enqueue)** and removed from the **front (dequeue)**. It models a real-world waiting line where the first entity to arrive is the first to be served.

---

### 🔹 Intuition / Core Idea

- Think of a **line at a ticket counter** — the person who arrives first gets served first.
- Queues are essential when **order of arrival must be preserved** for processing.
- Used when: tasks need to be processed in the order they were received — CPU scheduling, network packets, BFS traversal.

---

### 🔹 Key Properties & Insights

- **FIFO** (First In, First Out) — ordering guarantee.
- Two ends: **Front** (dequeue side) and **Rear** (enqueue side).
- Can be implemented via **array** (risk of queue overflow with front pointer drift), **circular array** (efficient space usage), or **linked list** (dynamic size).
- **Priority Queue** is a variation where elements have priority and highest priority element is dequeued first.
- **Deque (Double-Ended Queue)** allows insertions and deletions from both ends.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Enqueue (insert at rear) | O(1) | O(1) | O(1) |
| Dequeue (remove from front) | O(1) | O(1) | O(1) |
| Peek / Front | O(1) | O(1) | O(1) |
| Search | O(1) | O(n) | O(n) |
| IsEmpty | O(1) | O(1) | O(1) |

**Space Complexity:** `O(n)`

---

### 🔹 Verbal Explanation of Implementation Approach

**Circular Array-based Queue:**
- Maintain an array, `front` pointer (initialized to 0), `rear` pointer (initialized to -1), and `size` counter.
- **Enqueue:** `rear = (rear + 1) % capacity`, place element at `array[rear]`, increment `size`.
- **Dequeue:** Read `array[front]`, `front = (front + 1) % capacity`, decrement `size`.
- Use modulo arithmetic to wrap around — this prevents wasted space from simple front-pointer drift.
- Queue is full when `size == capacity`; empty when `size == 0`.

**Linked List-based Queue:**
- Maintain `head` (front pointer) and `tail` (rear pointer).
- **Enqueue:** Create new node, attach to `tail.next`, move `tail` to new node.
- **Dequeue:** Read `head.value`, advance `head` to `head.next`.
- Both operations are O(1) with the tail pointer — never traverse the list.

---

### 🔹 Variations / Modifications

- **Circular Queue** — Array-based queue using modulo arithmetic to reuse freed front spaces.
- **Priority Queue (Heap-based)** — Elements dequeued by priority, not arrival order. Backed by a binary heap.
- **Deque (Double-Ended Queue)** — Insert/delete from both ends. Used in sliding window problems.
- **Monotonic Deque** — Maintains sliding window maximum/minimum in O(n) total.
- **Blocking Queue** — Thread-safe queue; threads block when queue is empty/full. Used in producer-consumer problems.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(1) enqueue and dequeue | No random access |
| Preserves order of arrival | Simple array queue wastes space without circular logic |
| Natural fit for BFS and scheduling | Priority queue needs a heap for efficient priority access |

---

### 🔹 Interview Tips

- **Common Questions:** BFS on graphs/trees, Sliding Window Maximum (Monotonic Deque), LRU Cache (Queue + HashMap), Implement Queue using Stacks, First Non-Repeating Character in Stream.
- **Tricky Points:**
  - Circular queue implementation — getting modulo arithmetic right without off-by-one errors.
  - Knowing when to use a deque vs a regular queue.
  - Distinguishing between queue (FIFO) and priority queue (order by priority).
- **Mistakes to Avoid:**
  - Forgetting that BFS uses a queue — not a stack.
  - Not handling the empty queue case before dequeue.

---

### 🔹 Real-World Use Cases

- **OS Process Scheduling:** Ready queue holds processes waiting for CPU time.
- **Network Routers:** Packet queues manage transmission order.
- **BFS Traversal:** Level-order traversal of trees/graphs.
- **Print Spooling:** Print jobs queued and served in order.
- **Asynchronous Task Queues:** Message brokers like RabbitMQ, Kafka use queue semantics.

---
---

## 4. 🔗 Singly Linked List

### 🔹 Technical Definition

A **Singly Linked List** is a dynamic linear data structure consisting of **nodes**, where each node stores a **data value** and a **single pointer (next)** to the subsequent node in the sequence. The list is accessed from a **head** pointer; the last node's `next` pointer is `null`, marking the list's end.

---

### 🔹 Intuition / Core Idea

- Think of a **treasure hunt** — each clue (node) tells you where the next clue is. You can only move forward.
- Unlike arrays, nodes are **not contiguous in memory** — the pointer links them logically.
- Excels at **dynamic insertion/deletion** at the head in O(1), without the shifting cost of arrays.

---

### 🔹 Key Properties & Insights

- **Unidirectional traversal** — can only traverse forward (head → tail).
- **No random access** — must traverse from head to reach index `i`; O(n).
- **Dynamic size** — grows and shrinks at runtime; no pre-allocation needed.
- **Head pointer** is the sole entry point — losing it means losing the entire list.
- **Tail insertion** requires traversal unless a tail pointer is maintained separately.
- Naturally supports **recursive algorithms** (each node is a subproblem).

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Access by Index | O(1) (head) | O(n) | O(n) |
| Search | O(1) | O(n) | O(n) |
| Insert at Head | O(1) | O(1) | O(1) |
| Insert at Tail (with tail ptr) | O(1) | O(1) | O(1) |
| Insert at Middle (by index) | O(1) | O(n) | O(n) |
| Delete at Head | O(1) | O(1) | O(1) |
| Delete at Tail | O(n) | O(n) | O(n) |
| Delete by Value | O(1) | O(n) | O(n) |
| Traversal | O(n) | O(n) | O(n) |

**Space Complexity:** `O(n)` + pointer overhead per node

---

### 🔹 Verbal Explanation of Implementation Approach

- Each **node** contains two fields: `data` and `next` pointer.
- **Insert at head:** Create a new node. Set `new_node.next = head`. Update `head = new_node`. Entire operation is O(1).
- **Insert at tail:** Traverse from head until `current.next == null`. Set `current.next = new_node`. O(n) without a tail pointer, O(1) with one.
- **Insert at index i:** Traverse to node at index `i-1` (the predecessor). Set `new_node.next = predecessor.next`. Set `predecessor.next = new_node`.
- **Delete by value:** Traverse while tracking `previous` and `current` nodes. When `current.data == target`, set `previous.next = current.next`. Discard `current`.
- **Delete at head:** Simply move `head = head.next`. Old head is dereferenced.
- **Detecting a cycle:** Use Floyd's Tortoise and Hare algorithm — slow pointer moves 1 step, fast pointer moves 2. If they meet, a cycle exists.

---

### 🔹 Variations / Modifications

- **Sorted Linked List** — Maintains sorted order; insertion finds correct position.
- **XOR Linked List** — Each node stores XOR of previous and next address; reduces pointer memory, complex to traverse.
- **Self-Organizing List** — Frequently accessed nodes move to the front; improves average access time.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(1) head insert/delete | O(n) random access (no indexing) |
| Dynamic size — no pre-allocation | Extra memory per node (pointer overhead) |
| Efficient for streaming data | No reverse traversal |
| No shifting during insert/delete | Cache-unfriendly (non-contiguous memory) |

---

### 🔹 Interview Tips

- **Common Questions:** Reverse a Linked List, Detect Cycle (Floyd's), Find Middle Node, Merge Two Sorted Lists, Remove Nth Node from End, Palindrome Linked List, Intersection of Two Lists.
- **Tricky Points:**
  - Always handle the `null` head case.
  - When deleting a node with only access to that node (not head): copy next node's data into current, delete next node — classic trick.
  - Two-pointer technique (fast/slow) solves many linked list problems elegantly.
  - Reversing iteratively requires three pointers: `prev`, `curr`, `next`.
- **Mistakes to Avoid:**
  - Losing the head pointer — always store it before modification.
  - Not updating the tail pointer when maintaining one.
  - Infinite loops from improper null checks.

---

### 🔹 Real-World Use Cases

- **Memory Allocators:** Free list of memory blocks is a linked list.
- **Browser Tab History:** Linked structure of visited pages.
- **Music Playlist:** Each song links to the next.
- **Hash Table Chaining:** Each bucket holds a linked list of colliding entries.
- **Undo Buffer in Editors:** Linked list of state snapshots.

---
---

## 5. ↔️ Doubly Linked List

### 🔹 Technical Definition

A **Doubly Linked List** is a linear data structure where each node contains a **data value**, a **next** pointer (to the successor node), and a **prev** pointer (to the predecessor node). Traversal is possible in **both directions**, and both the `head` and `tail` pointers are typically maintained.

---

### 🔹 Intuition / Core Idea

- Think of a **two-way street** — you can move forward or backward between nodes.
- The extra `prev` pointer doubles memory per node but unlocks **O(1) deletion** when you have a direct reference to a node — no need to find the predecessor by traversal.
- Used when: bidirectional traversal is needed, or O(1) deletion from anywhere is critical.

---

### 🔹 Key Properties & Insights

- **Bidirectional traversal** — can traverse forward and backward.
- **O(1) deletion** given a direct node reference — no predecessor traversal needed (use `node.prev`).
- More **memory per node** — two pointers instead of one.
- Maintaining **both head and tail** makes prepend and append O(1).
- Basis of the **LRU Cache** — most recently used node moves to head; least recently used removed from tail.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Access by Index | O(1) (head/tail) | O(n) | O(n) |
| Search | O(1) | O(n) | O(n) |
| Insert at Head | O(1) | O(1) | O(1) |
| Insert at Tail | O(1) | O(1) | O(1) |
| Insert at Middle | O(1) | O(n) | O(n) |
| Delete given Node Ref | O(1) | O(1) | O(1) |
| Delete by Value | O(1) | O(n) | O(n) |
| Traversal (Forward/Backward) | O(n) | O(n) | O(n) |

**Space Complexity:** `O(n)` — but with 2× pointer overhead vs singly linked list

---

### 🔹 Verbal Explanation of Implementation Approach

- Each node: `prev`, `data`, `next`.
- **Insert at head:** Create new node. Set `new_node.next = head`, `head.prev = new_node`, `new_node.prev = null`. Update `head = new_node`.
- **Insert at tail:** Create new node. Set `tail.next = new_node`, `new_node.prev = tail`, `new_node.next = null`. Update `tail = new_node`.
- **Delete a given node:** Set `node.prev.next = node.next` and `node.next.prev = node.prev`. Handle edge cases where node is head or tail separately.
- Always update **both** `prev` and `next` pointers during any insert/delete — forgetting either creates a broken link.
- Use **sentinel/dummy head and tail nodes** (common pattern) to eliminate edge case handling for head/tail deletion — all operations become uniform.

---

### 🔹 Variations / Modifications

- **Doubly Linked List with Sentinel Nodes** — Dummy head and tail nodes simplify boundary handling.
- **Skip List** — Built on top of linked lists with additional level-based shortcut pointers.
- **LRU Cache (HashMap + DLL)** — The canonical use case: O(1) get and put.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(1) deletion given node reference | 2× pointer memory overhead |
| Bidirectional traversal | More complex insert/delete logic (update 2 pointers) |
| O(1) insert/delete at both ends | Still no O(1) random access |

---

### 🔹 Interview Tips

- **Common Questions:** LRU Cache, Flatten a Multilevel Doubly Linked List, Design Browser History, All O(1) Data Structure.
- **Tricky Points:**
  - LRU Cache is the most important doubly linked list interview question — must know it cold.
  - Always update both `prev` and `next` on every operation.
  - Sentinel nodes pattern — worth mentioning as it simplifies implementation.
- **Mistakes to Avoid:**
  - Forgetting to update the `tail.prev` when deleting the tail node.
  - Memory leaks — ensure removed nodes are properly dereferenced.

---

### 🔹 Real-World Use Cases

- **LRU Cache:** Most critical real-world use — `HashMap` maps keys to DLL nodes; DLL maintains usage order.
- **Browser Forward/Back Navigation:** Doubly linked structure of pages.
- **Text Editors (Rope / Gap Buffer):** Some editors represent text as a DLL of blocks.
- **Thread Schedulers:** OS run queues use doubly linked lists for O(1) removal.
- **Music Players:** Playlist with previous/next track navigation.

---
---

## 6. 🔄 Circular Linked List

### 🔹 Technical Definition

A **Circular Linked List** is a linked list variant in which the **last node's `next` pointer points back to the first node (head)** instead of `null`, forming a closed cycle. It can be singly or doubly circular. There is no natural `null` terminator — traversal must be controlled by a stop condition based on revisiting the start node.

---

### 🔹 Intuition / Core Idea

- Think of players **sitting in a circle** — after the last player, you're back to the first. There is no "end."
- The circular structure eliminates the concept of a head/tail distinction when all positions are logically equivalent.
- Ideal for **round-robin scheduling**, cyclic buffers, and any problem requiring repeated cycling.

---

### 🔹 Key Properties & Insights

- **No null terminator** — the last node points to the head.
- For traversal, stop when you revisit the starting node.
- Maintaining a **tail pointer** (instead of head) is often more convenient — tail gives O(1) access to both tail and head (via `tail.next`).
- A singly circular list allows O(1) insertion at both front and back when a tail pointer is maintained.
- **Cycle detection algorithms** (Floyd's) are often tested on circular lists.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Insert at Beginning | O(1) | O(1) | O(1) |
| Insert at End (with tail ptr) | O(1) | O(1) | O(1) |
| Insert at Middle | O(n) | O(n) | O(n) |
| Delete at Beginning | O(1) | O(1) | O(1) |
| Delete at End | O(n) | O(n) | O(n) |
| Search | O(1) | O(n) | O(n) |
| Traversal | O(n) | O(n) | O(n) |

**Space Complexity:** `O(n)`

---

### 🔹 Verbal Explanation of Implementation Approach

- The key difference from a singly linked list: **last node's next = head** (not null).
- **Insert at beginning (using tail pointer):** Create new node. Set `new_node.next = tail.next` (current head). Set `tail.next = new_node`. This inserts at front in O(1).
- **Insert at end (using tail pointer):** Insert at beginning first, then move tail pointer forward: `tail = tail.next`.
- **Traversal:** Start at head. Iterate using `current = current.next`. Stop when `current == head` (not when `current == null`).
- **Delete beginning:** `tail.next = tail.next.next` (skip the head node).
- To **split a circular list into two:** Find the midpoint (using slow/fast pointers), adjust pointers to create two separate circular lists.

---

### 🔹 Variations / Modifications

- **Singly Circular Linked List** — Standard form.
- **Doubly Circular Linked List** — Both next and prev pointers form cycles; used in some OS scheduler implementations.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| No null checks during traversal | Infinite loop risk if stop condition is wrong |
| O(1) insert at front and back (with tail ptr) | Harder to detect end of list |
| Natural for cyclic/round-robin problems | Slightly more complex pointer management |

---

### 🔹 Interview Tips

- **Common Questions:** Josephus Problem, Round-Robin Scheduling Simulation, Split Circular List, Detect if a List is Circular.
- **Tricky Points:**
  - Always include a guard against infinite loops during traversal.
  - The tail pointer (not head) is more useful for circular lists.
  - Prefer circular lists when the problem inherently involves cycling.
- **Mistakes to Avoid:**
  - Using `current != null` as the loop termination — this will never be true in a circular list.

---

### 🔹 Real-World Use Cases

- **CPU Round-Robin Scheduling:** OS cycles through processes in a circular queue.
- **Circular Buffer / Ring Buffer:** Fixed-size buffer where the producer and consumer wrap around.
- **Multiplayer Games:** Turn rotation (Player 1 → 2 → 3 → 1).
- **Token Ring Network Protocol:** Circular topology with a token passed around the ring.

---
---

## 7. 🚀 Skip List

### 🔹 Technical Definition

A **Skip List** is a probabilistic data structure built on layered **sorted singly linked lists**. It maintains multiple levels of forward pointers — the bottom level contains all elements, and each higher level contains a progressively sparse subset (each element is promoted with probability `p`, typically `0.5`). This enables O(log n) expected search by skipping over large sections of the list.

---

### 🔹 Intuition / Core Idea

- Think of an **express train system** — you have local trains (bottom level, all stops) and express trains (higher levels, fewer stops). You take express as far as possible, then switch to local.
- The skip list achieves balanced-tree-like performance without complex rotations — it relies on **randomization** for balance.
- Used when: you need a sorted dynamic data structure without the implementation complexity of a balanced BST.

---

### 🔹 Key Properties & Insights

- **Probabilistic balancing** — height of each node determined by coin flips; expected O(log n) height.
- **Multiple levels** — Level 0 has all elements; Level `k` has ~n/2^k elements.
- **Forward pointers** — each node at level `k` stores pointers to the next node at every level from 0 to `k`.
- Expected space: O(n) — each element appears on average in O(1/p) levels.
- Supports **efficient range queries** — traverse level 0 from found lower bound.
- Concurrent skip lists are significantly easier to implement correctly than concurrent balanced trees.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Search | O(1) | O(log n) | O(n) |
| Insert | O(1) | O(log n) | O(n) |
| Delete | O(1) | O(log n) | O(n) |
| Range Query | O(log n) | O(log n + k) | O(n) |
| Traversal (sorted order) | O(n) | O(n) | O(n) |

*Worst case is O(n) due to probabilistic nature — extremely rare in practice.*

**Space Complexity:** `O(n)` expected, `O(n log n)` worst case

---

### 🔹 Verbal Explanation of Implementation Approach

- Initialize with a **header node** with the maximum number of levels, all pointing to a **nil sentinel** node.
- **Search:** Start at the highest level of the header. At each node, compare the target with the next node. If next is smaller, advance forward. If next is larger or nil, drop down one level. Repeat until level 0, then check if found.
- **Insert:**
  - Perform a search and record the predecessor node at each level in an `update[]` array.
  - Randomly determine the height of the new node (flip coins until tails).
  - Create the new node. For each level from 0 to new node's height: splice the new node in after `update[level]` at that level.
- **Delete:**
  - Search and populate `update[]` array.
  - For each level, if `update[level].next == target_node`, bypass it: `update[level].next = target.next[level]`.
  - Reduce the list's max level if top levels become empty.

---

### 🔹 Variations / Modifications

- **Deterministic Skip List (1-2 Skip List)** — Uses deterministic promotion rules instead of randomization; guarantees O(log n) worst case.
- **Concurrent Skip List** — Lock-free versions using CAS (Compare-And-Swap); used in Java's `ConcurrentSkipListMap`.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| Simple to implement vs balanced BSTs | Probabilistic — no hard worst-case guarantee |
| O(log n) expected for all operations | More memory than a simple sorted linked list |
| Cache-friendlier than trees in some cases | Randomness makes performance non-deterministic |
| Easy concurrent implementation | Less commonly taught — may be unfamiliar |

---

### 🔹 Interview Tips

- **Common Questions:** Typically conceptual — "How does a Skip List work?", "How does it compare to a BST?", "What is the time complexity and why?", Design a Skip List (LeetCode 1206).
- **Tricky Points:**
  - The randomized promotion mechanism — be ready to explain the coin-flip analogy.
  - Why the expected height is O(log n).
  - The `update[]` array pattern during insert/delete.
- **Mistakes to Avoid:**
  - Claiming O(log n) worst case — it is expected/average, not worst case.
  - Forgetting the sentinel nil node at the end.

---

### 🔹 Real-World Use Cases

- **Redis Sorted Sets (`ZSET`):** Internally uses a skip list for sorted score-based operations.
- **LevelDB / RocksDB:** Uses skip lists for in-memory memtable.
- **Java `ConcurrentSkipListMap`:** Thread-safe sorted map in the JDK.
- **Lucene (Full-Text Search):** Skip lists for faster posting list traversal.

---
---

## 8. 🗂️ Hash Table

### 🔹 Technical Definition

A **Hash Table** (also called Hash Map) is a data structure that maps **keys to values** using a **hash function** to compute an index (bucket) into an array where the value is stored. It provides expected O(1) time for insert, delete, and search operations. Collisions — when two keys hash to the same index — are resolved using chaining or open addressing.

---

### 🔹 Intuition / Core Idea

- Think of a **library with a smart indexing system** — rather than searching every shelf, the index (hash function) instantly tells you which shelf (bucket) holds your book.
- The hash function converts any key (string, integer, object) into a fixed-range integer index.
- The fundamental trade-off: **space for speed** — pre-allocating an array of buckets buys O(1) lookup.

---

### 🔹 Key Properties & Insights

- **Hash function** must be deterministic, fast, and uniformly distribute keys.
- **Load factor** (`α = n/m`, where n = elements, m = buckets) — as load factor increases, collision probability rises and performance degrades.
- **Rehashing** — when load factor exceeds a threshold (typically 0.75), the table is resized and all elements are re-inserted into a new larger table.
- **Collision** is unavoidable when keys > buckets (Pigeonhole Principle).
- Order is **not preserved** — hash tables are unordered by nature.
- A good hash function for strings: polynomial rolling hash — `hash = Σ (char[i] × p^i) mod m`.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Insert | O(1) | O(1) | O(n) |
| Search / Lookup | O(1) | O(1) | O(n) |
| Delete | O(1) | O(1) | O(n) |
| Traversal (all keys) | O(m) | O(m+n) | O(m+n) |

*Worst case O(n) occurs with a poor hash function causing all elements to cluster in one bucket.*

**Space Complexity:** `O(n)` — with potential for sparse table overhead

---

### 🔹 Verbal Explanation of Implementation Approach

**Chaining (Separate Chaining):**
- Array of linked lists (or dynamic arrays). Each bucket stores a list of all keys that hash to it.
- **Insert:** Compute `hash(key) % m`. Append (or prepend) `(key, value)` to the list at that bucket.
- **Search:** Hash the key, go to that bucket, traverse the list to find a matching key.
- **Delete:** Hash, traverse the bucket's list, remove matching node.
- Load factor can exceed 1. Easy to implement. Each list can grow independently.

**Open Addressing:**
- All elements stored in the array itself — no separate chains.
- **Insert:** Hash the key; if the slot is occupied, probe for the next available slot.
  - **Linear Probing:** Check `(hash + 1) % m`, `(hash + 2) % m`, etc. Suffers from primary clustering.
  - **Quadratic Probing:** Check `(hash + 1²) % m`, `(hash + 2²) % m`. Reduces clustering.
  - **Double Hashing:** Use a second hash function to determine step size. Best distribution.
- **Delete:** Must use a **tombstone** marker — simply clearing a slot breaks the probe chain for subsequent lookups.

---

### 🔹 Variations / Modifications

- **Chaining vs Open Addressing:** Chaining is simpler and handles high load factors better; open addressing is more cache-friendly.
- **Cuckoo Hashing** — Two hash functions, two tables; guaranteed O(1) worst-case lookup.
- **Robin Hood Hashing** — Open addressing where richer elements "steal" from poorer ones to minimize variance in probe lengths.
- **Perfect Hashing** — For static key sets, a two-level scheme guarantees O(1) worst case.
- **Consistent Hashing** — Used in distributed systems (database sharding, CDNs) to minimize rehashing when nodes are added/removed.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(1) average insert/search/delete | Unordered — no sorted traversal |
| Flexible key types with custom hash functions | Worst case O(n) with poor hash or many collisions |
| Foundation of many advanced data structures | Resizing (rehashing) is O(n) and can cause latency spikes |
| Simple API | Extra memory overhead (load factor < 1 typically) |

---

### 🔹 Interview Tips

- **Common Questions:** Two Sum, Group Anagrams, Longest Consecutive Sequence, LRU Cache, Top K Frequent Elements, Valid Anagram, Subarray Sum Equals K.
- **Tricky Points:**
  - Why load factor matters — must be able to explain degradation at high load.
  - Tombstone deletion in open addressing — forgetting this breaks lookups.
  - Why rehashing is needed and what the amortized cost is.
  - Collision resolution strategies — know both chaining and at least one open addressing method.
- **Mistakes to Avoid:**
  - Claiming O(1) worst case — it is O(1) **average** case.
  - Forgetting that dictionary/map iteration order is undefined (unless `LinkedHashMap` / ordered dict).
  - Not handling `null` keys — some implementations support them, some don't.

---

### 🔹 Real-World Use Cases

- **Database Indexing (Hash Index):** Direct lookup by exact key match.
- **Compilers:** Symbol tables storing variable names and their attributes.
- **Caching (Memcached, Redis):** Key-value store at the core.
- **DNS Resolution:** Domain name to IP mapping cached in hash tables.
- **Set Implementations:** `HashSet` is a hash table storing only keys.
- **Routing Tables:** Network switches use hash tables for fast MAC address lookup.

---
---

## 9. 🌳 Binary Search Tree (BST)

### 🔹 Technical Definition

A **Binary Search Tree** is a rooted binary tree where each node stores a key, and satisfies the **BST property**: for every node `N`, all keys in `N`'s left subtree are **strictly less than** `N.key`, and all keys in `N`'s right subtree are **strictly greater than** `N.key`. This property holds recursively for every subtree.

---

### 🔹 Intuition / Core Idea

- Think of a **decision tree for a guessing game** — at every node, you ask "Is it smaller or larger?" and go left or right. Each comparison eliminates half the remaining tree (in a balanced case).
- The BST property imposes a natural **total order** — an in-order traversal always yields elements in sorted order.

---

### 🔹 Key Properties & Insights

- **In-order traversal** (Left → Root → Right) yields sorted keys — a fundamental property.
- **Height** determines performance: balanced BST has height O(log n); a degenerate (sorted insertion) BST degrades to O(n).
- **No duplicate keys** in a standard BST (handle duplicates by convention: left for ≤ or right for ≥, consistently).
- **Predecessor and Successor** can be found without storing parent pointers — in-order predecessor is the rightmost node of the left subtree; in-order successor is the leftmost node of the right subtree.
- A BST with n nodes can have heights ranging from `⌊log₂n⌋` (perfectly balanced) to `n-1` (fully degenerate/linked list shape).

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Search | O(1) | O(log n) | O(n) |
| Insert | O(log n) | O(log n) | O(n) |
| Delete | O(log n) | O(log n) | O(n) |
| Min / Max | O(1) (maintained) | O(log n) | O(n) |
| In-order Traversal | O(n) | O(n) | O(n) |
| Find Successor/Predecessor | O(log n) | O(log n) | O(n) |

**Space Complexity:** `O(n)` — O(h) additional for recursive stack

---

### 🔹 Verbal Explanation of Implementation Approach

- **Search:** Start at root. If target < current, go left. If target > current, go right. If equal, found. If null, not found.
- **Insert:** Follow search path until a null child position is found. Create a new node there.
- **Delete (3 cases):**
  1. **Node is a leaf:** Simply remove it (set parent's pointer to null).
  2. **Node has one child:** Bypass the node — connect parent directly to the node's child.
  3. **Node has two children:** Find the **in-order successor** (leftmost node of right subtree). Copy its key into the current node. Delete the in-order successor (which has at most one child — simpler case).
- **Finding Min:** Follow left pointers until left child is null.
- **Finding Max:** Follow right pointers until right child is null.
- **In-order Traversal (recursive):** Recurse on left subtree → visit current → recurse on right subtree.

---

### 🔹 Variations / Modifications

- **Balanced BSTs** — AVL Tree, Red-Black Tree, Splay Tree prevent O(n) degradation.
- **Augmented BST** — Each node stores additional information (subtree size, min/max) to support order-statistics queries.
- **Threaded BST** — Null pointers replaced with pointers to in-order predecessor/successor; enables O(1) traversal without a stack.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(log n) operations on balanced tree | Degrades to O(n) on sorted input (unbalanced) |
| In-order gives sorted output | No automatic balancing in plain BST |
| Supports range queries naturally | More complex implementation than a hash table |
| Floor/ceiling/predecessor operations | Pointer overhead per node |

---

### 🔹 Interview Tips

- **Common Questions:** Validate BST, LCA of BST, Kth Smallest in BST, Convert BST to Sorted Array, BST Iterator, Delete Node in BST, Recover BST (two nodes swapped).
- **Tricky Points:**
  - BST validation — must pass min/max bounds down the recursion, not just check parent.
  - The three-case delete is always tested — must know it cold.
  - LCA in BST is O(log n) — much simpler than LCA in a general binary tree.
- **Mistakes to Avoid:**
  - Checking only immediate parent-child order when validating — this misses the global BST property.
  - Forgetting that in-order successor may be in the right subtree's leftmost node, not the right child itself.

---

### 🔹 Real-World Use Cases

- **Database Indexes (B-Tree variant):** Core of most relational database index structures.
- **Dynamic Sets / Maps (std::map in C++):** Red-Black Tree backed sorted map.
- **File Systems:** Directory structures in some filesystems use BST-like structures.
- **Symbol Tables in Compilers:** For sorted, range-queryable symbol lookup.

---
---

## 10. 🃏 Cartesian Tree

### 🔹 Technical Definition

A **Cartesian Tree** is a binary tree derived from a sequence of values (typically array elements) that simultaneously satisfies two properties: the **in-order traversal** of the tree yields the original array sequence (BST property on indices), and it is a **min-heap (or max-heap)** — every parent's value is smaller (or larger) than its children. It is defined uniquely for a sequence with distinct values.

---

### 🔹 Intuition / Core Idea

- Think of it as a **BST over array indices** but also a **heap over values** — both structures simultaneously.
- The root is always the **minimum (or maximum) element** of the array. Its left subtree is the Cartesian tree of the subarray to the left of this element, and its right subtree is that of the subarray to the right.
- Powerful for **Range Minimum Query (RMQ)** — the LCA (Lowest Common Ancestor) of two nodes in a Cartesian tree corresponds to the minimum element in the range between those indices.

---

### 🔹 Key Properties & Insights

- **Uniquely defined** for arrays with distinct elements.
- **In-order = original array order** (index-based BST property).
- **Heap property on values** — root is always the min/max of the entire array.
- LCA in Cartesian tree → RMQ in original array.
- Can be built in **O(n)** using a stack-based algorithm.
- Closely related to **Treap** (Cartesian Tree with random priorities).

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Build from Array | O(n) | O(n) | O(n) |
| Search by Index | O(log n) | O(log n) | O(n) |
| Range Min Query (via LCA) | O(1) with preprocessing | O(log n) | O(n) |
| Insert | O(log n) | O(log n) | O(n) |

**Space Complexity:** `O(n)`

---

### 🔹 Verbal Explanation of Implementation Approach

- **Stack-based O(n) construction:**
  - Maintain a stack representing the **rightmost path** of the tree built so far.
  - For each new element in the array:
    - Pop all elements from the stack that have a **value greater than** the current element (for a min-Cartesian tree).
    - The last popped element becomes the **left child** of the new node (it was to the left in the array).
    - The new node becomes the **right child** of the current top of the stack (what remains).
    - Push the new node onto the stack.
  - The bottom of the stack at the end is the root.
- This works because we maintain the heap property (smaller values higher up) while preserving in-order sequence.

---

### 🔹 Variations / Modifications

- **Max-Cartesian Tree** — Heap property is max instead of min; root is the array maximum.
- **Treap** — Cartesian Tree where keys are the actual data and priorities are random values; acts as a randomized BST.
- **Implicit Treap** — Index-based Treap where the BST key is the implicit index; supports O(log n) array split/merge.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(n) build time | Not self-balancing |
| Enables O(1) RMQ with preprocessing | Less intuitive than BST or heap individually |
| Foundation of Treap (randomized BST) | Rarely needed outside competitive programming |

---

### 🔹 Interview Tips

- **When asked:** Typically appears in the context of RMQ, Treaps, or as a conceptual question.
- **Key insight to state:** "The LCA of two nodes equals the RMQ answer for that range."
- **Tricky Points:** The O(n) stack-based construction — be ready to trace through an example.
- **Mistakes to Avoid:** Confusing Cartesian Tree (deterministic, built from array) with a Treap (uses random priorities).

---

### 🔹 Real-World Use Cases

- **Range Minimum Query Preprocessing:** Used with LCA algorithms for O(1) RMQ.
- **Treap implementations:** Redis sorted sets are backed by skip lists, but some systems use Treaps.
- **Suffix Arrays + LCP Arrays:** Cartesian tree of the LCP array is used in string algorithms.

---
---

## 11. 🗄️ B-Tree

### 🔹 Technical Definition

A **B-Tree** of order `m` is a self-balancing, multi-way search tree where every node can hold between `⌈m/2⌉ - 1` and `m - 1` keys, and have between `⌈m/2⌉` and `m` children. All leaf nodes are at the **same depth** (perfectly height-balanced). It is specifically designed to minimize **disk I/O** by maximizing the number of keys per node, reducing tree height.

---

### 🔹 Intuition / Core Idea

- Think of a **library catalog with multiple entries per card** — instead of one key per node (like a BST), each node holds many keys, allowing you to cover large ranges with a single disk read.
- B-Trees are designed for **secondary storage (HDD/SSD)** where each disk block read is expensive. A fat, short tree minimizes the number of block reads.
- Every lookup, insert, and delete requires at most O(log_m n) disk accesses.

---

### 🔹 Key Properties & Insights

- **All leaves at same level** — perfectly balanced by height.
- **Order m** means: max `m` children per node, max `m-1` keys per node.
- **Minimum fill constraint** — each non-root node must be at least half full. Prevents excessive emptiness after deletions.
- A B-Tree of order 3 is called a **2-3 Tree** (each node has 2 or 3 children).
- **B+ Tree** (most common variant): only leaf nodes store actual data records; internal nodes store only keys for routing. Leaves are linked as a linked list for efficient range scans.
- Disk block size typically dictates the order `m` of a B-Tree in practice.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Search | O(log n) | O(log n) | O(log n) |
| Insert | O(log n) | O(log n) | O(log n) |
| Delete | O(log n) | O(log n) | O(log n) |
| Range Query | O(log n + k) | O(log n + k) | O(log n + k) |
| Traversal (in-order) | O(n) | O(n) | O(n) |

*`k` = number of elements in range. All operations are O(log n) — no degraded case unlike plain BST.*

**Space Complexity:** `O(n)`

---

### 🔹 Verbal Explanation of Implementation Approach

- **Search:** Start at root. At each node, binary search within the node's keys to find which child pointer to follow. Descend until found or reach a leaf (not found).
- **Insert:**
  - Search for the correct leaf. Insert the key in sorted order within the leaf.
  - If the leaf **overflows** (exceeds m-1 keys), **split** it: promote the median key to the parent node; create two child nodes from the left and right halves.
  - Splitting may propagate upward — if the parent also overflows, split it too.
  - If the root splits, a **new root** is created — this is the only way the tree grows in height.
- **Delete:**
  - If the key is in an internal node: replace it with its in-order predecessor/successor (which is in a leaf), then delete from the leaf.
  - After deletion, if a leaf/node **underflows** (below minimum fill), either:
    - **Borrow** a key from a sibling (via the parent, called rotation).
    - Or **merge** with a sibling, pulling the separator key down from the parent.
  - Merging may propagate upward similarly to splitting.

---

### 🔹 Variations / Modifications

- **B+ Tree** — Internal nodes store only routing keys; all data in leaves; leaves linked for range scans. Used in virtually all RDBMS indexes.
- **B* Tree** — Nodes must be at least 2/3 full instead of 1/2. Delays splits; more space-efficient.
- **2-3 Tree** — B-Tree of order 3; commonly used to teach B-Tree concepts.
- **2-3-4 Tree** — Equivalent to a Red-Black Tree; bridge between B-Trees and in-memory BSTs.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(log n) guaranteed for all operations | Complex implementation (split/merge logic) |
| Optimized for disk I/O (high branching factor) | Overkill for in-memory data (overhead not worth it) |
| Supports efficient range queries | Not ideal for very small datasets |
| Always balanced — no degenerate case | Higher memory per node for multi-key storage |

---

### 🔹 Interview Tips

- **Common Questions:** Conceptual — "How does a database index work?", "How does a B+ Tree differ from a B-Tree?", "Why use a B-Tree over a BST for disk storage?"
- **Key Statement:** "B-Trees reduce tree height by increasing branching factor. Since each disk block read is expensive, we want to maximize keys per read and minimize total reads."
- **Tricky Points:**
  - B+ Tree vs B-Tree distinction — interviewers often ask this specifically.
  - Splitting and merging logic during insert/delete.
- **Mistakes to Avoid:**
  - Confusing B-Tree with Binary Tree — they are unrelated. "B" stands for Bayer (inventor's name), balanced, broad, or bushy.

---

### 🔹 Real-World Use Cases

- **Relational Databases (InnoDB, PostgreSQL):** Primary and secondary indexes are B+ Trees.
- **File Systems (NTFS, ext4, HFS+):** Directory structures and file allocation tables use B-Tree variants.
- **SQLite:** B+ Tree for both table data (row-ID based) and indexes.
- **MongoDB (WiredTiger engine):** B-Tree based storage engine.

---
---

## 12. 🔴⚫ Red-Black Tree

### 🔹 Technical Definition

A **Red-Black Tree** is a self-balancing BST where each node is colored **red** or **black**, and the tree satisfies five properties that collectively guarantee the tree's height remains O(log n). It is a specialization of a 2-3-4 Tree and is widely used as the underlying structure for `TreeMap`, `TreeSet`, and `std::map`.

---

### 🔹 Intuition / Core Idea

- Think of it as a BST that **enforces balance through color rules** — instead of precisely measuring and correcting height imbalance (like AVL), the color invariants ensure no path is more than twice as long as another, bounding height to 2 log n.
- Red-Black Trees prefer **faster insertions and deletions** (fewer rotations) over strict height balance, making them preferred in practice over AVL Trees for write-heavy workloads.

---

### 🔹 Key Properties & Insights (The 5 Red-Black Properties)

1. Every node is either **Red** or **Black**.
2. The **root** is always **Black**.
3. Every **null leaf (NIL node)** is Black.
4. A **Red node** cannot have a Red child — no two consecutive red nodes on any path.
5. Every path from any node to any of its descendant NIL leaves has the **same number of Black nodes** (Black-height).

- **Height guarantee:** Maximum height ≤ 2 × log₂(n+1).
- **Black-height** (bh) of the tree — the uniform count of black nodes on any root-to-leaf path.
- Fixing violations after insert/delete requires: **recoloring** and/or **rotations** (left-rotate, right-rotate).

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Search | O(log n) | O(log n) | O(log n) |
| Insert | O(log n) | O(log n) | O(log n) |
| Delete | O(log n) | O(log n) | O(log n) |
| Rotation | O(1) | O(1) | O(1) |
| In-order Traversal | O(n) | O(n) | O(n) |

**Space Complexity:** `O(n)` + 1 bit per node for color

---

### 🔹 Verbal Explanation of Implementation Approach

- **Insert:**
  - Insert as in a standard BST. Color the new node **Red** (default, to avoid violating property 5).
  - If the parent is Black — no violation. Done.
  - If the parent is Red — violation of property 4. Fix based on the **uncle's color**:
    - **Uncle is Red:** Recolor parent and uncle to Black, grandparent to Red. Move the "problem" up to the grandparent. Repeat.
    - **Uncle is Black (or null):** Perform rotations (left or right rotation, possibly double) to restructure the subtree. Recolor nodes. Problem is resolved locally — does not propagate up.
  - At the end, always ensure the root is Black.

- **Delete:**
  - Structurally delete as in BST (replace with in-order successor if two children).
  - If the deleted (or replaced) node is Red — no black-height violation. Done.
  - If Black — **double-black problem** arises. Fix by:
    - Borrowing from a sibling (if sibling is black with at least one red child).
    - Recoloring sibling and propagating up (if sibling has two black children).
    - Rotating when sibling is Red.
  - This process terminates within O(log n) steps.

- **Rotations** (O(1) pointer reassignments):
  - **Left Rotation on X:** X's right child Y becomes the new subtree root. Y's left child becomes X's right child. X becomes Y's left child.
  - **Right Rotation on X:** Mirror of left rotation.

---

### 🔹 Variations / Modifications

- **Left-Leaning Red-Black Tree (LLRB)** — Simplified variant by Sedgewick; red links only go left, reducing implementation complexity.
- **2-3-4 Tree ↔ Red-Black Tree:** Direct isomorphism — every 2-3-4 tree can be represented as a Red-Black Tree.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| O(log n) guaranteed for all ops | Complex implementation (many rotation cases) |
| Faster insert/delete than AVL (fewer rotations) | Slightly worse search than AVL (less strict balance) |
| Widely used in standard libraries | Hard to implement correctly from scratch |

---

### 🔹 Interview Tips

- **Common Questions:** Mostly conceptual — properties of RB Tree, comparison with AVL, why it's preferred in practice.
- **Key Statement:** "Red-Black Trees offer a good balance between lookup and write performance. They guarantee O(log n) but with fewer rotations than AVL during insertions and deletions — this is why Java's `TreeMap` and Linux's CFS scheduler use them."
- **Tricky Points:** Memorize the 5 properties — interviewers test these directly.
- **Mistakes to Avoid:** Claiming AVL is better in all cases — it's better for read-heavy, RBT is better for write-heavy.

---

### 🔹 Real-World Use Cases

- **Java `TreeMap` / `TreeSet`:** Red-Black Tree backed sorted map/set.
- **C++ `std::map`, `std::set`:** Typically implemented as Red-Black Trees.
- **Linux CFS Scheduler:** Processes stored in a Red-Black Tree keyed by virtual runtime.
- **Nginx:** Uses Red-Black Trees for timer management.
- **Computational Geometry:** Used in sweep line algorithms.

---
---

## 13. 🔁 Splay Tree

### 🔹 Technical Definition

A **Splay Tree** is a self-adjusting BST where every access operation (search, insert, delete) moves the accessed node to the **root** via a sequence of tree rotations called **splaying**. It has no explicit balance invariant but achieves **amortized O(log n)** for all operations through its self-organizing property.

---

### 🔹 Intuition / Core Idea

- Think of a **self-organizing bookshelf** — the book you just read is placed back at the front. Frequently accessed items naturally migrate to the top.
- Splay trees exploit **temporal locality** — recently accessed nodes are near the root, making repeated accesses to the same elements very fast.
- No balance information stored per node — the tree self-organizes through access patterns.

---

### 🔹 Key Properties & Insights

- **No balance metadata** — no height, color, or rank stored. Simpler node structure.
- **Splaying** moves accessed node to root using combinations of three rotations:
  - **Zig:** Single rotation (accessed node is child of root).
  - **Zig-Zig:** Two rotations in same direction (accessed node and its parent are both left or both right children).
  - **Zig-Zag:** Two rotations in opposite directions.
- Amortized O(log n) — no single operation is guaranteed O(log n); worst case per operation is O(n), but averaged over sequences it is O(log n).
- **Working-set property** — if a set of `t` elements is accessed repeatedly, each access costs O(log t).

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average (Amortized) | Worst (Single Op) |
|---|---|---|---|
| Search | O(1) | O(log n) | O(n) |
| Insert | O(1) | O(log n) | O(n) |
| Delete | O(1) | O(log n) | O(n) |
| Splay | O(1) | O(log n) | O(n) |

**Space Complexity:** `O(n)` — simpler node structure (no balance fields)

---

### 🔹 Verbal Explanation of Implementation Approach

- **Splay(x):** The core operation — moves node `x` to the root.
  - While `x` is not the root:
    - **Zig case:** `x`'s parent `p` is the root. Rotate `x` over `p` (single rotation).
    - **Zig-Zig case:** `x` and `p` are both left children (or both right children). Rotate `p` over `p`'s parent first, then rotate `x` over `p`. (Double rotation — same direction.)
    - **Zig-Zag case:** `x` and `p` are in different directions. Rotate `x` over `p`, then rotate `x` over its new parent. (Double rotation — opposite directions.)
- **Search(k):** BST search. Splay the found (or last accessed) node to the root.
- **Insert(k):** BST insert. Splay the new node to the root.
- **Delete(k):** Splay `k` to the root. Now split the tree into left and right subtrees. Splay the maximum of the left subtree to the top of the left tree. Attach right subtree as its right child.

---

### 🔹 Variations / Modifications

- **Top-Down Splay Tree** — Splays while descending, rather than bottom-up. More cache-friendly.
- **Semi-Splay / Half-Splaying** — Moves node only halfway to root; reduces total work in some cases.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| Excellent cache behavior for repeated accesses | No worst-case per-operation guarantee |
| Simple node structure (no balance field) | Can degrade to O(n) on adversarial sequences |
| O(log n) amortized for all ops | Restructuring on every access — overhead for read-mostly |
| Split and Merge operations in O(log n) amortized | Less predictable latency than AVL/RBT |

---

### 🔹 Interview Tips

- **Common Questions:** Conceptual — "What is a Splay Tree?", "When would you use it over AVL or RBT?", explain splaying.
- **Key Statement:** "Splay trees are optimal for workloads with strong temporal locality — if the same few elements are accessed repeatedly, they stay at the root for O(1) access."
- **Tricky Points:**
  - Zig-Zig vs Zig-Zag rotation distinction — very commonly asked.
  - Why Zig-Zig (same-direction double rotation) is used instead of two single rotations — it provides better amortized balance.
- **Mistakes to Avoid:** Claiming O(log n) worst-case per operation — it is **amortized** only.

---

### 🔹 Real-World Use Cases

- **Windows NT Memory Management:** Virtual memory regions managed using splay trees.
- **GCC's `libstdc++`:** Used in some internal allocator structures.
- **Network Intrusion Detection:** Pattern matching systems leveraging temporal locality.
- **Cache-oblivious data structures:** Research applications exploiting access patterns.

---
---

## 14. ⚖️ AVL Tree

### 🔹 Technical Definition

An **AVL Tree** (Adelson-Velsky and Landis, 1962 — the first self-balancing BST) is a BST where for every node, the absolute difference between the heights of its left and right subtrees (**balance factor**) is at most 1: `|height(left) - height(right)| ≤ 1`. This strict balance is maintained after every insert and delete through rotations.

---

### 🔹 Intuition / Core Idea

- Think of an AVL tree as a **BST that constantly checks its balance** — after every modification, each affected node checks if it has become too lopsided. If the imbalance exceeds 1, it rotates to restore balance.
- AVL trees guarantee a height of at most `1.44 × log₂(n)` — significantly stricter than Red-Black Trees (2 log n).
- Ideal for **read-heavy** workloads where search dominates — the strict balance yields faster lookups.

---

### 🔹 Key Properties & Insights

- **Balance Factor** = `height(right subtree) - height(left subtree)` ∈ {-1, 0, +1} for every node.
- **Height** is `O(log n)` — specifically ≤ 1.44 log₂(n).
- **4 imbalance cases** to handle during insert/delete:
  1. Left-Left (LL) → Right Rotation
  2. Right-Right (RR) → Left Rotation
  3. Left-Right (LR) → Left Rotation on child, then Right Rotation on node
  4. Right-Left (RL) → Right Rotation on child, then Left Rotation on node
- Each node stores its **height** (or balance factor) as metadata.
- AVL trees perform **more rotations** during insert/delete than Red-Black Trees but offer **better search performance** (smaller height).

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Search | O(log n) | O(log n) | O(log n) |
| Insert | O(log n) | O(log n) | O(log n) |
| Delete | O(log n) | O(log n) | O(log n) |
| Rotation | O(1) | O(1) | O(1) |
| In-order Traversal | O(n) | O(n) | O(n) |

**Space Complexity:** `O(n)` + O(1) extra per node for height/balance factor

---

### 🔹 Verbal Explanation of Implementation Approach

- **Insert:**
  - Perform standard BST insert.
  - Walking back up (via recursion or parent pointers), **update the height** of each ancestor.
  - Check the **balance factor** at each ancestor.
  - If balance factor becomes +2 or -2, apply the appropriate rotation:
    - **LL Case (balance = -2, left child balance ≤ 0):** Single right rotation at current node.
    - **RR Case (balance = +2, right child balance ≥ 0):** Single left rotation at current node.
    - **LR Case (balance = -2, left child balance = +1):** Left rotate on left child first, then right rotate on current node.
    - **RL Case (balance = +2, right child balance = -1):** Right rotate on right child first, then left rotate on current node.
  - After a rotation, at most one rotation is needed per insert (the imbalance is fully fixed).

- **Delete:**
  - Standard BST delete (three cases).
  - Walk back up, update heights, check balance. Apply rotations as needed.
  - Unlike insert, delete may require **O(log n) rotations** propagating up the tree.

- **Rotation (Left Rotation on X):**
  - X's right child Y becomes the new root of this subtree.
  - Y's left subtree becomes X's right subtree.
  - X becomes Y's left child.
  - Update heights of X, then Y.

---

### 🔹 Variations / Modifications

- **AVL Tree with lazy deletion** — Mark nodes as deleted without restructuring; useful for concurrent access patterns.
- **Rank-balanced Trees (WAVL)** — Generalization with weaker balance guarantees but fewer rotations than AVL.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| Strictest balance among common BSTs — best search | More rotations during insert/delete vs Red-Black |
| O(log n) worst case — all operations | Slightly higher constant factors than Red-Black |
| Predictable, deterministic performance | More complex deletion logic |

---

### 🔹 Interview Tips

- **Common Questions:** Conceptual comparison with Red-Black Tree, balance factor explanation, identify which rotation is needed given a diagram.
- **Key Comparison:**

  | Property | AVL Tree | Red-Black Tree |
  |---|---|---|
  | Balance | Strict (|bf| ≤ 1) | Relaxed (2× height) |
  | Search | Faster | Slightly slower |
  | Insert/Delete | Slower (more rotations) | Faster (fewer rotations) |
  | Use Case | Read-heavy | Write-heavy |

- **Tricky Points:**
  - LR and RL cases involve double rotations — a common point of confusion.
  - Height update order in recursion matters — update child before parent.
- **Mistakes to Avoid:**
  - Saying "AVL is always better than RBT" — it depends on workload.
  - Forgetting to update heights after rotations.

---

### 🔹 Real-World Use Cases

- **Database Management Systems:** Some DBMS use AVL trees for in-memory indexes.
- **Real-time Systems:** Where predictable, bounded latency is critical.
- **Computational Geometry:** Efficient range queries with strict balance guarantees.
- **In-memory dictionaries** in applications requiring frequent lookups and rare writes.

---
---

## 15. 🌐 KD Tree (K-Dimensional Tree)

### 🔹 Technical Definition

A **KD Tree** (K-Dimensional Tree) is a binary tree that partitions a `k`-dimensional space by alternating splitting hyperplanes along each dimension, one per level. Each node represents a point in k-dimensional space and divides remaining points into two half-spaces based on comparison along the current dimension. It enables efficient **multidimensional range queries** and **nearest neighbor searches**.

---

### 🔹 Intuition / Core Idea

- Think of a **recursive binary partitioning of a map** — first split the entire map left/right (by x-coordinate), then split each half top/bottom (by y-coordinate), then by x again, and so on.
- For `k=2` (2D points), each level splits by x (even levels) or y (odd levels). This creates rectangular regions, and you only search regions that could contain the nearest neighbor.
- Used when: searching for nearest neighbors or points within a range in multi-dimensional space.

---

### 🔹 Key Properties & Insights

- **Dimension cycling:** At depth `d`, split on dimension `d mod k`.
- **Split value:** Typically the **median** along the current dimension (ensures balance); can also use the leftmost/rightmost value (simpler, but potentially unbalanced).
- **Balanced KD Tree height:** `O(log n)` with median splits.
- Performance **degrades in high dimensions** — "curse of dimensionality." For k >> log n, brute force may be comparable or faster.
- KD Trees are **static** in their most common form — bulk-loaded at construction. Dynamic insertion/deletion can unbalance them.
- **Backtracking** is key: during nearest neighbor search, you must backtrack and check the other half of a split if the splitting hyperplane is closer than the current best.

---

### 🔹 Operations & Time Complexity

| Operation | Best | Average | Worst |
|---|---|---|---|
| Build (balanced) | O(n log n) | O(n log n) | O(n log n) |
| Insert | O(log n) | O(log n) | O(n) |
| Search (exact) | O(log n) | O(log n) | O(n) |
| Nearest Neighbor Search | O(log n) | O(log n) | O(n) |
| Range Search (k=2) | O(√n + r) | O(√n + r) | O(n) |
| Delete | O(log n) | O(log n) | O(n) |

*`r` = number of points found in the range.*

**Space Complexity:** `O(n)`

---

### 🔹 Verbal Explanation of Implementation Approach

- **Build (median-based, balanced):**
  - Given a set of `n` points, select the splitting dimension (first dimension at root).
  - Find the **median** along this dimension. Place the median point at the root.
  - Recursively build the left subtree from points below the median, right subtree from points above.
  - Alternate dimension at each level: `dim = depth mod k`.
  - Height is O(log n) with median splitting.

- **Nearest Neighbor Search (NNS):**
  - Start at root. Descend the tree as you would in a BST — go to the half that contains the query point.
  - When you reach a leaf, that point is a candidate for nearest neighbor.
  - **Backtrack:** At each internal node, check if the splitting hyperplane is closer to the query than the current best. If it is, the other half of the tree could contain a closer point — explore it too.
  - Maintain and update `best_distance` as you explore.

- **Range Search:**
  - At each node, check if the splitting hyperplane intersects the query range.
  - If yes, explore both subtrees.
  - If no, only explore the relevant side.
  - Collect all points within the range at leaves.

---

### 🔹 Variations / Modifications

- **Ball Tree** — Encloses points in hyperspheres instead of hyperplanes; handles high dimensions better than KD Trees.
- **R-Tree** — Uses bounding rectangles; preferred for geographic data (PostGIS, spatial databases).
- **Approximate Nearest Neighbor (ANN)** — Sacrifices exact nearest neighbor for speed; algorithms like HNSW (Hierarchical Navigable Small World) used in vector databases.

---

### 🔹 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| Efficient NNS for low dimensions (k ≤ ~20) | Degrades in high dimensions (curse of dimensionality) |
| Range queries in O(√n + r) for 2D | Complex backtracking logic |
| O(n log n) build time | Dynamic insertions can unbalance the tree |
| No index overhead beyond the tree itself | Poor performance when k is large relative to n |

---

### 🔹 Interview Tips

- **Common Questions:** Conceptual — "How would you find the k-nearest neighbors?", "What data structure would you use for a 2D geographic search?", Design a system for nearest restaurant lookup.
- **Key Statement:** "KD Trees are the go-to for exact nearest neighbor search in low to moderate dimensions. For high-dimensional similarity search (embeddings, vectors), approximate methods like HNSW or Annoy are more practical."
- **Tricky Points:**
  - The backtracking step in NNS — most candidates forget about it.
  - Why median splitting gives O(log n) height while arbitrary splitting can degrade.
  - "Curse of dimensionality" — for k > ~20, the exponential growth of volume means nearly all points are equidistant, making KD tree pruning ineffective.
- **Mistakes to Avoid:**
  - Claiming O(log n) guaranteed for NNS — it's average case; worst is O(n).
  - Forgetting to check the "other side" of a split during NNS backtracking.

---

### 🔹 Real-World Use Cases

- **Machine Learning:** k-NN classification and regression — `sklearn` KNeighborsClassifier uses KD Trees.
- **Robotics & Autonomous Systems:** Point cloud processing, LiDAR nearest neighbor matching.
- **Computer Graphics:** Ray tracing, collision detection, spatial indexing in game engines.
- **Geographic Information Systems (GIS):** Find all points within a bounding box.
- **Vector Databases (approximate):** Conceptual ancestor of systems like Pinecone, Weaviate, FAISS for embedding search.

---
---

## 📊 Final Comparison Table

> All complexities refer to **worst case** unless marked †(average case)

| Data Structure | Access | Search | Insert | Delete | Space | Best Use Case |
|---|---|---|---|---|---|---|
| **Array** | O(1) | O(n) | O(n) | O(n) | O(n) | Random access, fixed-size collections, cache-sensitive ops |
| **Stack** | O(n) | O(n) | O(1) | O(1) | O(n) | LIFO operations, recursion, undo/redo, DFS |
| **Queue** | O(n) | O(n) | O(1) | O(1) | O(n) | FIFO operations, BFS, task scheduling |
| **Singly Linked List** | O(n) | O(n) | O(1) head | O(1) head | O(n) | Dynamic-size list, frequent head insertions |
| **Doubly Linked List** | O(n) | O(n) | O(1) ends | O(1) †given ref | O(n) | LRU Cache, bidirectional traversal |
| **Circular Linked List** | O(n) | O(n) | O(1) † | O(1) head | O(n) | Round-robin, cyclic processing |
| **Skip List** | O(n) | O(log n) † | O(log n) † | O(log n) † | O(n) | Sorted dynamic set, concurrent key-value stores |
| **Hash Table** | O(n) | O(1) † | O(1) † | O(1) † | O(n) | Fast key-value lookup, caching, deduplication |
| **Binary Search Tree** | O(n) | O(n) | O(n) | O(n) | O(n) | Sorted data, predecessor/successor, range queries |
| **Cartesian Tree** | O(n) | O(n) | O(n) | O(n) | O(n) | Range min/max queries, Treap foundation |
| **B-Tree** | O(log n) | O(log n) | O(log n) | O(log n) | O(n) | Disk-based storage, database indexes |
| **Red-Black Tree** | O(log n) | O(log n) | O(log n) | O(log n) | O(n) | General sorted map/set, write-heavy workloads |
| **Splay Tree** | O(n) | O(n) amort. | O(n) amort. | O(n) amort. | O(n) | Temporal locality workloads, caches |
| **AVL Tree** | O(log n) | O(log n) | O(log n) | O(log n) | O(n) | Read-heavy sorted data, strict balance needed |
| **KD Tree** | O(n) | O(n) | O(log n) † | O(log n) † | O(n) | Multidimensional nearest-neighbor and range search |

> **†** denotes **average case** (not worst case)  
> For **balanced BSTs** (AVL, RBT, B-Tree): all operations are **O(log n) worst case**

---

### 🔹 Quick Selection Guide

```
Need O(1) lookup by key?                    → Hash Table
Need sorted order + range queries?          → AVL Tree / Red-Black Tree
Disk-based sorted index?                    → B+ Tree
LIFO access pattern?                        → Stack
FIFO access pattern?                        → Queue
Frequent head insertions, dynamic size?     → Singly Linked List
O(1) delete by reference + ordered?        → Doubly Linked List
Cyclic / round-robin processing?            → Circular Linked List
Concurrent sorted map?                      → Skip List
Spatial / nearest-neighbor queries?         → KD Tree
Temporal locality, self-tuning?             → Splay Tree
Array-based range minimum query?            → Cartesian Tree
```

---

## 📎 Quick Reference Cheat Sheet

### Rotation Types (for Balanced Trees)

| Rotation | When Applied | Effect |
|---|---|---|
| **Left Rotation** | Right-heavy subtree (RR case) | Brings right child up, current node becomes left child |
| **Right Rotation** | Left-heavy subtree (LL case) | Brings left child up, current node becomes right child |
| **Left-Right (Double)** | Left child is right-heavy (LR case) | Left rotate on child, then right rotate on current |
| **Right-Left (Double)** | Right child is left-heavy (RL case) | Right rotate on child, then left rotate on current |

---

### Complexity Summary (One-Liner Memory Aid)

```
Array:        O(1) access | O(n) insert/delete (middle)
Stack/Queue:  O(1) push/pop/enqueue/dequeue
Linked Lists: O(1) head ops | O(n) access by index
Hash Table:   O(1) avg for all | O(n) worst
BST:          O(log n) avg | O(n) worst (unbalanced)
AVL/RBT:      O(log n) ALL cases (guaranteed)
B-Tree:       O(log n) ALL cases (disk-optimized)
Splay:        O(log n) AMORTIZED only
Skip List:    O(log n) EXPECTED
KD Tree:      O(log n) avg for NNS | O(n) worst
```

---

*📝 Study Tip: For each data structure, practice explaining it out loud in 60 seconds covering: definition, core property, 2 key operations with complexity, and one real-world use case. This mirrors the pace of a real technical screen.*

---

> **Last Updated:** 2025 | Designed for technical interview preparation  
> **Covers:** 15 core data structures + complexity theory fundamentals  
> **Target:** Fresher to mid-level software engineering interviews
