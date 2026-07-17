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

