# Two Pointers Technique - Cheat Sheet

## When to Use Two Pointers: Keywords & Red Flags

### 1. **Sorted Data**
**Keywords in problem:**
- "sorted array" or "sorted list"
- "find two numbers..." 
- "find pairs with..."
- Input is already sorted

**Why:** Sorted data allows you to move pointers strategically (left pointer increases sum, right pointer decreases sum)

**Example Problems:**
- Two Sum in Sorted Array
- Container with Most Water
- Closest Two Sum
- Three Sum / N-Sum problems

---

### 2. **Find Pairs / Triplets / Subarrays**
**Keywords in problem:**
- "find a pair"
- "find two numbers"
- "find triplet" / "3Sum" / "4Sum"
- "find two elements"
- "check if exists"

**Why:** Instead of nested loops O(n²), two pointers give O(n) or O(n²) for N-sum problems

**Example Problems:**
- Two Sum II (sorted input)
- 3Sum
- 4Sum
- Remove Duplicates from Sorted Array
- Valid Triangle Count

---

### 3. **Palindrome or Symmetry Check**
**Keywords in problem:**
- "palindrome"
- "valid parentheses"
- "symmetric"
- "mirror"

**Why:** Compare from both ends moving inward naturally identifies mismatches

**Example Problems:**
- Valid Palindrome
- Valid Palindrome II (remove one character)
- Reverse a String
- Most Water Container

---

### 4. **Sliding Window / Subarray / Substring**
**Keywords in problem:**
- "longest substring"
- "smallest subarray"
- "maximum/minimum subarray"
- "window"
- "contiguous"
- "without repeating characters"

**Why:** Two pointers represent the window boundaries; expand/contract based on conditions

**Example Problems:**
- Longest Substring Without Repeating Characters
- Minimum Window Substring
- Longest Substring with At Most K Distinct Characters
- Sliding Window Maximum

---

### 5. **Move/Partition Elements**
**Keywords in problem:**
- "move all zeros to end"
- "partition"
- "sort colors" (0, 1, 2)
- "rearrange"
- "filter"
- "in-place"

**Why:** One pointer scans ahead, other writes valid elements; achieves O(1) space

**Example Problems:**
- Move Zeros to End
- Remove Duplicates from Sorted Array
- Sort Array by Parity
- Sort Colors (0, 1, 2)
- Dutch National Flag Problem

---

### 6. **Linked List Cycle / Middle / Traversal**
**Keywords in problem:**
- "cycle detection"
- "linked list"
- "middle of linked list"
- "nth node from end"
- "tortoise and hare"

**Why:** Use slow (1 step) and fast (2 steps) pointers; fast catches slow if cycle exists

**Example Problems:**
- Detect Cycle in Linked List
- Find Middle of Linked List
- Remove Nth Node From End
- Palindrome Linked List

---

### 7. **Merge / Compare Two Sequences**
**Keywords in problem:**
- "merge two arrays"
- "merge two lists"
- "intersection of arrays"
- "common elements"
- "compare two strings/lists"

**Why:** One pointer per array; advance based on comparison; achieves O(n) merge

**Example Problems:**
- Merge Sorted Array
- Intersection of Two Arrays
- Is Subsequence
- Shortest Distance Between Words

---

### 8. **Container / Capacity / Boundary Problems**
**Keywords in problem:**
- "maximum water"
- "maximum area"
- "capacity"
- "container"
- "trap"

**Why:** Start wide, move inward greedily; optimal strategy for spanning problems

**Example Problems:**
- Container with Most Water
- Trapping Rain Water (variant)
- Rain Water II

---

## Two Pointers Patterns

### Pattern 1: **Inward Traversal (Squeeze)**
Pointers start at **opposite ends** and move toward each other.

```
left = 0
right = len(arr) - 1
while left < right:
    # process pair
    # move based on condition
    if condition:
        left += 1
    else:
        right -= 1
```

**Use for:**
- Palindromes
- Two Sum in sorted array
- Container problems
- Symmetric checks

---

### Pattern 2: **Unidirectional / Sliding Window**
Both pointers start at the **same end** (usually beginning) and move forward.

```
left = 0
right = 0
# OR
left = 0
for right in range(len(arr)):
    # Expand window with right pointer
    # Shrink window with left pointer
```

**Use for:**
- Sliding window problems
- Remove duplicates / filter elements
- Partition arrays
- Subarray/substring problems

---

### Pattern 3: **Slow-Fast Pointers**
One pointer moves **1 step**, other moves **2 steps**.

```
slow = head
fast = head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
    if slow == fast:  # Cycle detected
        break
```

**Use for:**
- Cycle detection in linked lists
- Find middle of linked list
- Check for duplicates in array (Floyd's algorithm)

---

### Pattern 4: **Staged Traversal**
One pointer **scans** for a condition, second pointer **acts on** that condition.

```
read = 0  # scans input
write = 0  # writes output
for read in range(len(arr)):
    if condition(arr[read]):
        arr[write] = arr[read]
        write += 1
```

**Use for:**
- Move zeros to end
- Remove duplicates in-place
- Compact valid elements

---

## Quick Detection Checklist

Ask yourself these questions:

- [ ] Is the input **sorted** or can be sorted?
- [ ] Do I need to find **pairs/triplets/subarrays**?
- [ ] Can I avoid **nested loops** with two pointers?
- [ ] Is **in-place modification** required?
- [ ] Does the problem involve **moving/filtering/partitioning**?
- [ ] Am I looking for **symmetric/mirror** properties?
- [ ] Is there a **subarray/substring** requirement?
- [ ] Are there **boundary conditions** (starts/ends)?
- [ ] Can I achieve **O(n) time and O(1) space**?

**If 2+ answers are YES → Likely a Two Pointers problem**

---

## Time & Space Complexity

| Pattern | Time | Space | Notes |
|---------|------|-------|-------|
| Inward Traversal | O(n) | O(1) | After sorting: O(n log n) + O(n) = O(n log n) |
| Sliding Window | O(n) | O(1) | Each element visited at most twice |
| Slow-Fast | O(n) | O(1) | For linked lists |
| Unidirectional | O(n) | O(1) | In-place operations |
| N-Sum | O(n^(k-1)) | O(1) | 3Sum: O(n²), 4Sum: O(n³), etc. |

---

## Common Mistakes to Avoid

1. **Forgetting to sort** - Two pointers usually require sorted data first
2. **Infinite loops** - Ensure pointers always converge (left < right condition)
3. **Missing duplicate handling** - Skip duplicates after finding valid pairs
4. **Wrong pointer movement** - Move the pointer pointing to smaller value (in sum problems)
5. **Off-by-one errors** - Check boundary conditions carefully (left < right vs left <= right)
6. **Not handling edge cases** - Empty arrays, single elements, all same elements

---

## Example: Two Sum II (Most Common)

```python
def twoSum(numbers, target):
    left = 0
    right = len(numbers) - 1
    
    while left < right:
        total = numbers[left] + numbers[right]
        
        if total == target:
            return [left + 1, right + 1]  # 1-indexed
        elif total < target:
            left += 1  # Need larger sum
        else:
            right -= 1  # Need smaller sum
    
    return []
```

**Time:** O(n) | **Space:** O(1)

---

## Keywords to Spot Two Pointers Problems

| Category | Keywords |
|----------|----------|
| **Data Property** | sorted, ordered, sequence |
| **Find Operation** | find pair, find two, find triplet, exists, valid |
| **Optimization** | minimum, maximum, smallest, largest |
| **In-Place** | in-place, modify, rearrange, swap |
| **Boundaries** | start, end, boundary, symmetric, mirror |
| **Subarray/Substring** | contiguous, subarray, substring, window |
| **Linked List** | cycle, middle, node, traversal, tortoise |
| **Partition** | partition, move, remove, filter, eliminate |

---

## Practice Problems by Difficulty

### Easy
- Reverse String
- Valid Palindrome
- Two Sum II (Sorted Input)
- Move Zeros to End
- Remove Duplicates from Sorted Array

### Medium
- 3Sum
- Container with Most Water
- Longest Substring Without Repeating Characters
- Sort Colors
- Remove Duplicates II

### Hard
- 4Sum
- Trapping Rain Water
- Minimum Window Substring
- Shortest Distance Between Words
- Longest Substring with At Most K Distinct Characters

---

**Remember:** Two pointers is not about the pointers themselves, but about strategically exploring the data space to avoid redundant operations and achieve optimal time complexity.