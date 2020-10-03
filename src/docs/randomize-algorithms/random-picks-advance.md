# Random picks : advance

This topic contains optimization what we already discussed in [Random picks : init](random-picks-init.md). It's highly recommended to visit that topic first as we will build optimisization on top of those solutions.

## 1. Random pick with weights :

**Problem Statement** : Given two arrays of positive integers, `arr` and `weights`, each of size `n`, randomly pick an element from `arr` such that probablity of picking any element with index `i` is propotional to its weight (i.e. `weight[i]/sum(weights)`).

For eg with `arr = [1,2]` and `weights = [1,3]`, then `P(1)` should be `1/4` (i.e 25%) and `P(2)` should be `3/4` (i.e 75%) where `P(x)` is probablity of picking element `x`.

From previous discussion our solution was to extend `arr = [1,2]` to new `extended_arr=[1,2,2,2]` so that we can then forget about weights and just pick a uniformly random index. 
Inefficiency lies in the way we are extending our array.

- _Do we really need to extend array by adding elements multiple times?_ 
- _Can we represent it in some other form, so that this information is still preserved ?_

Turns out there is a way we can achieve this! 

|      index     | 0 | 1 | 2 | 3 |
|----------------|:-:|:-:|:-:|:-:|
|  extended_arr  | 1 | 2 | 2 | 2 |

Consider above `extended_arr`, here we are preserving every index. And when we generate random number `r` from index range `[0,3]` we say answer is `extended_arr[r]`. One thing to notice over here is, for any `arr[i]` it will be repeated **contiguously** for `weights[i]` times in our `extended_arr`. That's the catch ! If it's repeated **contiguously** then we can represent the repetition as range rather then individual incides. So if our `r` lies in range `[0,1)` we can say our answer is `arr[0]` and if `r` lies in range `[1,3)` then our answer is `arr[1]`, and so on. 

You can verify from below representation of `extended_arr` that these ranges are nothing but prefix sum of `weights` array (or you can think them as end indices of every repetition subarrays). And now, for randomly generated `r` we need to find `nextGreater(r)` in `extended_arr`. `nextGreater(r)` will give us the required index. This can be done using binary search in `log(n)` time if `n` is size of input `arr`. Awesome!

|      index     | 0 | 1 |
|----------------|:-:|:-:|
|       arr      | 1 | 2 |
|     weights    | 1 | 3 |
|  extended_arr  | 1 | 4 |

```python
def randomPickWithWeightV2(arr, weights):
    extended_arr = []
    prefix_sum = 0
    for i in range(len(arr)):
        prefix_sum += weights[i]
        extended_arr.append(prefix_sum)

    random_index = randint(0, extended_arr[-1]-1)
    random_index_in_range_mapping = nextGreater(random_index, extended_arr)
    return arr[random_index_in_range_mapping]

def nextGreater(x, arr):
    l = 0
    r = len(arr)-1
    idx = -1
    while l<=r:
        m = l + (r-l)/2
        if x < arr[m]:
            idx = m
            r = m-1
        else:
            l = m+1
    return idx
```

**Practice link** : [[leetcode] Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/)

## 2. Random pick with weights in 2D :

**Problem Statement** : Given a list of non-overlapping `rectangles` which are aligned to axis of the cartesian plane, randomly and uniformily pick an integer point in the space covered by these rectangles. Here `rectangles` is list of `(x1, y1, x2, y2)` tuples such that `(x1, y1)` is the integer coordinate of the bottom-left corner and `(x2, y2)` is the integer coordinate of the top-right corner.

Here also once we convert rectange representation to weights array representation as we discussed in [Random picks : init](random-picks-init.md), we can leverage above approach to efficiently generate uniformly random integer point.

```python
def randomPickWithWeightIn2D(rectangles):
    n = len(rectangles)
    # np[i] represents number of points for rectangles[i]
    np = [0]*n
    # representing i-th rectangle by index i
    rectangle_names = [0]*n
    for i in range(n):
        # calculating number of points
        x1, y1, x2, y2 = rectangles[i]
        np[i] = (x2-x1+1)*(y2-y1+1)
        # naming rectangle
        rectangle_names[i] = i
    
    picked_rectangle = randomPickWithWeightV2(rectangle_names, np)
    x1, y1, x2, y2 = rectangles[picked_rectangle]
    return (randint(x1,x2), randint(y1,y2))
```

**Practice link** : [[leetcode] Random Point in Non-overlapping Rectangles](https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/)


## Practice pool :

| #  | Practice link  |
|----|:--------------|
| 1  |  https://leetcode.com/problems/random-pick-with-weight |
| 2  |  https://leetcode.com/problems/random-point-in-non-overlapping-rectangles  |