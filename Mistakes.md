# 1

n = int(input())
t = input().split()
print(hash(t))

->Error
TypeError: unhashable type: 'list'

->Solution
t = tuple(map(int, input().split()))
print(hash(t))


.split() creates a list by default. ✅
The problem is asking you to convert the input numbers into a tuple and print its hash value, because tuples are hashable but lists are not.










# 2

## 2.1
Tuple par remove() use kiya.
t = ('pen', 'pencil')
t.remove('pen')

->Error
AttributeError: 'tuple' object has no attribute 'remove'

->Solution
Take input from the user in the form of a comma-separated string
tup_input =list(map(str, input().split(",")))

Take the item to be removed from the tuple
item = input( )
tup_input.remove(item)

Your code starts below
tup_input = tuple(tup_input)
print(tup_input)


## 2.2
lst = ['pen', 'pencil']
lst.remove('marker')

->Error
ValueError: list.remove(x): x not in list

->Solution
if 'marker' in lst:
    lst.remove('marker')

Tuple is immutable → no remove(), append(), or pop().
Before using remove(x) on a list, ensure x exists in the list. ✅



# 3


lst_stage.append(i)
lst_stage.append(j)
lst_stage.append(k)

if sum(lst_stage) != n:
    lst.append(lst_stage)


->Error / Problem

I was reusing the same list object:
lst_stage = []
and repeatedly modifying it using:

append()
pop()
Then storing it in:

lst.append(lst_stage)
Why is this a problem?

Lists are mutable objects.

When we do:

lst.append(lst_stage)
Python stores a reference to lst_stage, not a separate copy.

->Solution
lst = []

for i in range(x + 1):
    for j in range(y + 1):
        for k in range(z + 1):

            if i + j + k != n:
                lst.append([i, j, k])

print(lst)

❌ Avoid reusing the same mutable list object with multiple append() and pop() operations.
Lists are mutable and stored by reference; when generating combinations, create a new list ([i, j, k]) instead of repeatedly modifying and storing the same list object. ✅





# 4

## Runner-Up Score (Duplicate Maximum)

->Error

```python
arr.remove(max_ele)
```

`remove()` deletes **only the first occurrence** of the value. If the maximum appears multiple times, one copy still remains in the list.

Example:

```python
arr = [2, 3, 6, 6, 5]

arr.remove(6)

print(arr)
```

Output:

```python
[2, 3, 6, 5]
```

The second `6` is still present, so searching for the maximum again returns `6` instead of the runner-up `5`.

---

->Solution

### Method 1

```python
while max_ele in arr:
    arr.remove(max_ele)

print(max(arr))
```

### Method 2 (Better)

```python
arr = list(set(arr))
arr.remove(max(arr))
print(max(arr))
```

---

->Summary

- `list.remove(value)` removes **only the first matching element**.
- Remove **all duplicate maximum values** before finding the runner-up.





# 5
## HackerRank - Nested Lists

### Problem

Store the name and score of each student in a nested list. Print the name(s) of the student(s) having the **second lowest score**. If multiple students have the same second lowest score, print their names in **alphabetical order**.

---

### My Approach

1. Store each student's data as `[name, score]`.
2. Find the lowest score.
3. Remove all students having the lowest score.
4. Find the new lowest score (second lowest).
5. Print all students having the second lowest score.

---

## Error 1: Removing Elements While Iterating

### Wrong

```python
for i in lst:
    if min_score == i[1]:
        lst.remove(i)
```

### Why?

When you remove an element while iterating over the same list, the remaining elements shift to the left. The iterator moves to the next index, causing some elements to be skipped.

Example:

```python
lst = [
    ["A", 10],
    ["B", 10],
    ["C", 20]
]
```

Iteration:

```
Remove A

List becomes

[B, C]

Iterator moves to next index

B is skipped
```

Result:

```python
["B", 10]
```

One minimum-score student is still left in the list.

### Correct

```python
lst = [i for i in lst if i[1] != min_score]
```

This creates a new list containing only the required elements.

---

### Error 2: Names Were Not Printed Alphabetically

### Wrong

```python
for i in lst:
    if i[1] == min_score:
        print(i[0])
```

This prints names in input order.

### Correct

```python
names = []

for i in lst:
    if i[1] == min_score:
        names.append(i[0])

names.sort()

for name in names:
    print(name)
```

---

### Learning

- Never modify a list while iterating over it.
- Use list comprehension to filter elements safely.
- When the question asks for alphabetical order, sort the names before printing.
- `list.sort()` modifies the original list.
- `sorted()` returns a new sorted list.

---

## Summary

- **Don't remove elements while iterating over the same list.**
- **Always sort the names before printing if alphabetical order is required.**




#  6

## Captain's Room (Sorting Approach)

## Error

```python
for i in range(length):
    if lst_room_numbers[i] == lst_room_numbers[i+1]:
        i += k
```

Changing the loop variable (`i += k`) inside a `for` loop **does not affect the next iteration**.

Python automatically assigns the next value from `range()`.

### Example

```python
for i in range(5):
    i += 2
    print(i)
```

Output:

```
2
3
4
5
6
```

The loop still iterates over `0, 1, 2, 3, 4`.

---

## Error

Checking only the next element is not enough.

```python
if lst_room_numbers[i] == lst_room_numbers[i+1]:
```

This only confirms two consecutive elements are equal.

To verify an entire group of size `k`, compare:

```python
lst_room_numbers[i] == lst_room_numbers[i + k - 1]
```

Since the list is sorted, if the first and last elements of the group are equal, all `k` elements belong to the same room.

---

## Solution

Use a `while` loop so the index can be updated manually.

```python
room_numbers.sort()

i = 0

while i < len(room_numbers):

    if i + k - 1 < len(room_numbers) and room_numbers[i] == room_numbers[i + k - 1]:
        i += k
    else:
        print(room_numbers[i])
        break
```

---

## Better Solution (Mathematical)

```python
captain_room = (k * sum(set(rooms)) - sum(rooms)) // (k - 1)

print(captain_room)
```

This works because every family room appears exactly `k` times, while the Captain's room appears only once.

---

## Summary

- Changing the loop variable inside a `for` loop does **not** change the loop sequence.
- Use a `while` loop when you need manual index control.
- After sorting, compare the first and `(k-1)`th element to validate an entire group.
- The mathematical (`set`) solution is the shortest and most efficient approach.











#  7

## Set Mutations (HackerRank)

## Problem

Given a set `A` and multiple operations (`update`, `intersection_update`, `difference_update`, `symmetric_difference_update`), perform each mutation on `A` and print the sum of the final set.

---

## My Approach

```python
lst = []

for i in range(iteration):
    task_i, n_i = input().split()
    set_i = set(input().split())
    lst.append(task_i)

for i in range(iteration):

    if lst[i] == "update":
        A.update(set_i)
```

---

## Error 1

Only the operation names were stored.

```python
lst.append(task_i)
```

The corresponding sets were **not stored**.

During the second loop, `set_i` refers only to the **last input set**, so every operation is performed on the same set.

### Example

Input

```text
update
{1,2}

difference_update
{5,6}
```

After reading all input,

```python
set_i = {5,6}
```

Now both operations use `{5,6}`, which is incorrect.

---

## Error 2

Elements were stored as strings.

```python
A = set(input().split())
```

Output becomes

```python
{'1', '2', '3'}
```

Instead of

```python
{1, 2, 3}
```

Therefore,

```python
sum(A)
```

raises

```text
TypeError
```

### Solution

Convert every input element into an integer.

```python
A = set(map(int, input().split()))

other_set = set(map(int, input().split()))
```

---

## Better Approach

Perform the mutation immediately after reading the input.

```python
for _ in range(iteration):

    operation, size = input().split()

    other_set = set(map(int, input().split()))

    if operation == "update":
        A.update(other_set)

    elif operation == "intersection_update":
        A.intersection_update(other_set)

    elif operation == "difference_update":
        A.difference_update(other_set)

    elif operation == "symmetric_difference_update":
        A.symmetric_difference_update(other_set)
```

No extra list is required.

---

## Python Shortcut (getattr)

Instead of multiple `if-elif` statements, Python can dynamically call a method.

```python
getattr(A, operation)(other_set)
```

Example

```python
operation = "update"

getattr(A, operation)(other_set)
```

Equivalent to

```python
A.update(other_set)
```

If

```python
operation = "difference_update"
```

Then

```python
getattr(A, operation)(other_set)
```

Equivalent to

```python
A.difference_update(other_set)
```

---

## What is getattr()?

### Definition

`getattr()` is a built-in Python function that retrieves an attribute or method of an object dynamically using its name as a string.

### Syntax

```python
getattr(object, attribute_name)
```

or

```python
getattr(object, attribute_name, default)
```

---

## Learning

- Mutation methods modify the original set.
- Read the operation and execute it immediately.
- Do not reuse the last input set for every operation.
- Use `map(int, ...)` when numeric operations like `sum()` are required.
- `getattr()` is useful when the method name is available as a string.

---

## Time Complexity

Let:

- `N` = size of set `A`
- `M` = total elements processed across all other sets

Overall Time Complexity:

```text
O(M)
```

Each mutation operation is approximately linear in the size of the other set.

Space Complexity:

```text
O(N)
```

---

## Summary

- Every mutation operation has its own corresponding set.
- Execute the operation immediately after reading its input.
- Store integers, not strings.
- `getattr()` can replace long `if-elif` chains when method names are provided dynamically.
