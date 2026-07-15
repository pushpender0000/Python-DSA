#1

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










#2
