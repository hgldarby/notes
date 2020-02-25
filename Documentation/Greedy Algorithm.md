# Greedy Algorithm

### Description

- An algorithm that follows the problem solving heuristic of making the locally optimum choice at each stage with the intent of finding a global optimum.
- In many problems this does not usually produce an optimal solution, but nonetheless a greedy heuristic may yield locally optimal solutions that approximate a globally optimal solution in a reasonable amount of time.

### Example

- The example below shows the greedy algorithm working through a tree
- The key is to find the path that creates the largest number where each step is an addition.

![Image result for greedy algorithm example](https://d18l82el6cdm1i.cloudfront.net/uploads/EKKlGLuUQd-greedy-search-path.gif)

- The first step chooses 12 as 12 > 3
- Step 2: choose 6 as 6 > 5
- Step 3: choose 9 as 9 > 2
- This is the optimal route chosen by the greedy algorithm
- The actual optimal would be 7 - 3 - 1 - 99