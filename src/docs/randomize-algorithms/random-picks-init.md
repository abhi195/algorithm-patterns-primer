# Random picks : init

## 1. Random pick :

**Problem Statement** : Given an array of positive integers `arr` of size `n`, randomly pick an element from `arr` such that probablity of picking any element is `1/n`.

This is pretty straight forward ! Just randomly pick an index `i` from `0...n` and return `arr[i]`.

```python
def randomPick(arr):
    n = len(arr)
    return arr[randint(0,n-1)]
```

**Trade-offs** : 
- What if we cannot fit whole input array in memory ?
- What if we don't have access to whole input array, but rather we have stream of integers coming as input.

These trade-offs fall under category of random sampling and we will explore this in [reservoir sampling](reservoir-sampling.md)


## 2. Random pick with weights :

**Problem Statement** : Given two arrays of positive integers, `arr` and `weights`, each of size `n`, randomly pick an element from `arr` such that probablity of picking any element with index `i` is propotional to its weight (i.e. `weight[i]/sum(weights)`).

For eg with `arr = [1,2]` and `weights = [1,3]`, then `P(1)` should be `1/4` (i.e 25%) and `P(2)` should be `3/4` (i.e 75%) where `P(x)` is probablity of picking element `x`.

How can we convert this problem to equal probablity problem that we solved before ?

If we forget about `weights` for a moment then `P(1)` is `1/2` and `P(2)` is `1/2`. 
How can we extend `arr` to satisfy requried probablities ?

What if we extend `arr` such that our new `arr=[1,2,2,2]`. Now if we see, `P(1)` is `1/4` and `P(2)` is `3/4`. This is exactly what we wanted !

_You see the pattern ?_

Just extend the input array `arr` such that each element at index `i` is present `weight[i]` times and then we can just randomly pick an index `i` from this `extended_arr`.

```python
def randomPickWithWeight(arr, weights):
    extended_arr = []
    for i in range(len(arr)):
        extended_arr += [arr[i]]*weights[i]
    return randomPick(extended_arr)
```

**Practice link** : [[leetcode] Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/)

**Optimal Outlier** : This problem can be solved in more optimal way which we will discuss in [random picks : advance](random-pick-advance.md) section.

## 3. Random pick with weights in 2D :

**Problem Statement** : Given a list of non-overlapping `rectangles` which are aligned to axis of the cartesian plane, randomly and uniformily pick an integer point in the space covered by these rectangles. Here `rectangles` is list of `(x1, y1, x2, y2)` tuples such that `(x1, y1)` is the integer coordinate of the bottom-left corner and `(x2, y2)` is the integer coordinate of the top-right corner.

To solve this problem we should be asking below questions : 
- How do we pick a rectangle ?
    -  Out of given `n` rectangles, we cannot pick a rectangle uniformly randomly, because larger the rectangle, higher is the probability of picking an random integer point which is lying inside this rectangle.
    - So how do we quantify this largeness of a rectangle ? Area ? Yes, you are close !
    - More formally, we can quantify this largeness of rectangle by number of points lying inside this rectangle, including boundaries. So for a rectangle `(x1, y1, x2, y2)`, number of integer points `np = (x2-x1+1)*(y2-y1+1)`
    - Now probability of picking a rectangle `i` is propotional to the number of points `np` lying inside this rectangle (including boundaries).
    - This problem is now reduced to what we solved in above example with random element being a random rectangle and weight being the number of points `np` of that rectangle !
- How do we pick an uniformly random integer point inside a rectangle ?
    - This is just randomly and uniformly choosing `x` & `y` coordinate from given rectangle points.

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
    
    picked_rectangle = randomPickWithWeight(rectangle_names, np)
    x1, y1, x2, y2 = rectangles[picked_rectangle]
    return (randint(x1,x2), randint(y1,y2))
```

**Practice link** : [[leetcode] Random Point in Non-overlapping Rectangles](https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/)

**Optimal Outlier** : This problem can be solved in more optimal way which we will discuss in [random picks : advance](random-pick-advance.md) section.



## Practice pool :

| #  | Problem link  |
|----|:--------------|
| 1  |  https://leetcode.com/problems/random-pick-with-weight |
| 2  |  https://leetcode.com/problems/random-point-in-non-overlapping-rectangles  |