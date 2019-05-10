Add your answers to the Algorithms exercises here.
## Exercise I

a) O(n)
```
a = 0
while (a < n * n * n):
    a = a + n * n
```
-As a will always be zero and will always be less than large n at first pass.
-a will then always increment by Kn^2; K being a constant equal to the n pass made
(So on the first pass n^2, second pass 2n^2, thrid pass 3n^2, etc)
-The function stops running when Kn^2 >= n^3
-Therefore the function ends when K = n or when the nth pass is made
-So the running time is n

b) O(n^3)
```
    sum = 0
    for i in range(n):
      i += 1
      for j in range(i + 1, n):
        j += 1
        for k in range(j + 1, n):
          k += 1
          for l in range(k + 1, 10 + k):
            l += 1
            sum += 1
```
sum = 0 => O(1)

for i in range(n): => O(n)
    -as i only depends on n and increments one at a time

i += 1 => O(1)

for j in range(i + 1, n): => O(n)
    -as j only depends on i and n and increments one at a time

j += 1 => O(1)

for k in range(j + 1, n): => O(n)
    -as k only depends on size of j and n and increments one at a time

k += 1  => O(1)

for l in range(k + 1, 10 + k): => O(1)
    -because no matter what l is this always runs 9 (10-1)
    -as 10+k is not inclusive
    -O(9) reduces to constant O(1)

l += 1 => O(1)

sum += 1 => O(1)

O(1+(n(1+n(1+n(1+1(1+1))))))
O(1+(n(1+n(1+n(1+2)))))
O(1+(n(1+n(1+3n))))
O(1+(n(1+n(3n))))
O(1+(n(1+3n^2)))
O(1+(n(3n^2)))
O(1+(3n^3))
O(3n^3)
O(n^3)


c) O(n)
```
    def bunnyEars(bunnies):
      if bunnies == 0:
        return 0

      return 2 + bunnyEars(bunnies-1)
```
-Will run one function for n
-Then re-call function for every decremnting integer value down to 0
-Which at that point will return 0 and stop function call
-O(n+1) => O(m)


## Exercise II
We can use a recursive binary search function to start at the middle floor and throw the egg. If the egg breaks we eliminate all floors that are above that floor and thus breaking our search in half. (Else if it doesn't break we elimate all floors below.) We can repeat this function with the new middle floor with the base floor being the last minimum floor used and our new max floor being what the last middle floor was. (Or if it didn't break the minimum floor being whata our last middle floor was and the max floor being that last max floor). We stop this process one the difference between the minimum floor and maximum floor is only 1 where the minimum floor is the higest you can throw an egg and the maximum floor is the breaking point.

-Initital max_floor being the _n_-story building or number of floors the building has

def breakingPoint(max_floor, min_floor=1):
    mid_floor = (max_floor + min_floor) // 2
    if max_floor - min_floor == 1:
        return max_floor
    if eggBreaks(mid_floor):
        return breakingPoint(mid_floor, min_floor)
    else:
        return breakingPoint(max_floor, mid_floor)

-where eggBreaks() would be some other function such as K is a given or random number where an egg breaks
def eggBreaks(floor):
    if floor >= K:
        return True
    else:
        return False