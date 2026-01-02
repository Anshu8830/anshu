# Complete DSA Guide: From Basics to Advanced (Python)

## Table of Contents
1. [Introduction](#introduction)
2. [Python Fundamentals for DSA](#python-fundamentals-for-dsa)
3. [Time & Space Complexity](#time--space-complexity)
4. [Arrays & Strings](#arrays--strings)
5. [Two Pointers](#two-pointers)
6. [Sliding Window](#sliding-window)
7. [Hash Maps & Sets](#hash-maps--sets)
8. [Linked Lists](#linked-lists)
9. [Stacks & Queues](#stacks--queues)
10. [Trees](#trees)
11. [Binary Search](#binary-search)
12. [Graphs](#graphs)
13. [Dynamic Programming](#dynamic-programming)
14. [Backtracking](#backtracking)
15. [Greedy Algorithms](#greedy-algorithms)
16. [Trie (Prefix Tree)](#trie-prefix-tree)
17. [Union-Find (Disjoint Set)](#union-find-disjoint-set)
18. [Segment Trees & Fenwick Trees](#segment-trees--fenwick-trees)
19. [Advanced Topics](#advanced-topics)
20. [Pattern Recognition Guide](#pattern-recognition-guide)
21. [Interview Preparation Strategy](#interview-preparation-strategy)
22. [Resources](#resources)

---

## Introduction

### Learning Approach
1. **Pattern-Based Learning**: Understand problem patterns, not just solutions
2. **Progressive Difficulty**: Start with basics, gradually move to advanced
3. **Practice**: Solve 2-3 problems per topic at each difficulty level
4. **Time Complexity**: Always analyze time and space complexity
5. **Code Quality**: Write clean, readable, optimized code

### Python vs C++ for DSA
- **Python Advantages**: 
  - Cleaner syntax, faster to write
  - Built-in data structures (dict, set, list)
  - Better for interviews (focus on logic, not syntax)
- **C++ Advantages**: 
  - Faster execution
  - More control over memory
- **For Interviews**: Python is preferred (faster coding, easier to explain)

---

## Python Fundamentals for DSA

### Essential Data Structures

```python
# Lists (Dynamic Arrays)
arr = [1, 2, 3]
arr.append(4)        # O(1)
arr.pop()            # O(1)
arr.insert(0, 0)     # O(n)
arr[0]               # O(1)

# Dictionaries (Hash Maps)
d = {}
d['key'] = 'value'   # O(1)
d.get('key')         # O(1)
'key' in d           # O(1)

# Sets
s = set()
s.add(1)             # O(1)
1 in s               # O(1)
s.remove(1)          # O(1)

# Tuples (Immutable)
t = (1, 2, 3)        # O(1) access

# Deque (Double-ended queue)
from collections import deque
dq = deque()
dq.append(1)         # O(1)
dq.popleft()         # O(1)
dq.appendleft(0)     # O(1)

# Heap (Priority Queue)
import heapq
heap = []
heapq.heappush(heap, 3)  # O(log n)
heapq.heappop(heap)      # O(log n)
```

### Useful Python Tricks

```python
# List comprehensions
squares = [x**2 for x in range(10)]

# Dictionary comprehensions
square_dict = {x: x**2 for x in range(10)}

# Enumerate
for i, val in enumerate(arr):
    print(i, val)

# Zip
for a, b in zip(arr1, arr2):
    print(a, b)

# Counter
from collections import Counter
count = Counter(arr)

# Defaultdict
from collections import defaultdict
dd = defaultdict(int)
dd['key'] += 1  # No KeyError

# Sorting
arr.sort()                    # In-place
sorted_arr = sorted(arr)      # New list
arr.sort(key=lambda x: x[1])  # Custom key
```

---

## Time & Space Complexity

### Big O Notation

| Complexity | Name | Example |
|------------|------|---------|
| O(1) | Constant | Array access, hash map lookup |
| O(log n) | Logarithmic | Binary search, heap operations |
| O(n) | Linear | Single loop through array |
| O(n log n) | Linearithmic | Sorting, divide & conquer |
| O(n²) | Quadratic | Nested loops |
| O(2ⁿ) | Exponential | Recursive Fibonacci |
| O(n!) | Factorial | Permutations |

### Space Complexity
- **Auxiliary Space**: Extra space used by algorithm
- **Total Space**: Input space + auxiliary space
- **In-place**: O(1) extra space

### Common Patterns Complexity

| Pattern | Time | Space |
|---------|------|-------|
| Two Pointers | O(n) | O(1) |
| Sliding Window | O(n) | O(k) |
| Hash Map | O(n) | O(n) |
| Binary Search | O(log n) | O(1) |
| DFS/BFS | O(V + E) | O(V) |
| DP | O(n) to O(n²) | O(n) to O(n²) |

---

## Arrays & Strings

### Basic Operations

**Pattern Recognition**:
- Array manipulation
- Index-based problems
- Subarray problems

#### Basic Level

1. **Two Sum** - [LeetCode 1](https://leetcode.com/problems/two-sum/)
   - Pattern: Hash map for O(n) solution
   - Time: O(n), Space: O(n)

2. **Best Time to Buy and Sell Stock** - [LeetCode 121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
   - Pattern: Track minimum price
   - Time: O(n), Space: O(1)

3. **Contains Duplicate** - [LeetCode 217](https://leetcode.com/problems/contains-duplicate/)
   - Pattern: Set for O(1) lookup
   - Time: O(n), Space: O(n)

4. **Maximum Subarray** - [LeetCode 53](https://leetcode.com/problems/maximum-subarray/)
   - Pattern: Kadane's algorithm
   - Time: O(n), Space: O(1)

5. **Product of Array Except Self** - [LeetCode 238](https://leetcode.com/problems/product-of-array-except-self/)
   - Pattern: Prefix and suffix products
   - Time: O(n), Space: O(1) excluding output

#### Medium Level

6. **3Sum** - [LeetCode 15](https://leetcode.com/problems/3sum/)
   - Pattern: Two pointers after sorting
   - Time: O(n²), Space: O(1)

7. **Container With Most Water** - [LeetCode 11](https://leetcode.com/problems/container-with-most-water/)
   - Pattern: Two pointers
   - Time: O(n), Space: O(1)

8. **Longest Consecutive Sequence** - [LeetCode 128](https://leetcode.com/problems/longest-consecutive-sequence/)
   - Pattern: Hash set + sequence detection
   - Time: O(n), Space: O(n)

9. **Group Anagrams** - [LeetCode 49](https://leetcode.com/problems/group-anagrams/)
   - Pattern: Hash map with sorted string as key
   - Time: O(n*k log k), Space: O(n*k)

10. **Top K Frequent Elements** - [LeetCode 347](https://leetcode.com/problems/top-k-frequent-elements/)
    - Pattern: Hash map + heap
    - Time: O(n log k), Space: O(n)

#### Hard Level

11. **Trapping Rain Water** - [LeetCode 42](https://leetcode.com/problems/trapping-rain-water/)
    - Pattern: Two pointers or stack
    - Time: O(n), Space: O(1) or O(n)

12. **Merge Intervals** - [LeetCode 56](https://leetcode.com/problems/merge-intervals/)
    - Pattern: Sort + merge overlapping
    - Time: O(n log n), Space: O(n)

13. **Find Median from Data Stream** - [LeetCode 295](https://leetcode.com/problems/find-median-from-data-stream/)
    - Pattern: Two heaps (min + max)
    - Time: O(log n) insert, O(1) find, Space: O(n)

14. **Sliding Window Maximum** - [LeetCode 239](https://leetcode.com/problems/sliding-window-maximum/)
    - Pattern: Monotonic deque
    - Time: O(n), Space: O(k)

15. **First Missing Positive** - [LeetCode 41](https://leetcode.com/problems/first-missing-positive/)
    - Pattern: Array as hash map (cyclic sort)
    - Time: O(n), Space: O(1)

#### Very Hard Level

16. **Candy** - [LeetCode 135](https://leetcode.com/problems/candy/)
    - Pattern: Greedy with two passes
    - Time: O(n), Space: O(n)

17. **Trapping Rain Water II** - [LeetCode 407](https://leetcode.com/problems/trapping-rain-water-ii/)
    - Pattern: Priority queue + BFS
    - Time: O(m*n*log(m*n)), Space: O(m*n)

18. **Serialize and Deserialize Binary Tree** - [LeetCode 297](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
    - Pattern: Preorder traversal
    - Time: O(n), Space: O(n)

---

## Two Pointers

### Pattern Recognition
- Sorted arrays
- Palindrome problems
- Pair/triplet sum problems
- Removing duplicates

#### Basic Level

1. **Valid Palindrome** - [LeetCode 125](https://leetcode.com/problems/valid-palindrome/)
   - Time: O(n), Space: O(1)

2. **Squares of a Sorted Array** - [LeetCode 977](https://leetcode.com/problems/squares-of-a-sorted-array/)
   - Time: O(n), Space: O(1)

3. **Reverse String** - [LeetCode 344](https://leetcode.com/problems/reverse-string/)
   - Time: O(n), Space: O(1)

#### Medium Level

4. **3Sum Closest** - [LeetCode 16](https://leetcode.com/problems/3sum-closest/)
   - Time: O(n²), Space: O(1)

5. **4Sum** - [LeetCode 18](https://leetcode.com/problems/4sum/)
   - Time: O(n³), Space: O(1)

6. **Partition Labels** - [LeetCode 763](https://leetcode.com/problems/partition-labels/)
   - Time: O(n), Space: O(1)

#### Hard Level

7. **Trapping Rain Water** - [LeetCode 42](https://leetcode.com/problems/trapping-rain-water/)
   - Time: O(n), Space: O(1)

8. **Boats to Save People** - [LeetCode 881](https://leetcode.com/problems/boats-to-save-people/)
   - Time: O(n log n), Space: O(1)

---

## Sliding Window

### Pattern Recognition
- Subarray/substring problems
- Fixed or variable window size
- "Longest/shortest substring with K distinct"
- "Maximum/minimum in window"

#### Basic Level

1. **Maximum Average Subarray I** - [LeetCode 643](https://leetcode.com/problems/maximum-average-subarray-i/)
   - Pattern: Fixed window
   - Time: O(n), Space: O(1)

2. **Minimum Size Subarray Sum** - [LeetCode 209](https://leetcode.com/problems/minimum-size-subarray-sum/)
   - Pattern: Variable window
   - Time: O(n), Space: O(1)

#### Medium Level

3. **Longest Substring Without Repeating Characters** - [LeetCode 3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
   - Pattern: Hash map + sliding window
   - Time: O(n), Space: O(min(n, m))

4. **Longest Repeating Character Replacement** - [LeetCode 424](https://leetcode.com/problems/longest-repeating-character-replacement/)
   - Pattern: Sliding window with frequency map
   - Time: O(n), Space: O(1)

5. **Permutation in String** - [LeetCode 567](https://leetcode.com/problems/permutation-in-string/)
   - Pattern: Fixed window + frequency matching
   - Time: O(n), Space: O(1)

6. **Fruit Into Baskets** - [LeetCode 904](https://leetcode.com/problems/fruit-into-baskets/)
   - Pattern: Longest substring with at most K distinct
   - Time: O(n), Space: O(1)

#### Hard Level

7. **Sliding Window Maximum** - [LeetCode 239](https://leetcode.com/problems/sliding-window-maximum/)
   - Pattern: Monotonic deque
   - Time: O(n), Space: O(k)

8. **Minimum Window Substring** - [LeetCode 76](https://leetcode.com/problems/minimum-window-substring/)
   - Pattern: Variable window + frequency map
   - Time: O(n + m), Space: O(m)

9. **Substring with Concatenation of All Words** - [LeetCode 30](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)
   - Pattern: Sliding window + hash map
   - Time: O(n * m * k), Space: O(m * k)

---

## Hash Maps & Sets

### Pattern Recognition
- Frequency counting
- Lookup optimization
- Duplicate detection
- Grouping problems

#### Basic Level

1. **Two Sum** - [LeetCode 1](https://leetcode.com/problems/two-sum/)
   - Time: O(n), Space: O(n)

2. **Contains Duplicate** - [LeetCode 217](https://leetcode.com/problems/contains-duplicate/)
   - Time: O(n), Space: O(n)

3. **Valid Anagram** - [LeetCode 242](https://leetcode.com/problems/valid-anagram/)
   - Time: O(n), Space: O(1) if fixed alphabet

#### Medium Level

4. **Group Anagrams** - [LeetCode 49](https://leetcode.com/problems/group-anagrams/)
   - Time: O(n*k log k), Space: O(n*k)

5. **Longest Consecutive Sequence** - [LeetCode 128](https://leetcode.com/problems/longest-consecutive-sequence/)
   - Time: O(n), Space: O(n)

6. **Copy List with Random Pointer** - [LeetCode 138](https://leetcode.com/problems/copy-list-with-random-pointer/)
   - Time: O(n), Space: O(n)

7. **Design HashMap** - [LeetCode 706](https://leetcode.com/problems/design-hashmap/)
   - Time: O(1) average, Space: O(n)

#### Hard Level

8. **LRU Cache** - [LeetCode 146](https://leetcode.com/problems/lru-cache/)
   - Pattern: Hash map + doubly linked list
   - Time: O(1), Space: O(capacity)

9. **LFU Cache** - [LeetCode 460](https://leetcode.com/problems/lfu-cache/)
   - Pattern: Hash maps + doubly linked lists
   - Time: O(1), Space: O(capacity)

---

## Linked Lists

### Pattern Recognition
- Pointer manipulation
- Cycle detection
- Reversal problems
- Merge problems

#### Basic Level

1. **Reverse Linked List** - [LeetCode 206](https://leetcode.com/problems/reverse-linked-list/)
   - Pattern: Iterative or recursive
   - Time: O(n), Space: O(1) iterative, O(n) recursive

2. **Merge Two Sorted Lists** - [LeetCode 21](https://leetcode.com/problems/merge-two-sorted-lists/)
   - Time: O(n + m), Space: O(1)

3. **Linked List Cycle** - [LeetCode 141](https://leetcode.com/problems/linked-list-cycle/)
   - Pattern: Floyd's cycle detection
   - Time: O(n), Space: O(1)

#### Medium Level

4. **Add Two Numbers** - [LeetCode 2](https://leetcode.com/problems/add-two-numbers/)
   - Time: O(max(n, m)), Space: O(1)

5. **Remove Nth Node From End** - [LeetCode 19](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
   - Pattern: Two pointers
   - Time: O(n), Space: O(1)

6. **Swap Nodes in Pairs** - [LeetCode 24](https://leetcode.com/problems/swap-nodes-in-pairs/)
   - Time: O(n), Space: O(1)

7. **Rotate List** - [LeetCode 61](https://leetcode.com/problems/rotate-list/)
   - Time: O(n), Space: O(1)

#### Hard Level

8. **Merge k Sorted Lists** - [LeetCode 23](https://leetcode.com/problems/merge-k-sorted-lists/)
   - Pattern: Divide & conquer or heap
   - Time: O(n log k), Space: O(1) or O(k)

9. **Reverse Nodes in k-Group** - [LeetCode 25](https://leetcode.com/problems/reverse-nodes-in-k-group/)
   - Pattern: Recursive reversal
   - Time: O(n), Space: O(n/k)

10. **Copy List with Random Pointer** - [LeetCode 138](https://leetcode.com/problems/copy-list-with-random-pointer/)
    - Pattern: Hash map or interleaving
    - Time: O(n), Space: O(n) or O(1)

---

## Stacks & Queues

### Pattern Recognition
- LIFO/FIFO operations
- Parentheses matching
- Monotonic stack
- Next greater/smaller element

#### Basic Level

1. **Valid Parentheses** - [LeetCode 20](https://leetcode.com/problems/valid-parentheses/)
   - Pattern: Stack for matching
   - Time: O(n), Space: O(n)

2. **Implement Queue using Stacks** - [LeetCode 232](https://leetcode.com/problems/implement-queue-using-stacks/)
   - Time: O(1) amortized, Space: O(n)

3. **Implement Stack using Queues** - [LeetCode 225](https://leetcode.com/problems/implement-stack-using-queues/)
   - Time: O(n) push, O(1) pop, Space: O(n)

#### Medium Level

4. **Daily Temperatures** - [LeetCode 739](https://leetcode.com/problems/daily-temperatures/)
   - Pattern: Monotonic stack
   - Time: O(n), Space: O(n)

5. **Next Greater Element I** - [LeetCode 496](https://leetcode.com/problems/next-greater-element-i/)
   - Pattern: Monotonic stack
   - Time: O(n + m), Space: O(n)

6. **Asteroid Collision** - [LeetCode 735](https://leetcode.com/problems/asteroid-collision/)
   - Pattern: Stack simulation
   - Time: O(n), Space: O(n)

7. **Decode String** - [LeetCode 394](https://leetcode.com/problems/decode-string/)
   - Pattern: Stack for nested structures
   - Time: O(n), Space: O(n)

#### Hard Level

8. **Largest Rectangle in Histogram** - [LeetCode 84](https://leetcode.com/problems/largest-rectangle-in-histogram/)
   - Pattern: Monotonic stack
   - Time: O(n), Space: O(n)

9. **Maximal Rectangle** - [LeetCode 85](https://leetcode.com/problems/maximal-rectangle/)
   - Pattern: Stack + DP
   - Time: O(m*n), Space: O(n)

10. **Basic Calculator** - [LeetCode 224](https://leetcode.com/problems/basic-calculator/)
    - Pattern: Stack for expression evaluation
    - Time: O(n), Space: O(n)

---

## Trees

### Pattern Recognition
- Hierarchical data
- Traversal problems (DFS/BFS)
- Path problems
- Tree construction

### Binary Tree Traversals

```python
# Preorder: Root -> Left -> Right
def preorder(root):
    if not root:
        return
    result.append(root.val)
    preorder(root.left)
    preorder(root.right)

# Inorder: Left -> Root -> Right
def inorder(root):
    if not root:
        return
    inorder(root.left)
    result.append(root.val)
    inorder(root.right)

# Postorder: Left -> Right -> Root
def postorder(root):
    if not root:
        return
    postorder(root.left)
    postorder(root.right)
    result.append(root.val)

# Level Order (BFS)
from collections import deque
def levelOrder(root):
    if not root:
        return []
    queue = deque([root])
    result = []
    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)
    return result
```

#### Basic Level

1. **Maximum Depth of Binary Tree** - [LeetCode 104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
   - Time: O(n), Space: O(h)

2. **Same Tree** - [LeetCode 100](https://leetcode.com/problems/same-tree/)
   - Time: O(n), Space: O(h)

3. **Invert Binary Tree** - [LeetCode 226](https://leetcode.com/problems/invert-binary-tree/)
   - Time: O(n), Space: O(h)

4. **Symmetric Tree** - [LeetCode 101](https://leetcode.com/problems/symmetric-tree/)
   - Time: O(n), Space: O(h)

#### Medium Level

5. **Binary Tree Level Order Traversal** - [LeetCode 102](https://leetcode.com/problems/binary-tree-level-order-traversal/)
   - Time: O(n), Space: O(n)

6. **Construct Binary Tree from Preorder and Inorder** - [LeetCode 105](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
   - Time: O(n), Space: O(n)

7. **Validate Binary Search Tree** - [LeetCode 98](https://leetcode.com/problems/validate-binary-search-tree/)
   - Pattern: Inorder traversal or bounds checking
   - Time: O(n), Space: O(h)

8. **Kth Smallest Element in BST** - [LeetCode 230](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
   - Pattern: Inorder traversal
   - Time: O(h + k), Space: O(h)

9. **Lowest Common Ancestor** - [LeetCode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
   - Pattern: DFS with backtracking
   - Time: O(n), Space: O(h)

10. **Path Sum II** - [LeetCode 113](https://leetcode.com/problems/path-sum-ii/)
    - Pattern: DFS + backtracking
    - Time: O(n), Space: O(h)

#### Hard Level

11. **Binary Tree Maximum Path Sum** - [LeetCode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
    - Pattern: DFS with path calculation
    - Time: O(n), Space: O(h)

12. **Serialize and Deserialize Binary Tree** - [LeetCode 297](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
    - Pattern: Preorder traversal
    - Time: O(n), Space: O(n)

13. **Binary Tree Postorder Traversal** - [LeetCode 145](https://leetcode.com/problems/binary-tree-postorder-traversal/)
    - Time: O(n), Space: O(h)

14. **Count Complete Tree Nodes** - [LeetCode 222](https://leetcode.com/problems/count-complete-tree-nodes/)
    - Pattern: Binary search on tree
    - Time: O(log² n), Space: O(1)

---

## Binary Search

### Pattern Recognition
- Sorted arrays
- Search in rotated arrays
- Finding boundaries
- "Find minimum/maximum satisfying condition"

### Template

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

#### Basic Level

1. **Binary Search** - [LeetCode 704](https://leetcode.com/problems/binary-search/)
   - Time: O(log n), Space: O(1)

2. **Search Insert Position** - [LeetCode 35](https://leetcode.com/problems/search-insert-position/)
   - Time: O(log n), Space: O(1)

3. **First Bad Version** - [LeetCode 278](https://leetcode.com/problems/first-bad-version/)
   - Pattern: Find first occurrence
   - Time: O(log n), Space: O(1)

#### Medium Level

4. **Search in Rotated Sorted Array** - [LeetCode 33](https://leetcode.com/problems/search-in-rotated-sorted-array/)
   - Pattern: Modified binary search
   - Time: O(log n), Space: O(1)

5. **Find First and Last Position** - [LeetCode 34](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
   - Pattern: Two binary searches
   - Time: O(log n), Space: O(1)

6. **Search a 2D Matrix** - [LeetCode 74](https://leetcode.com/problems/search-a-2d-matrix/)
   - Pattern: Treat as 1D array
   - Time: O(log(m*n)), Space: O(1)

7. **Find Peak Element** - [LeetCode 162](https://leetcode.com/problems/find-peak-element/)
   - Pattern: Binary search on condition
   - Time: O(log n), Space: O(1)

#### Hard Level

8. **Median of Two Sorted Arrays** - [LeetCode 4](https://leetcode.com/problems/median-of-two-sorted-arrays/)
   - Pattern: Binary search on partition
   - Time: O(log(min(m, n))), Space: O(1)

9. **Split Array Largest Sum** - [LeetCode 410](https://leetcode.com/problems/split-array-largest-sum/)
   - Pattern: Binary search on answer
   - Time: O(n * log(sum)), Space: O(1)

10. **Kth Smallest Element in Sorted Matrix** - [LeetCode 378](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)
    - Pattern: Binary search on value
    - Time: O(k * log(max - min)), Space: O(1)

---

## Graphs

### Pattern Recognition
- Network problems
- Path finding
- Cycle detection
- Connected components
- Shortest path

### Graph Representations

```python
# Adjacency List
graph = {
    0: [1, 2],
    1: [0, 3],
    2: [0, 3],
    3: [1, 2]
}

# Adjacency Matrix
graph = [
    [0, 1, 1, 0],
    [1, 0, 0, 1],
    [1, 0, 0, 1],
    [0, 1, 1, 0]
]
```

### DFS Template

```python
def dfs(graph, node, visited):
    visited.add(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

### BFS Template

```python
from collections import deque

def bfs(graph, start):
    queue = deque([start])
    visited = {start}
    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

#### Basic Level

1. **Number of Islands** - [LeetCode 200](https://leetcode.com/problems/number-of-islands/)
   - Pattern: DFS/BFS on grid
   - Time: O(m*n), Space: O(m*n)

2. **Clone Graph** - [LeetCode 133](https://leetcode.com/problems/clone-graph/)
   - Pattern: DFS/BFS with hash map
   - Time: O(V + E), Space: O(V)

3. **Course Schedule** - [LeetCode 207](https://leetcode.com/problems/course-schedule/)
   - Pattern: Cycle detection (DFS)
   - Time: O(V + E), Space: O(V + E)

#### Medium Level

4. **Course Schedule II** - [LeetCode 210](https://leetcode.com/problems/course-schedule-ii/)
   - Pattern: Topological sort
   - Time: O(V + E), Space: O(V + E)

5. **Word Ladder** - [LeetCode 127](https://leetcode.com/problems/word-ladder/)
   - Pattern: BFS shortest path
   - Time: O(M * N), Space: O(M * N)

6. **Pacific Atlantic Water Flow** - [LeetCode 417](https://leetcode.com/problems/pacific-atlantic-water-flow/)
   - Pattern: Multi-source BFS/DFS
   - Time: O(m*n), Space: O(m*n)

7. **Surrounded Regions** - [LeetCode 130](https://leetcode.com/problems/surrounded-regions/)
   - Pattern: DFS from boundaries
   - Time: O(m*n), Space: O(m*n)

8. **Rotting Oranges** - [LeetCode 994](https://leetcode.com/problems/rotting-oranges/)
   - Pattern: Multi-source BFS
   - Time: O(m*n), Space: O(m*n)

#### Hard Level

9. **Word Ladder II** - [LeetCode 126](https://leetcode.com/problems/word-ladder-ii/)
   - Pattern: BFS + backtracking
   - Time: O(N * M²), Space: O(N * M)

10. **Alien Dictionary** - [LeetCode 269](https://leetcode.com/problems/alien-dictionary/)
    - Pattern: Topological sort
    - Time: O(C), Space: O(1) or O(U + min(U², N))

11. **Cheapest Flights Within K Stops** - [LeetCode 787](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
    - Pattern: BFS with cost tracking
    - Time: O(E * K), Space: O(V)

12. **Network Delay Time** - [LeetCode 743](https://leetcode.com/problems/network-delay-time/)
    - Pattern: Dijkstra's algorithm
    - Time: O(E log V), Space: O(V + E)

---

## Dynamic Programming

### Pattern Recognition
- Optimization problems
- Overlapping subproblems
- Optimal substructure
- "Count ways", "minimum/maximum"

### DP Patterns

1. **1D DP**: Fibonacci, climbing stairs
2. **2D DP**: Grid paths, LCS, edit distance
3. **Knapsack**: 0/1, unbounded, subset sum
4. **Interval DP**: Matrix chain, palindrome partitioning
5. **State Machine**: Stock problems with states

### Framework

```python
# 1. Define state
# 2. Define recurrence relation
# 3. Base cases
# 4. Order of computation
# 5. Return answer

# Example: Fibonacci
def fib(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```

#### Basic Level

1. **Climbing Stairs** - [LeetCode 70](https://leetcode.com/problems/climbing-stairs/)
   - Pattern: 1D DP
   - Time: O(n), Space: O(1)

2. **House Robber** - [LeetCode 198](https://leetcode.com/problems/house-robber/)
   - Pattern: 1D DP with choice
   - Time: O(n), Space: O(1)

3. **Coin Change** - [LeetCode 322](https://leetcode.com/problems/coin-change/)
   - Pattern: Unbounded knapsack
   - Time: O(amount * coins), Space: O(amount)

4. **Longest Increasing Subsequence** - [LeetCode 300](https://leetcode.com/problems/longest-increasing-subsequence/)
   - Pattern: 1D DP or binary search
   - Time: O(n²) or O(n log n), Space: O(n)

#### Medium Level

5. **Unique Paths** - [LeetCode 62](https://leetcode.com/problems/unique-paths/)
   - Pattern: 2D DP
   - Time: O(m*n), Space: O(n)

6. **Longest Common Subsequence** - [LeetCode 1143](https://leetcode.com/problems/longest-common-subsequence/)
   - Pattern: 2D DP
   - Time: O(m*n), Space: O(min(m, n))

7. **Edit Distance** - [LeetCode 72](https://leetcode.com/problems/edit-distance/)
   - Pattern: 2D DP
   - Time: O(m*n), Space: O(min(m, n))

8. **Partition Equal Subset Sum** - [LeetCode 416](https://leetcode.com/problems/partition-equal-subset-sum/)
   - Pattern: 0/1 Knapsack
   - Time: O(n * sum), Space: O(sum)

9. **Word Break** - [LeetCode 139](https://leetcode.com/problems/word-break/)
   - Pattern: 1D DP
   - Time: O(n²), Space: O(n)

10. **Decode Ways** - [LeetCode 91](https://leetcode.com/problems/decode-ways/)
    - Pattern: 1D DP with conditions
    - Time: O(n), Space: O(1)

#### Hard Level

11. **Best Time to Buy and Sell Stock IV** - [LeetCode 188](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)
    - Pattern: State machine DP
    - Time: O(n*k), Space: O(k)

12. **Regular Expression Matching** - [LeetCode 10](https://leetcode.com/problems/regular-expression-matching/)
    - Pattern: 2D DP
    - Time: O(m*n), Space: O(m*n)

13. **Wildcard Matching** - [LeetCode 44](https://leetcode.com/problems/wildcard-matching/)
    - Pattern: 2D DP
    - Time: O(m*n), Space: O(m*n)

14. **Burst Balloons** - [LeetCode 312](https://leetcode.com/problems/burst-balloons/)
    - Pattern: Interval DP
    - Time: O(n³), Space: O(n²)

15. **Palindrome Partitioning II** - [LeetCode 132](https://leetcode.com/problems/palindrome-partitioning-ii/)
    - Pattern: 1D DP + palindrome check
    - Time: O(n²), Space: O(n²)

16. **Longest Valid Parentheses** - [LeetCode 32](https://leetcode.com/problems/longest-valid-parentheses/)
    - Pattern: 1D DP or stack
    - Time: O(n), Space: O(n)

---

## Backtracking

### Pattern Recognition
- Generate all solutions
- Constraint satisfaction
- "Find all combinations/permutations"
- Decision tree problems

### Template

```python
def backtrack(path, choices):
    # Base case
    if is_solution(path):
        result.append(path[:])
        return
    
    # Try each choice
    for choice in choices:
        # Make choice
        path.append(choice)
        # Recurse
        backtrack(path, remaining_choices)
        # Undo choice (backtrack)
        path.pop()
```

#### Basic Level

1. **Subsets** - [LeetCode 78](https://leetcode.com/problems/subsets/)
   - Time: O(2^n), Space: O(n)

2. **Combinations** - [LeetCode 77](https://leetcode.com/problems/combinations/)
   - Time: O(C(n,k)), Space: O(k)

#### Medium Level

3. **Permutations** - [LeetCode 46](https://leetcode.com/problems/permutations/)
   - Time: O(n! * n), Space: O(n)

4. **Combination Sum** - [LeetCode 39](https://leetcode.com/problems/combination-sum/)
   - Time: O(2^target), Space: O(target)

5. **Word Search** - [LeetCode 79](https://leetcode.com/problems/word-search/)
   - Time: O(m*n*4^L), Space: O(L)

6. **N-Queens** - [LeetCode 51](https://leetcode.com/problems/n-queens/)
   - Time: O(N!), Space: O(N)

7. **Generate Parentheses** - [LeetCode 22](https://leetcode.com/problems/generate-parentheses/)
   - Time: O(4^n / sqrt(n)), Space: O(n)

#### Hard Level

8. **Sudoku Solver** - [LeetCode 37](https://leetcode.com/problems/sudoku-solver/)
   - Time: O(9^m), Space: O(1)

9. **Word Search II** - [LeetCode 212](https://leetcode.com/problems/word-search-ii/)
   - Pattern: Backtracking + Trie
   - Time: O(m*n*4*3^(L-1)), Space: O(L)

10. **Remove Invalid Parentheses** - [LeetCode 301](https://leetcode.com/problems/remove-invalid-parentheses/)
    - Time: O(2^n), Space: O(n)

---

## Greedy Algorithms

### Pattern Recognition
- Local optimal choices
- "Minimum/Maximum" problems
- Interval problems
- Activity selection

#### Basic Level

1. **Best Time to Buy and Sell Stock** - [LeetCode 121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
   - Time: O(n), Space: O(1)

2. **Jump Game** - [LeetCode 55](https://leetcode.com/problems/jump-game/)
   - Time: O(n), Space: O(1)

#### Medium Level

3. **Jump Game II** - [LeetCode 45](https://leetcode.com/problems/jump-game-ii/)
   - Time: O(n), Space: O(1)

4. **Gas Station** - [LeetCode 134](https://leetcode.com/problems/gas-station/)
   - Time: O(n), Space: O(1)

5. **Non-overlapping Intervals** - [LeetCode 435](https://leetcode.com/problems/non-overlapping-intervals/)
   - Time: O(n log n), Space: O(1)

6. **Merge Intervals** - [LeetCode 56](https://leetcode.com/problems/merge-intervals/)
   - Time: O(n log n), Space: O(n)

#### Hard Level

7. **Candy** - [LeetCode 135](https://leetcode.com/problems/candy/)
   - Time: O(n), Space: O(n)

8. **Insert Interval** - [LeetCode 57](https://leetcode.com/problems/insert-interval/)
   - Time: O(n), Space: O(n)

---

## Trie (Prefix Tree)

### Pattern Recognition
- Prefix matching
- Word dictionary problems
- Autocomplete
- String prefix/suffix queries

### Implementation

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
```

#### Medium Level

1. **Implement Trie** - [LeetCode 208](https://leetcode.com/problems/implement-trie-prefix-tree/)
   - Time: O(m) insert/search, Space: O(ALPHABET_SIZE * N * M)

2. **Word Search II** - [LeetCode 212](https://leetcode.com/problems/word-search-ii/)
   - Pattern: Trie + Backtracking
   - Time: O(m*n*4*3^(L-1)), Space: O(L)

3. **Design Add and Search Words** - [LeetCode 211](https://leetcode.com/problems/design-add-and-search-words-data-structure/)
   - Pattern: Trie + DFS
   - Time: O(m) add, O(m*26^k) search, Space: O(ALPHABET_SIZE * N * M)

#### Hard Level

4. **Concatenated Words** - [LeetCode 472](https://leetcode.com/problems/concatenated-words/)
   - Pattern: Trie + DP
   - Time: O(N * L²), Space: O(N * L)

---

## Union-Find (Disjoint Set)

### Pattern Recognition
- Connected components
- Dynamic connectivity
- Cycle detection in undirected graphs
- "Find if connected", "merge groups"

### Implementation

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
    
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # Path compression
        return self.parent[x]
    
    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        if root_x == root_y:
            return
        if self.rank[root_x] < self.rank[root_y]:
            self.parent[root_x] = root_y
        elif self.rank[root_x] > self.rank[root_y]:
            self.parent[root_y] = root_x
        else:
            self.parent[root_y] = root_x
            self.rank[root_x] += 1
```

#### Medium Level

1. **Number of Islands** - [LeetCode 200](https://leetcode.com/problems/number-of-islands/)
   - Pattern: Union-Find alternative
   - Time: O(m*n), Space: O(m*n)

2. **Redundant Connection** - [LeetCode 684](https://leetcode.com/problems/redundant-connection/)
   - Pattern: Cycle detection
   - Time: O(n), Space: O(n)

#### Hard Level

3. **Accounts Merge** - [LeetCode 721](https://leetcode.com/problems/accounts-merge/)
   - Pattern: Union-Find + Hash map
   - Time: O(n*k*log(n*k)), Space: O(n*k)

4. **Number of Islands II** - [LeetCode 305](https://leetcode.com/problems/number-of-islands-ii/)
   - Pattern: Union-Find with dynamic updates
   - Time: O(m*n + L), Space: O(m*n)

---

## Segment Trees & Fenwick Trees

### Pattern Recognition
- Range queries (sum, min, max)
- Range updates
- "Query range [L, R]"
- "Update element at index"

### Segment Tree Template

```python
class SegmentTree:
    def __init__(self, arr):
        self.n = len(arr)
        self.size = 1
        while self.size < self.n:
            self.size *= 2
        self.tree = [0] * (2 * self.size)
        for i in range(self.n):
            self.tree[self.size + i] = arr[i]
        for i in range(self.size - 1, 0, -1):
            self.tree[i] = self.tree[2*i] + self.tree[2*i + 1]
    
    def update(self, index, value):
        index += self.size
        self.tree[index] = value
        while index > 1:
            index //= 2
            self.tree[index] = self.tree[2*index] + self.tree[2*index + 1]
    
    def query(self, l, r):
        l += self.size
        r += self.size
        res = 0
        while l < r:
            if l % 2 == 1:
                res += self.tree[l]
                l += 1
            if r % 2 == 1:
                r -= 1
                res += self.tree[r]
            l //= 2
            r //= 2
        return res
```

#### Hard Level

1. **Range Sum Query - Mutable** - [LeetCode 307](https://leetcode.com/problems/range-sum-query-mutable/)
   - Time: O(log n) update/query, Space: O(n)

2. **Count of Smaller Numbers After Self** - [LeetCode 315](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)
   - Pattern: Segment Tree or Fenwick Tree
   - Time: O(n log n), Space: O(n)

---

## Advanced Topics

### 1. Monotonic Stack/Queue
- **Pattern**: Maintain increasing/decreasing order
- **Problems**: Next greater element, sliding window maximum
- **Time**: Usually O(n)

### 2. Sliding Window with Deque
- **Pattern**: Maintain window with deque
- **Problems**: Sliding window maximum/minimum
- **Time**: O(n)

### 3. Binary Search on Answer
- **Pattern**: Search on answer space, not array
- **Problems**: Split array, koko eating bananas
- **Time**: O(n * log(max))

### 4. State Machine DP
- **Pattern**: Multiple states, transitions
- **Problems**: Stock problems with cooldown
- **Time**: Usually O(n)

### 5. Interval DP
- **Pattern**: DP on intervals
- **Problems**: Matrix chain, burst balloons
- **Time**: Usually O(n³)

### 6. Bit Manipulation
- **Pattern**: Use bits to represent states
- **Problems**: Subset generation, bit masks
- **Time**: Usually O(2^n)

#### Hard Problems

1. **N-Queens** - [LeetCode 51](https://leetcode.com/problems/n-queens/)
2. **Word Ladder II** - [LeetCode 126](https://leetcode.com/problems/word-ladder-ii/)
3. **Serialize and Deserialize N-ary Tree** - [LeetCode 428](https://leetcode.com/problems/serialize-and-deserialize-n-ary-tree/)
4. **Design Search Autocomplete System** - [LeetCode 642](https://leetcode.com/problems/design-search-autocomplete-system/)

---

## Pattern Recognition Guide

### How to Identify Patterns

#### 1. **Array/String Problems**
- **Two Pointers**: Sorted array, palindrome, pair sum
- **Sliding Window**: Subarray/substring, "longest/shortest with K"
- **Hash Map**: Frequency, lookup, grouping
- **Sorting**: "Kth largest/smallest", "merge intervals"

#### 2. **Tree Problems**
- **DFS**: Path problems, tree construction
- **BFS**: Level order, shortest path
- **Inorder**: BST problems
- **Postorder**: Tree deletion, subtree problems

#### 3. **Graph Problems**
- **DFS**: Connected components, cycle detection
- **BFS**: Shortest path (unweighted)
- **Topological Sort**: DAG, prerequisites
- **Union-Find**: Dynamic connectivity

#### 4. **DP Problems**
- **1D DP**: Linear problems, "ways to reach"
- **2D DP**: Grid, two sequences
- **Knapsack**: "Subset sum", "partition"
- **Interval DP**: "Optimal way to split"

#### 5. **Backtracking Problems**
- **Generate all**: Permutations, combinations
- **Constraint satisfaction**: N-Queens, Sudoku
- **Decision tree**: "Try all possibilities"

### Problem-Solving Framework

1. **Understand**: Read problem carefully, identify constraints
2. **Examples**: Work through examples manually
3. **Pattern**: Identify which pattern applies
4. **Algorithm**: Choose appropriate algorithm
5. **Complexity**: Analyze time and space complexity
6. **Edge Cases**: Consider empty, single element, duplicates
7. **Code**: Implement cleanly
8. **Test**: Test with examples and edge cases

---

## Interview Preparation Strategy

### 8-Week Plan

#### **Week 1-2: Foundation**
- Arrays, Strings, Hash Maps
- Two Pointers, Sliding Window
- Basic Tree and Graph traversals
- **Goal**: Solve 50 Easy, 20 Medium problems

#### **Week 3-4: Core Algorithms**
- Binary Search
- Stacks, Queues
- Linked Lists
- Advanced Tree problems
- **Goal**: Solve 30 Medium, 10 Hard problems

#### **Week 5-6: Advanced Topics**
- Dynamic Programming (all patterns)
- Backtracking
- Graph algorithms (DFS, BFS, Topological)
- **Goal**: Solve 40 Medium, 15 Hard problems

#### **Week 7: Specialized Structures**
- Trie, Union-Find
- Segment Trees (if time)
- Greedy algorithms
- **Goal**: Solve 20 Medium, 10 Hard problems

#### **Week 8: Mock Interviews & Revision**
- Solve 3-5 problems daily
- Focus on Hard problems
- Mock interviews
- **Goal**: Solve 30 Hard problems

### Daily Practice Routine

1. **Morning (1 hour)**: Learn new concept, solve 1-2 problems
2. **Evening (1-2 hours)**: Solve 2-3 problems, review solutions
3. **Weekend**: Mock interviews, solve Hard problems

### Problem Selection Strategy

1. **By Pattern**: Master one pattern before moving to next
2. **By Difficulty**: Start Easy, progress to Hard
3. **By Company**: Practice company-specific problems
4. **By Frequency**: Focus on frequently asked problems

### Tips for Success

1. **Don't Memorize**: Understand the pattern, not the solution
2. **Time Yourself**: Practice with time constraints
3. **Explain Aloud**: Practice explaining your approach
4. **Review Mistakes**: Learn from wrong solutions
5. **Consistency**: Practice daily, even if just 30 minutes
6. **Mock Interviews**: Practice with peers or platforms

---

## Resources

### LeetCode
- **LeetCode Premium**: Company-specific problems
- **LeetCode Discuss**: Solutions and explanations
- **LeetCode Contest**: Weekly practice

### Other Platforms
- **Codeforces**: Competitive programming
- **HackerRank**: Practice problems
- **InterviewBit**: Structured learning path
- **GeeksforGeeks**: Theory and problems

### Books
- **Cracking the Coding Interview**: Problem-solving approach
- **Elements of Programming Interviews**: Comprehensive guide
- **Algorithm Design Manual**: Deep understanding

### YouTube Channels
- **NeetCode**: Pattern-based explanations
- **Back To Back SWE**: Detailed problem walkthroughs
- **Tech Dummies Narendra L**: Indian perspective

### Practice Lists
- **Blind 75**: Must-solve problems
- **Grind 75**: Updated version of Blind 75
- **NeetCode 150**: Pattern-based problem list

### Python Resources
- **Python Official Docs**: Language reference
- **Real Python**: Python tutorials
- **Python Tricks**: Advanced Python features

---

## Final Notes

### Key Takeaways

1. **Pattern Recognition**: Most important skill - identify patterns quickly
2. **Time Complexity**: Always analyze and optimize
3. **Practice**: Consistency beats intensity
4. **Mock Interviews**: Essential for interview success
5. **Stay Calm**: Problem-solving under pressure is a skill

### Common Mistakes to Avoid

1. Jumping to code without understanding
2. Not considering edge cases
3. Ignoring time/space complexity
4. Memorizing solutions instead of patterns
5. Not practicing enough Hard problems

### Success Metrics

- Can identify pattern in < 2 minutes
- Can solve Medium in < 20 minutes
- Can solve Hard in < 40 minutes
- Can explain approach clearly
- Comfortable with all major patterns

### Remember

> "The goal is not to solve every problem, but to recognize patterns and apply the right algorithm efficiently."

Good luck with your preparation! 🚀

---

**Last Updated**: 2024
**Total Problems Listed**: 150+
**Difficulty Levels**: Basic, Medium, Hard, Very Hard
**Languages**: Python

