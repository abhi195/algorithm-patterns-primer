# Algorithm Patterns Primer


> "Fret not, for there is **rhyme & reason** to this madness!" -- [Patterns in Algorithm Design](https://levelup.gitconnected.com/patterns-in-algorithm-design-17b327167c5e)

An organised list of algorithmic problems categorised by similarities or patterns in their solutions.

## Why ?

Consider this timeline in life of an adventurous programmer :

- **Day 0** : On this fine day you were feeling adventurous and decided to learn Dynamic Programming. Your started with theory, learned recursion, optimal substructure property, etc, etc...
- **Day 1** : You decided Knapsack is good place to start solving dynamic programming questions, so you learned 0/1 Knapsack.
- **Day 2** : You learned 0/1 Unbounded Knapsack.
- **Day 10** : You stumbled upon Rod Cutting problem. At first you weren't able to solve it. Thats totally okay on Day 10! But after seeing the solution you were able to reason with it. Great! Catching on.
- **Day 28** : After 30 days of learning DP, now you feel like you are ready to take a long contest on Codechef. You came across [Chef and Wedding Arrangements](https://www.codechef.com/problems/CHEFWED) problem. But you weren't able to solve it. :-(
- **Day 29** : After reading editorial you came to know that it was clever little variation of Rod Cutting problem that (you thought!) you have already mastered on Day 10. 
- **Day 30** : You decided to revisit Rod Cutting problem and suddenly realized that Rod Cutting problem is itself a variation of 0/1 Knapsack. Whattttttttt ? Everything is linking back to Day 1!

At this point you should have an epiphany and you should give a second thought on your whole learning framework.

In my experience while learning some hard topics such as Dynamic Programming it could be really frustrating to tackle them individually without understanding patterns. Versus if you picked a base problem and tried to tackle related problem as variations of the previously solved problems, it could really help you to grasp the concept. And in future you would be easily able to figure out if any new problem is variation of what you have already solved.

So this repository contains a curated list of patterns that either I observed myself or learned through some awesome article or youtube channels. I will try to link all original sources with each topics or lists.

## Structure :

For every topic or pattern list, I will try to follow below structure :

- Base problem.
    - First problem will be the base problem.
    - I'll either try to explain the base problem or link to the best possbile explanation of the base problem.
- Then one by one we will try to go through related problems and see how can they be solved as variation of a base or an intermediate problem.
    - Treat solution as sudo code, it might not be fully working piece of code.
- Trade-offs : There will be some cases where there are trade-offs between space and time complexities. I'll also try to link or explain trade-offs which might or might not conform to current pattern.
- Optimal Outlier : There will be some cases where a solution conforming to the current pattern is a valid solution, but there exists an another solution which is outlier to the current pattern and is optimal. Either you will need to use another pattern or some other concept. Whenever it's the case, I'll try to mention this as well.
- Practice Pool : Practice link for discussed problems as well as I'll try to maintain a growing list of problems that are similar to the pattern, where you can test your learnings.

## Table of contents :

- [Randomize Algorithms](src/docs/randomize-algorithms/README.md) : 
    - [Random Picks : init](src/docs/randomize-algorithms/random-picks-init.md)
    - [Random Picks : advance](src/docs/randomize-algorithms/random-picks-advance.md)
    - [Reservoir Sampling](src/docs/randomize-algorithms/reservoir-sampling.md)

## Upcoming :

- Array :
    - Range Addition Queries
    - Boyer Moore Voting
    - Sliding Window/Two Pointers
- Binary Search
- Trees
- Graphs :
    - Topological Sort
- Disjoint Union Set
- Dynamic Programming:
    - 101:
        - Kadane
        - Prefix & Suffix Sum Patterns
    - Knapsack
        - 0/1 Bounded
        - 0/1 Unbounded
    - Longest Common Subsequence
    - Matrix Chain Multiplication
    - Stock Span

## Awesome online content :

List of some awesome online content to learn theory, base concepts, algorithms, data structures or explanations to well known problems : 

- [cp-algorithms](https://cp-algorithms.com/)
- [geeksforgeeks](https://www.geeksforgeeks.org/)
- [Aditya Verma](https://www.youtube.com/channel/UC5WO7o71wvxMxEtLRkPhiQQ)
- [Tushar Roy - Coding Made Simple](https://www.youtube.com/channel/UCZLJf_R2sWyUtXSKiKlyvAw)

## Contribution guidelines :

- While contributing new pattern list, if possible please stick to the mentioned [structure](#structure-). Include it in [Table of contents](#table-of-contents-).
- Fell free to raise a patch for updates in any existing pattern explanations as well.
- You can add/update practice links or Similarity Practice Pool with problem links from any practice platform (hackerrank, codeforces, leetcode, etc) where we can submit a solution and there'a a online judge to review the solution.
