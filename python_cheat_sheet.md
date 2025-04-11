# Python Crash Course (LeetCode-Style)

A concise refresher on essential Python structures, APIs, and patterns commonly used in coding interviews.

---

## 1. Lists

**Creation and Basic Methods**:

```python
lst = [1, 2, 3]
lst.append(4)         # [1, 2, 3, 4]
lst.extend([5, 6])    # [1, 2, 3, 4, 5, 6]
lst.insert(2, 99)     # insert 99 at index 2
lst.pop()             # pops from end
lst.pop(1)            # pop item at index 1
lst.remove(3)         # removes first occurrence of 3
lst.index(99)         # returns index of first occurrence
lst.count(2)          # count occurrences of 2
```

**Slicing**:

```python
sub_list = lst[1:4]      # from index 1 to 3
sub_list = lst[::2]      # step by 2
sub_list = lst[::-1]     # reversed copy
```

**List Comprehension**:

```python
squares = [x*x for x in range(5)]                # [0, 1, 4, 9, 16]
evens   = [x for x in lst if x % 2 == 0]
```

## 2. Dictionaries

**Creation and Access**:

```python
d = {"a": 1, "b": 2}
val = d["a"]              # 1
val = d.get("c", 0)       # returns 0 if "c" not found
d["c"] = 3                # add or overwrite
del d["a"]                # remove key 'a'
```

**Iteration**:

```python
for key in d:
    print(key, d[key])

for key, value in d.items():
    print(key, value)

for val in d.values():
    print(val)
```

## 3. Sets

**Usage**:

```python
s = {1, 2, 3}
s.add(4)
s.remove(2)   # KeyError if 2 not in set
s.discard(2)  # no error if 2 not found
if 3 in s:
    ...
s2 = set([2, 3, 5])
s.union(s2)         # s | s2
s.intersection(s2)  # s & s2
s.difference(s2)    # s - s2
```

## 3. Sorting

**In-Place vs Returned**:

```python
arr = [3, 1, 2]
arr.sort()                 # modifies arr in place
sorted_arr = sorted(arr)   # returns new list
```

**Custom Sorting**:

```python
arr.sort(reverse=True)
arr.sort(key=lambda x: x[1])  # if arr is a list of tuples
```

## 4. Strings

**Basic Operations**:

```python
s = "hello"
s.upper()              # "HELLO"
s.lower()              # "hello"
s.strip()              # removes whitespace from both ends
s.split(",")           # splits string into list
",".join(["a", "b"])   # joins list into string with delimiter
```

**F-Strings and Formatting**:

```python
name = "Alice"
age = 25
# f-strings (Python 3.6+)
print(f"Name: {name}, Age: {age}")
print(f"Math: {2 * 3}")
# format method
print("Name: {}, Age: {}".format(name, age))
```

## 5. Collections Module

**Counter**:

```python
from collections import Counter
cnt = Counter([1, 2, 2, 3, 3, 3])  # Counter({3: 3, 2: 2, 1: 1})
cnt[3]                              # 3 (count of element 3)
cnt.most_common(2)                  # [(3, 3), (2, 2)]
```

**defaultdict**:

```python
from collections import defaultdict
d = defaultdict(list)     # default value is empty list
d['a'].append(1)         # no KeyError if 'a' doesn't exist
d = defaultdict(int)      # default value is 0
```

## 6. Queue and Deque

**Queue (FIFO)**:

```python
from collections import deque
q = deque()
q.append(1)           # add to right
q.appendleft(2)       # add to left
q.pop()              # remove from right
q.popleft()          # remove from left
q.extend([3, 4])     # extend on right
q.extendleft([5, 6]) # extend on left
```

## 7. Named Tuples

```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(11, y=22)
print(p.x, p.y)      # 11 22
x, y = p             # unpacking
```

## 8. Heaps (Priority Queues)

```python
import heapq

# Min heap operations
nums = [3, 1, 4, 1, 5]
heapq.heapify(nums)               # convert list to heap in-place
heapq.heappush(nums, 2)           # push new element
smallest = heapq.heappop(nums)    # pop smallest element
smallest = nums[0]                # peek at smallest element

# For max heap, negate the values
nums = [3, 1, 4, 1, 5]
nums = [-x for x in nums]         # negate all values
heapq.heapify(nums)
largest = -heapq.heappop(nums)    # pop largest element

# K largest elements
k_largest = heapq.nlargest(3, nums)
k_smallest = heapq.nsmallest(3, nums)
```

## 9. Additional Tips

**Infinity in Python**:

```python
float('inf')   # positive infinity
float('-inf')  # negative infinity
```

**List/Dict/Set Comprehension with Multiple Conditions**:

```python
# List comprehension with if-else
[x if x > 0 else 0 for x in nums]

# Multiple if conditions
[x for x in nums if x > 0 and x % 2 == 0]

# Dict comprehension
{x: x**2 for x in range(5)}

# Set comprehension
{x**2 for x in range(5)}
```

**Enumerate**:

```python
for i, val in enumerate(lst):        # start from 0
    print(f"Index {i}: {val}")

for i, val in enumerate(lst, 1):     # start from 1
    print(f"Index {i}: {val}")
```
