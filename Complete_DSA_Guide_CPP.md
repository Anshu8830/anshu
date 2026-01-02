# Complete DSA Guide: From Basics to Advanced (C++)

## Table of Contents
1. [Introduction](#introduction)
2. [C++ Fundamentals for DSA](#c-fundamentals-for-dsa)
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

### Your Journey
- **Background**: B.Tech CS, 2.5 years Data Engineering experience
- **Goal**: Master DSA in C++ to crack tier-1 company interviews (40-50 LPA CTC)
- **Target**: LeetCode Hard, Codeforces problems

### Learning Approach
1. **Pattern-Based Learning**: Understand problem patterns, not just solutions
2. **Progressive Difficulty**: Start with basics, gradually move to advanced
3. **Practice**: Solve 2-3 problems per topic at each difficulty level
4. **Time Complexity**: Always analyze time and space complexity
5. **Code Quality**: Write clean, readable, optimized code

### C++ Advantages for DSA
- **Performance**: Faster execution, crucial for competitive programming
- **STL**: Powerful Standard Template Library with optimized containers
- **Memory Control**: Direct memory management when needed
- **Competitive Programming**: Preferred language in contests (Codeforces, ICPC)
- **Industry**: Many system-level companies prefer C++

---

## C++ Fundamentals for DSA

### Essential Headers

```cpp
#include <bits/stdc++.h>  // Includes everything (competitive programming)
using namespace std;

// Or specific headers for interviews:
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <unordered_set>
#include <map>
#include <set>
#include <queue>
#include <stack>
#include <algorithm>
#include <numeric>
#include <climits>
```

### Essential Data Structures

```cpp
// Vector (Dynamic Array)
vector<int> arr = {1, 2, 3};
arr.push_back(4);        // O(1) amortized
arr.pop_back();          // O(1)
arr.insert(arr.begin(), 0);  // O(n)
arr[0];                  // O(1)
arr.size();              // O(1)
arr.empty();             // O(1)

// String
string s = "hello";
s += "world";            // O(m)
s.substr(0, 3);          // O(k)
s.find("lo");            // O(n*m)
s.length();              // O(1)

// Unordered Map (Hash Map)
unordered_map<string, int> mp;
mp["key"] = 1;           // O(1) average
mp.count("key");         // O(1) average
mp.find("key");          // O(1) average
mp.erase("key");         // O(1) average

// Unordered Set (Hash Set)
unordered_set<int> st;
st.insert(1);            // O(1) average
st.count(1);             // O(1) average
st.erase(1);             // O(1) average

// Ordered Map (Red-Black Tree)
map<int, int> orderedMap;
orderedMap[1] = 10;      // O(log n)
orderedMap.lower_bound(5);  // O(log n)

// Ordered Set (Red-Black Tree)
set<int> orderedSet;
orderedSet.insert(1);    // O(log n)
orderedSet.lower_bound(5);  // O(log n)

// Deque (Double-ended Queue)
deque<int> dq;
dq.push_back(1);         // O(1)
dq.push_front(0);        // O(1)
dq.pop_back();           // O(1)
dq.pop_front();          // O(1)

// Priority Queue (Max Heap by default)
priority_queue<int> maxHeap;
maxHeap.push(3);         // O(log n)
maxHeap.top();           // O(1)
maxHeap.pop();           // O(log n)

// Min Heap
priority_queue<int, vector<int>, greater<int>> minHeap;
minHeap.push(3);         // O(log n)
minHeap.top();           // O(1)
minHeap.pop();           // O(log n)

// Pair
pair<int, int> p = {1, 2};
p.first;                 // 1
p.second;                // 2

// Tuple
tuple<int, string, double> t = {1, "hello", 3.14};
get<0>(t);               // 1
```

### Useful C++ Tricks

```cpp
// Range-based for loop
for (int x : arr) { cout << x; }
for (int& x : arr) { x *= 2; }  // Modify elements
for (const auto& [key, val] : mp) { cout << key << val; }  // C++17

// Lambda functions
auto cmp = [](int a, int b) { return a > b; };
sort(arr.begin(), arr.end(), cmp);

// Custom comparator for priority_queue
auto cmp = [](pair<int,int>& a, pair<int,int>& b) {
    return a.first > b.first;  // Min heap by first element
};
priority_queue<pair<int,int>, vector<pair<int,int>>, decltype(cmp)> pq(cmp);

// Sorting
sort(arr.begin(), arr.end());                    // Ascending
sort(arr.begin(), arr.end(), greater<int>());    // Descending
sort(arr.begin(), arr.end(), [](int a, int b) {  // Custom
    return a > b;
});

// Binary search (on sorted array)
binary_search(arr.begin(), arr.end(), target);   // Returns bool
lower_bound(arr.begin(), arr.end(), target);     // First >= target
upper_bound(arr.begin(), arr.end(), target);     // First > target

// Min/Max
int mx = *max_element(arr.begin(), arr.end());
int mn = *min_element(arr.begin(), arr.end());
auto [minIt, maxIt] = minmax_element(arr.begin(), arr.end());  // C++17

// Sum
int sum = accumulate(arr.begin(), arr.end(), 0);

// Reverse
reverse(arr.begin(), arr.end());

// Unique (removes consecutive duplicates)
arr.erase(unique(arr.begin(), arr.end()), arr.end());

// Fill
fill(arr.begin(), arr.end(), 0);
memset(arr, 0, sizeof(arr));  // For C-style arrays

// 2D Vector initialization
vector<vector<int>> grid(m, vector<int>(n, 0));

// String to int and vice versa
int num = stoi("123");
string str = to_string(123);

// Character operations
isalpha(c);   // Is letter
isdigit(c);   // Is digit
isalnum(c);   // Is alphanumeric
tolower(c);   // Convert to lowercase
toupper(c);   // Convert to uppercase
```

### Input/Output Optimization

```cpp
// Fast I/O for competitive programming
ios_base::sync_with_stdio(false);
cin.tie(NULL);

// Reading input
int n;
cin >> n;
vector<int> arr(n);
for (int i = 0; i < n; i++) cin >> arr[i];

// Reading line with spaces
string line;
getline(cin, line);

// Output
cout << "Answer: " << ans << "\n";  // Use "\n" instead of endl (faster)
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

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> mp;
    for (int i = 0; i < nums.size(); i++) {
        int complement = target - nums[i];
        if (mp.count(complement)) {
            return {mp[complement], i};
        }
        mp[nums[i]] = i;
    }
    return {};
}
```

2. **Best Time to Buy and Sell Stock** - [LeetCode 121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
   - Pattern: Track minimum price
   - Time: O(n), Space: O(1)

```cpp
int maxProfit(vector<int>& prices) {
    int minPrice = INT_MAX, maxProfit = 0;
    for (int price : prices) {
        minPrice = min(minPrice, price);
        maxProfit = max(maxProfit, price - minPrice);
    }
    return maxProfit;
}
```

3. **Contains Duplicate** - [LeetCode 217](https://leetcode.com/problems/contains-duplicate/)
   - Pattern: Set for O(1) lookup
   - Time: O(n), Space: O(n)

4. **Maximum Subarray** - [LeetCode 53](https://leetcode.com/problems/maximum-subarray/)
   - Pattern: Kadane's algorithm
   - Time: O(n), Space: O(1)

```cpp
int maxSubArray(vector<int>& nums) {
    int maxSum = nums[0], currentSum = nums[0];
    for (int i = 1; i < nums.size(); i++) {
        currentSum = max(nums[i], currentSum + nums[i]);
        maxSum = max(maxSum, currentSum);
    }
    return maxSum;
}
```

5. **Product of Array Except Self** - [LeetCode 238](https://leetcode.com/problems/product-of-array-except-self/)
   - Pattern: Prefix and suffix products
   - Time: O(n), Space: O(1) excluding output

#### Medium Level

6. **3Sum** - [LeetCode 15](https://leetcode.com/problems/3sum/)
   - Pattern: Two pointers after sorting
   - Time: O(n²), Space: O(1)

```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> result;
    sort(nums.begin(), nums.end());
    int n = nums.size();
    
    for (int i = 0; i < n - 2; i++) {
        if (i > 0 && nums[i] == nums[i-1]) continue;  // Skip duplicates
        
        int left = i + 1, right = n - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum == 0) {
                result.push_back({nums[i], nums[left], nums[right]});
                while (left < right && nums[left] == nums[left+1]) left++;
                while (left < right && nums[right] == nums[right-1]) right--;
                left++; right--;
            } else if (sum < 0) {
                left++;
            } else {
                right--;
            }
        }
    }
    return result;
}
```

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

```cpp
int trap(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int leftMax = 0, rightMax = 0;
    int water = 0;
    
    while (left < right) {
        if (height[left] < height[right]) {
            if (height[left] >= leftMax) {
                leftMax = height[left];
            } else {
                water += leftMax - height[left];
            }
            left++;
        } else {
            if (height[right] >= rightMax) {
                rightMax = height[right];
            } else {
                water += rightMax - height[right];
            }
            right--;
        }
    }
    return water;
}
```

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

```cpp
bool isPalindrome(string s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        while (left < right && !isalnum(s[left])) left++;
        while (left < right && !isalnum(s[right])) right--;
        if (tolower(s[left]) != tolower(s[right])) return false;
        left++; right--;
    }
    return true;
}
```

2. **Squares of a Sorted Array** - [LeetCode 977](https://leetcode.com/problems/squares-of-a-sorted-array/)
   - Time: O(n), Space: O(n)

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

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> charIndex;
    int maxLen = 0, start = 0;
    
    for (int end = 0; end < s.length(); end++) {
        if (charIndex.count(s[end]) && charIndex[s[end]] >= start) {
            start = charIndex[s[end]] + 1;
        }
        charIndex[s[end]] = end;
        maxLen = max(maxLen, end - start + 1);
    }
    return maxLen;
}
```

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

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;  // Store indices
    vector<int> result;
    
    for (int i = 0; i < nums.size(); i++) {
        // Remove indices outside window
        while (!dq.empty() && dq.front() <= i - k) {
            dq.pop_front();
        }
        // Remove smaller elements
        while (!dq.empty() && nums[dq.back()] < nums[i]) {
            dq.pop_back();
        }
        dq.push_back(i);
        
        if (i >= k - 1) {
            result.push_back(nums[dq.front()]);
        }
    }
    return result;
}
```

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

```cpp
bool containsDuplicate(vector<int>& nums) {
    unordered_set<int> seen;
    for (int num : nums) {
        if (seen.count(num)) return true;
        seen.insert(num);
    }
    return false;
}
```

3. **Valid Anagram** - [LeetCode 242](https://leetcode.com/problems/valid-anagram/)
   - Time: O(n), Space: O(1) if fixed alphabet

#### Medium Level

4. **Group Anagrams** - [LeetCode 49](https://leetcode.com/problems/group-anagrams/)
   - Time: O(n*k log k), Space: O(n*k)

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> groups;
    for (const string& s : strs) {
        string key = s;
        sort(key.begin(), key.end());
        groups[key].push_back(s);
    }
    
    vector<vector<string>> result;
    for (auto& [key, group] : groups) {
        result.push_back(move(group));
    }
    return result;
}
```

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

```cpp
class LRUCache {
    int capacity;
    list<pair<int, int>> cache;  // {key, value}
    unordered_map<int, list<pair<int, int>>::iterator> mp;
    
public:
    LRUCache(int capacity) : capacity(capacity) {}
    
    int get(int key) {
        if (!mp.count(key)) return -1;
        // Move to front
        cache.splice(cache.begin(), cache, mp[key]);
        return mp[key]->second;
    }
    
    void put(int key, int value) {
        if (mp.count(key)) {
            mp[key]->second = value;
            cache.splice(cache.begin(), cache, mp[key]);
            return;
        }
        if (cache.size() == capacity) {
            int oldKey = cache.back().first;
            cache.pop_back();
            mp.erase(oldKey);
        }
        cache.push_front({key, value});
        mp[key] = cache.begin();
    }
};
```

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

### Node Definition

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode* next) : val(x), next(next) {}
};
```

#### Basic Level

1. **Reverse Linked List** - [LeetCode 206](https://leetcode.com/problems/reverse-linked-list/)
   - Pattern: Iterative or recursive
   - Time: O(n), Space: O(1) iterative, O(n) recursive

```cpp
// Iterative
ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    while (curr) {
        ListNode* next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}

// Recursive
ListNode* reverseListRecursive(ListNode* head) {
    if (!head || !head->next) return head;
    ListNode* newHead = reverseListRecursive(head->next);
    head->next->next = head;
    head->next = nullptr;
    return newHead;
}
```

2. **Merge Two Sorted Lists** - [LeetCode 21](https://leetcode.com/problems/merge-two-sorted-lists/)
   - Time: O(n + m), Space: O(1)

3. **Linked List Cycle** - [LeetCode 141](https://leetcode.com/problems/linked-list-cycle/)
   - Pattern: Floyd's cycle detection
   - Time: O(n), Space: O(1)

```cpp
bool hasCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}
```

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

```cpp
ListNode* mergeKLists(vector<ListNode*>& lists) {
    auto cmp = [](ListNode* a, ListNode* b) { return a->val > b->val; };
    priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> pq(cmp);
    
    for (ListNode* list : lists) {
        if (list) pq.push(list);
    }
    
    ListNode dummy(0);
    ListNode* tail = &dummy;
    
    while (!pq.empty()) {
        ListNode* node = pq.top();
        pq.pop();
        tail->next = node;
        tail = tail->next;
        if (node->next) pq.push(node->next);
    }
    return dummy.next;
}
```

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

```cpp
bool isValid(string s) {
    stack<char> st;
    unordered_map<char, char> pairs = {{')', '('}, {']', '['}, {'}', '{'}};
    
    for (char c : s) {
        if (pairs.count(c)) {
            if (st.empty() || st.top() != pairs[c]) return false;
            st.pop();
        } else {
            st.push(c);
        }
    }
    return st.empty();
}
```

2. **Implement Queue using Stacks** - [LeetCode 232](https://leetcode.com/problems/implement-queue-using-stacks/)
   - Time: O(1) amortized, Space: O(n)

3. **Implement Stack using Queues** - [LeetCode 225](https://leetcode.com/problems/implement-stack-using-queues/)
   - Time: O(n) push, O(1) pop, Space: O(n)

#### Medium Level

4. **Daily Temperatures** - [LeetCode 739](https://leetcode.com/problems/daily-temperatures/)
   - Pattern: Monotonic stack
   - Time: O(n), Space: O(n)

```cpp
vector<int> dailyTemperatures(vector<int>& temperatures) {
    int n = temperatures.size();
    vector<int> result(n, 0);
    stack<int> st;  // Store indices
    
    for (int i = 0; i < n; i++) {
        while (!st.empty() && temperatures[i] > temperatures[st.top()]) {
            int idx = st.top();
            st.pop();
            result[idx] = i - idx;
        }
        st.push(i);
    }
    return result;
}
```

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

```cpp
int largestRectangleArea(vector<int>& heights) {
    stack<int> st;
    int maxArea = 0;
    int n = heights.size();
    
    for (int i = 0; i <= n; i++) {
        int h = (i == n) ? 0 : heights[i];
        while (!st.empty() && h < heights[st.top()]) {
            int height = heights[st.top()];
            st.pop();
            int width = st.empty() ? i : i - st.top() - 1;
            maxArea = max(maxArea, height * width);
        }
        st.push(i);
    }
    return maxArea;
}
```

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

### Node Definition

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
```

### Binary Tree Traversals

```cpp
// Preorder: Root -> Left -> Right
void preorder(TreeNode* root, vector<int>& result) {
    if (!root) return;
    result.push_back(root->val);
    preorder(root->left, result);
    preorder(root->right, result);
}

// Inorder: Left -> Root -> Right
void inorder(TreeNode* root, vector<int>& result) {
    if (!root) return;
    inorder(root->left, result);
    result.push_back(root->val);
    inorder(root->right, result);
}

// Postorder: Left -> Right -> Root
void postorder(TreeNode* root, vector<int>& result) {
    if (!root) return;
    postorder(root->left, result);
    postorder(root->right, result);
    result.push_back(root->val);
}

// Level Order (BFS)
vector<vector<int>> levelOrder(TreeNode* root) {
    if (!root) return {};
    vector<vector<int>> result;
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int size = q.size();
        vector<int> level;
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            level.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(level);
    }
    return result;
}
```

#### Basic Level

1. **Maximum Depth of Binary Tree** - [LeetCode 104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
   - Time: O(n), Space: O(h)

```cpp
int maxDepth(TreeNode* root) {
    if (!root) return 0;
    return 1 + max(maxDepth(root->left), maxDepth(root->right));
}
```

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

```cpp
bool isValidBST(TreeNode* root, long minVal = LONG_MIN, long maxVal = LONG_MAX) {
    if (!root) return true;
    if (root->val <= minVal || root->val >= maxVal) return false;
    return isValidBST(root->left, minVal, root->val) &&
           isValidBST(root->right, root->val, maxVal);
}
```

8. **Kth Smallest Element in BST** - [LeetCode 230](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
   - Pattern: Inorder traversal
   - Time: O(h + k), Space: O(h)

9. **Lowest Common Ancestor** - [LeetCode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
   - Pattern: DFS with backtracking
   - Time: O(n), Space: O(h)

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    if (left && right) return root;
    return left ? left : right;
}
```

10. **Path Sum II** - [LeetCode 113](https://leetcode.com/problems/path-sum-ii/)
    - Pattern: DFS + backtracking
    - Time: O(n), Space: O(h)

#### Hard Level

11. **Binary Tree Maximum Path Sum** - [LeetCode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
    - Pattern: DFS with path calculation
    - Time: O(n), Space: O(h)

```cpp
class Solution {
    int maxSum = INT_MIN;
    
    int maxGain(TreeNode* node) {
        if (!node) return 0;
        int leftGain = max(maxGain(node->left), 0);
        int rightGain = max(maxGain(node->right), 0);
        int pathSum = node->val + leftGain + rightGain;
        maxSum = max(maxSum, pathSum);
        return node->val + max(leftGain, rightGain);
    }
    
public:
    int maxPathSum(TreeNode* root) {
        maxGain(root);
        return maxSum;
    }
};
```

12. **Serialize and Deserialize Binary Tree** - [LeetCode 297](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
    - Pattern: Preorder traversal
    - Time: O(n), Space: O(n)

---

## Binary Search

### Pattern Recognition
- Sorted arrays
- Search in rotated arrays
- Finding boundaries
- "Find minimum/maximum satisfying condition"

### Template

```cpp
int binarySearch(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}
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

```cpp
int search(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        
        // Left half is sorted
        if (nums[left] <= nums[mid]) {
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        // Right half is sorted
        else {
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }
    return -1;
}
```

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

```cpp
// Adjacency List
unordered_map<int, vector<int>> graph = {
    {0, {1, 2}},
    {1, {0, 3}},
    {2, {0, 3}},
    {3, {1, 2}}
};

// Adjacency Matrix
vector<vector<int>> graph = {
    {0, 1, 1, 0},
    {1, 0, 0, 1},
    {1, 0, 0, 1},
    {0, 1, 1, 0}
};

// Edge List
vector<pair<int, int>> edges = {{0, 1}, {0, 2}, {1, 3}, {2, 3}};
```

### DFS Template

```cpp
void dfs(unordered_map<int, vector<int>>& graph, int node, unordered_set<int>& visited) {
    visited.insert(node);
    for (int neighbor : graph[node]) {
        if (!visited.count(neighbor)) {
            dfs(graph, neighbor, visited);
        }
    }
}
```

### BFS Template

```cpp
void bfs(unordered_map<int, vector<int>>& graph, int start) {
    queue<int> q;
    unordered_set<int> visited;
    q.push(start);
    visited.insert(start);
    
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        for (int neighbor : graph[node]) {
            if (!visited.count(neighbor)) {
                visited.insert(neighbor);
                q.push(neighbor);
            }
        }
    }
}
```

#### Basic Level

1. **Number of Islands** - [LeetCode 200](https://leetcode.com/problems/number-of-islands/)
   - Pattern: DFS/BFS on grid
   - Time: O(m*n), Space: O(m*n)

```cpp
class Solution {
    void dfs(vector<vector<char>>& grid, int i, int j) {
        if (i < 0 || i >= grid.size() || j < 0 || j >= grid[0].size() || grid[i][j] == '0')
            return;
        grid[i][j] = '0';
        dfs(grid, i + 1, j);
        dfs(grid, i - 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i, j - 1);
    }
    
public:
    int numIslands(vector<vector<char>>& grid) {
        int count = 0;
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == '1') {
                    dfs(grid, i, j);
                    count++;
                }
            }
        }
        return count;
    }
};
```

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

```cpp
vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
    vector<vector<int>> graph(numCourses);
    vector<int> inDegree(numCourses, 0);
    
    for (auto& pre : prerequisites) {
        graph[pre[1]].push_back(pre[0]);
        inDegree[pre[0]]++;
    }
    
    queue<int> q;
    for (int i = 0; i < numCourses; i++) {
        if (inDegree[i] == 0) q.push(i);
    }
    
    vector<int> result;
    while (!q.empty()) {
        int course = q.front();
        q.pop();
        result.push_back(course);
        for (int next : graph[course]) {
            if (--inDegree[next] == 0) q.push(next);
        }
    }
    
    return result.size() == numCourses ? result : vector<int>();
}
```

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

```cpp
int networkDelayTime(vector<vector<int>>& times, int n, int k) {
    vector<vector<pair<int, int>>> graph(n + 1);
    for (auto& t : times) {
        graph[t[0]].push_back({t[1], t[2]});
    }
    
    vector<int> dist(n + 1, INT_MAX);
    dist[k] = 0;
    
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
    pq.push({0, k});
    
    while (!pq.empty()) {
        auto [d, u] = pq.top();
        pq.pop();
        if (d > dist[u]) continue;
        
        for (auto& [v, w] : graph[u]) {
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }
    
    int maxDist = *max_element(dist.begin() + 1, dist.end());
    return maxDist == INT_MAX ? -1 : maxDist;
}
```

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

```cpp
// 1. Define state
// 2. Define recurrence relation
// 3. Base cases
// 4. Order of computation
// 5. Return answer

// Example: Fibonacci
int fib(int n) {
    if (n <= 1) return n;
    vector<int> dp(n + 1);
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

#### Basic Level

1. **Climbing Stairs** - [LeetCode 70](https://leetcode.com/problems/climbing-stairs/)
   - Pattern: 1D DP
   - Time: O(n), Space: O(1)

```cpp
int climbStairs(int n) {
    if (n <= 2) return n;
    int prev2 = 1, prev1 = 2;
    for (int i = 3; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

2. **House Robber** - [LeetCode 198](https://leetcode.com/problems/house-robber/)
   - Pattern: 1D DP with choice
   - Time: O(n), Space: O(1)

```cpp
int rob(vector<int>& nums) {
    int prev2 = 0, prev1 = 0;
    for (int num : nums) {
        int curr = max(prev1, prev2 + num);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

3. **Coin Change** - [LeetCode 322](https://leetcode.com/problems/coin-change/)
   - Pattern: Unbounded knapsack
   - Time: O(amount * coins), Space: O(amount)

```cpp
int coinChange(vector<int>& coins, int amount) {
    vector<int> dp(amount + 1, amount + 1);
    dp[0] = 0;
    for (int i = 1; i <= amount; i++) {
        for (int coin : coins) {
            if (coin <= i) {
                dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}
```

4. **Longest Increasing Subsequence** - [LeetCode 300](https://leetcode.com/problems/longest-increasing-subsequence/)
   - Pattern: 1D DP or binary search
   - Time: O(n²) or O(n log n), Space: O(n)

```cpp
// O(n log n) solution
int lengthOfLIS(vector<int>& nums) {
    vector<int> tails;
    for (int num : nums) {
        auto it = lower_bound(tails.begin(), tails.end(), num);
        if (it == tails.end()) {
            tails.push_back(num);
        } else {
            *it = num;
        }
    }
    return tails.size();
}
```

#### Medium Level

5. **Unique Paths** - [LeetCode 62](https://leetcode.com/problems/unique-paths/)
   - Pattern: 2D DP
   - Time: O(m*n), Space: O(n)

6. **Longest Common Subsequence** - [LeetCode 1143](https://leetcode.com/problems/longest-common-subsequence/)
   - Pattern: 2D DP
   - Time: O(m*n), Space: O(min(m, n))

```cpp
int longestCommonSubsequence(string text1, string text2) {
    int m = text1.size(), n = text2.size();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1[i-1] == text2[j-1]) {
                dp[i][j] = dp[i-1][j-1] + 1;
            } else {
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    return dp[m][n];
}
```

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

```cpp
void backtrack(vector<int>& path, vector<int>& choices, vector<vector<int>>& result) {
    // Base case
    if (isSolution(path)) {
        result.push_back(path);
        return;
    }
    
    // Try each choice
    for (int choice : choices) {
        // Make choice
        path.push_back(choice);
        // Recurse
        backtrack(path, remainingChoices, result);
        // Undo choice (backtrack)
        path.pop_back();
    }
}
```

#### Basic Level

1. **Subsets** - [LeetCode 78](https://leetcode.com/problems/subsets/)
   - Time: O(2^n), Space: O(n)

```cpp
vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> path;
    
    function<void(int)> backtrack = [&](int start) {
        result.push_back(path);
        for (int i = start; i < nums.size(); i++) {
            path.push_back(nums[i]);
            backtrack(i + 1);
            path.pop_back();
        }
    };
    
    backtrack(0);
    return result;
}
```

2. **Combinations** - [LeetCode 77](https://leetcode.com/problems/combinations/)
   - Time: O(C(n,k)), Space: O(k)

#### Medium Level

3. **Permutations** - [LeetCode 46](https://leetcode.com/problems/permutations/)
   - Time: O(n! * n), Space: O(n)

```cpp
vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> result;
    
    function<void(int)> backtrack = [&](int start) {
        if (start == nums.size()) {
            result.push_back(nums);
            return;
        }
        for (int i = start; i < nums.size(); i++) {
            swap(nums[start], nums[i]);
            backtrack(start + 1);
            swap(nums[start], nums[i]);
        }
    };
    
    backtrack(0);
    return result;
}
```

4. **Combination Sum** - [LeetCode 39](https://leetcode.com/problems/combination-sum/)
   - Time: O(2^target), Space: O(target)

5. **Word Search** - [LeetCode 79](https://leetcode.com/problems/word-search/)
   - Time: O(m*n*4^L), Space: O(L)

6. **N-Queens** - [LeetCode 51](https://leetcode.com/problems/n-queens/)
   - Time: O(N!), Space: O(N)

7. **Generate Parentheses** - [LeetCode 22](https://leetcode.com/problems/generate-parentheses/)
   - Time: O(4^n / sqrt(n)), Space: O(n)

```cpp
vector<string> generateParenthesis(int n) {
    vector<string> result;
    
    function<void(string&, int, int)> backtrack = [&](string& path, int open, int close) {
        if (path.size() == 2 * n) {
            result.push_back(path);
            return;
        }
        if (open < n) {
            path += '(';
            backtrack(path, open + 1, close);
            path.pop_back();
        }
        if (close < open) {
            path += ')';
            backtrack(path, open, close + 1);
            path.pop_back();
        }
    };
    
    string path;
    backtrack(path, 0, 0);
    return result;
}
```

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

```cpp
bool canJump(vector<int>& nums) {
    int maxReach = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (i > maxReach) return false;
        maxReach = max(maxReach, i + nums[i]);
    }
    return true;
}
```

#### Medium Level

3. **Jump Game II** - [LeetCode 45](https://leetcode.com/problems/jump-game-ii/)
   - Time: O(n), Space: O(1)

4. **Gas Station** - [LeetCode 134](https://leetcode.com/problems/gas-station/)
   - Time: O(n), Space: O(1)

5. **Non-overlapping Intervals** - [LeetCode 435](https://leetcode.com/problems/non-overlapping-intervals/)
   - Time: O(n log n), Space: O(1)

6. **Merge Intervals** - [LeetCode 56](https://leetcode.com/problems/merge-intervals/)
   - Time: O(n log n), Space: O(n)

```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    sort(intervals.begin(), intervals.end());
    vector<vector<int>> result;
    
    for (auto& interval : intervals) {
        if (result.empty() || result.back()[1] < interval[0]) {
            result.push_back(interval);
        } else {
            result.back()[1] = max(result.back()[1], interval[1]);
        }
    }
    return result;
}
```

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

```cpp
class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEnd = false;
};

class Trie {
    TrieNode* root;
    
public:
    Trie() {
        root = new TrieNode();
    }
    
    void insert(const string& word) {
        TrieNode* node = root;
        for (char c : word) {
            if (!node->children.count(c)) {
                node->children[c] = new TrieNode();
            }
            node = node->children[c];
        }
        node->isEnd = true;
    }
    
    bool search(const string& word) {
        TrieNode* node = root;
        for (char c : word) {
            if (!node->children.count(c)) return false;
            node = node->children[c];
        }
        return node->isEnd;
    }
    
    bool startsWith(const string& prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            if (!node->children.count(c)) return false;
            node = node->children[c];
        }
        return true;
    }
};
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

```cpp
class UnionFind {
    vector<int> parent, rank_;
    
public:
    UnionFind(int n) {
        parent.resize(n);
        rank_.resize(n, 0);
        iota(parent.begin(), parent.end(), 0);  // parent[i] = i
    }
    
    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);  // Path compression
        }
        return parent[x];
    }
    
    void unite(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX == rootY) return;
        
        // Union by rank
        if (rank_[rootX] < rank_[rootY]) {
            parent[rootX] = rootY;
        } else if (rank_[rootX] > rank_[rootY]) {
            parent[rootY] = rootX;
        } else {
            parent[rootY] = rootX;
            rank_[rootX]++;
        }
    }
    
    bool connected(int x, int y) {
        return find(x) == find(y);
    }
};
```

#### Medium Level

1. **Number of Islands** - [LeetCode 200](https://leetcode.com/problems/number-of-islands/)
   - Pattern: Union-Find alternative
   - Time: O(m*n), Space: O(m*n)

2. **Redundant Connection** - [LeetCode 684](https://leetcode.com/problems/redundant-connection/)
   - Pattern: Cycle detection
   - Time: O(n), Space: O(n)

```cpp
vector<int> findRedundantConnection(vector<vector<int>>& edges) {
    int n = edges.size();
    UnionFind uf(n + 1);
    
    for (auto& edge : edges) {
        if (uf.connected(edge[0], edge[1])) {
            return edge;
        }
        uf.unite(edge[0], edge[1]);
    }
    return {};
}
```

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

```cpp
class SegmentTree {
    vector<int> tree;
    int n;
    
    void build(vector<int>& arr, int node, int start, int end) {
        if (start == end) {
            tree[node] = arr[start];
        } else {
            int mid = (start + end) / 2;
            build(arr, 2*node, start, mid);
            build(arr, 2*node+1, mid+1, end);
            tree[node] = tree[2*node] + tree[2*node+1];
        }
    }
    
    void update(int node, int start, int end, int idx, int val) {
        if (start == end) {
            tree[node] = val;
        } else {
            int mid = (start + end) / 2;
            if (idx <= mid) {
                update(2*node, start, mid, idx, val);
            } else {
                update(2*node+1, mid+1, end, idx, val);
            }
            tree[node] = tree[2*node] + tree[2*node+1];
        }
    }
    
    int query(int node, int start, int end, int l, int r) {
        if (r < start || end < l) return 0;
        if (l <= start && end <= r) return tree[node];
        int mid = (start + end) / 2;
        return query(2*node, start, mid, l, r) + 
               query(2*node+1, mid+1, end, l, r);
    }
    
public:
    SegmentTree(vector<int>& arr) {
        n = arr.size();
        tree.resize(4 * n);
        build(arr, 1, 0, n-1);
    }
    
    void update(int idx, int val) {
        update(1, 0, n-1, idx, val);
    }
    
    int query(int l, int r) {
        return query(1, 0, n-1, l, r);
    }
};
```

### Fenwick Tree (Binary Indexed Tree)

```cpp
class FenwickTree {
    vector<int> tree;
    int n;
    
public:
    FenwickTree(int n) : n(n), tree(n + 1, 0) {}
    
    void update(int i, int delta) {
        for (++i; i <= n; i += i & (-i)) {
            tree[i] += delta;
        }
    }
    
    int query(int i) {
        int sum = 0;
        for (++i; i > 0; i -= i & (-i)) {
            sum += tree[i];
        }
        return sum;
    }
    
    int rangeQuery(int l, int r) {
        return query(r) - (l > 0 ? query(l - 1) : 0);
    }
};
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

```cpp
// Common bit operations
x & 1           // Check if odd
x >> 1          // Divide by 2
x << 1          // Multiply by 2
x & (x - 1)     // Remove rightmost set bit
x | (x + 1)     // Set rightmost unset bit
__builtin_popcount(x)  // Count set bits
__builtin_clz(x)       // Count leading zeros
```

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
- **Codeforces**: Competitive programming (C++ preferred)
- **HackerRank**: Practice problems
- **InterviewBit**: Structured learning path
- **GeeksforGeeks**: Theory and problems

### Books
- **Cracking the Coding Interview**: Problem-solving approach
- **Elements of Programming Interviews (C++ Edition)**: Comprehensive guide
- **Algorithm Design Manual**: Deep understanding
- **Competitive Programming 3**: Advanced techniques

### YouTube Channels
- **NeetCode**: Pattern-based explanations
- **Back To Back SWE**: Detailed problem walkthroughs
- **Errichto**: Competitive programming
- **William Fiset**: Data structures & algorithms

### Practice Lists
- **Blind 75**: Must-solve problems
- **Grind 75**: Updated version of Blind 75
- **NeetCode 150**: Pattern-based problem list

### C++ Resources
- **cppreference.com**: Complete C++ reference
- **C++ STL Documentation**: Container and algorithm reference
- **Effective Modern C++**: Best practices

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

### C++ Specific Tips

1. **Use STL**: Master `vector`, `unordered_map`, `priority_queue`
2. **Know Complexity**: Understand STL container complexities
3. **Avoid TLE**: Use `ios_base::sync_with_stdio(false)`
4. **Use References**: Pass large objects by reference
5. **Lambda Functions**: Use for custom comparators

### Remember

> "The goal is not to solve every problem, but to recognize patterns and apply the right algorithm efficiently."

Good luck with your preparation! 🚀

---

**Last Updated**: 2024
**Total Problems Listed**: 150+
**Difficulty Levels**: Basic, Medium, Hard, Very Hard
**Languages**: C++

