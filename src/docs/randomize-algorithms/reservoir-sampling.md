# Reservoir sampling

> Reservoir sampling is a family of [randomized algorithms](README.md) for choosing a simple random sample, without replacement, of `k` items from a population of unknown size `n` in a single pass over the items. The size of the population `n` is not known to the algorithm and is typically too large for all `n` items to fit into main memory. The population is revealed to the algorithm over time, and the algorithm cannot look back at previous items. At any point, the current state of the algorithm must permit extraction of a simple random sample without replacement of size `k` over the part of the population seen so far. -- [wikipedia](https://en.wikipedia.org/wiki/Reservoir_sampling)


## 1. Random pick : 

**Problem Statement** : Given a very big array(or stream) of positive integers `stream`. Randomly pick an element from `stream`. Probability of picking any integer should be equal.

This is an extension of random pick problem that we have discussed in [random picks : init](random-picks-init.md). Please refer to that first for better understanding. Generally we cannot use the solution we used in [random picks : init](random-picks-init.md), either because array is too big to fit into main memory or integers are available to us in streaming fashion so we don't know the size of the array.

These kind of problems could be solved using reservoir sampling technique. Idea is similar to [Fisher–Yates shuffle](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle) algorithm. 

Algorithm : 
- Initialize random pick `random_pick = None`
- Element by element traverse the `stream` and generate random integer `r` from `[0,i]` where `i` is index of current element of stream. 
- If `r==0` then pick current element as our random pick.

For proof refer to [this](https://www.cs.rice.edu/~as143/COMP441_Spring17/scribe/lect2.pdf) article.

```python
def randomPick(stream):
    random_pick = None
    i = 0
    while stream:
        element = stream.popleft()
        r = randint(0,i)
        if r == 0:
            random_pick = element
    return random_pick
```

For various other advance implementations please refer to [wikipedia page](https://en.wikipedia.org/wiki/Reservoir_sampling).

## 2. Random pick index:

**Problem Statement** : Given an array(or stream) of integers `stream` with possible duplicates, randomly output the index(or position in stream) `i` of a given target integer `t`.

This could be solved in same was as we solved above problem, using reservoir sampling. In above example whole array(or stream) was our universe and we need to pick randomly from whole array(or stream), but here we only need to pick randomly from indices where our target `t` is occuring and we can ignore all other elements.

```python
def randomPickIndex(stream, t):
    random_pick_index = -1
    i = 0
    target_count = 0
    while stream:
        element = stream.popleft()
        if element==t:
            target_count +=1
            r = randint(0, target_count-1)
            if r == 0:
                random_pick_index = i
        i+=1
    return random_pick_index
```

**Practice link** : [[leetcode] Random Pick Index](https://leetcode.com/problems/random-pick-index/)


## 3. Random pick index of max:

**Problem Statement** : Given an array(or stream) of integers `stream` with possible duplicates, randomly output the index(or position in stream) `i` of the max values seen so far in `stream`.

Consider `stream = [11, 30, 2, 30, 30, 30, 6, 2, 62, 62]`, then one of the many possible valid output is `[0, 1, 1, 1, 4, 3, 5, 1, 8, 9]`. 
- Having iterated up to the index 2 (where the first `2` is), randomly give an index among `[1]` which are indices of `30` - the max value by far. Each index should have a `1/1` chance to get picked.
- Having iterated up to the index 5 (where the last `30` is), randomly give an index among `[1, 3, 4, 5]` which are indices of `30` - the max value by far. Each index should have a `1/4` chance to get picked.
- Having iterated through the entire array, randomly give an index among ``[8, 9]`` which are indices of `62` - the max value by far. Each index should have a `1/2` chance to get picked.

This could again be solved in same way we solved above random pick index. There we had fixed target `t`. Here our target changes as we see bigger then current max element. We make that element as our max element(or target) and continue same algorithm.

```python
def randomPickMaxIndex(stream):
    random_max_index_picks = []
    max_element = -sys.maxint-1 # same as target t
    max_index = -1 # same as random_pick_index
    max_count = 0 # same as target_count
    i = 0
    while stream:
        element = stream.popleft()
        if element > max_element:
            max_element = element
            max_index = -1
            max_count = 0
        if element == max_element:
            max_count +=1
            r = randint(0, max_count-1)
            if r==0:
                max_index = i
        i+=1
        random_max_index_picks.append(max_index)
    return random_max_index_picks
```


## 4. Random pick sample:

In the 1st example of this series we saw how to pick a random integer from a stream of integers using reservoir sampling. Same algorithm could be extended to pick `k` random samples from given stream of integers.

**Problem Statement** : Given a very big array(or stream) of positive integers `stream`. Randomly pick a sample of size `k` from given stream `stream`.

Algorithm : 
- Initialize random sample called `reservoir` of size `k` with first `k` elements of the stream.
- Element by element traverse rest of the `stream` and generate random integer `r` from `[0,i]` where `i` is index of current element of stream. 
- If `r<k` then replace `reservoir[r]` with `stream[i]`.

For proof refer to [this](https://www.cs.rice.edu/~as143/COMP441_Spring17/scribe/lect2.pdf) article.

```python
def randomPickSample(stream, k):
    reservoir = [0]*k
    i = 0
    while i<k:
        reservoir[i] = stream.popleft()
        i+=1
    while stream:
        element = stream.popleft()
        r = randint(0,i)
        if r < k:
            reservoir[r] = element
        i+=1
    return reservoir
```

For various other advance implementations please refer to [wikipedia page](https://en.wikipedia.org/wiki/Reservoir_sampling).

## Practice pool :

| #  | Practice link  |
|----|:--------------|
| 1  |  https://leetcode.com/problems/random-pick-index/ |
| 2  |  https://leetcode.com/problems/linked-list-random-node/  |
| 3  |  https://leetcode.com/discuss/interview-question/451431/facebook-onsite-generate-random-max-index |