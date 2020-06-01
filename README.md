# BackTracking
## Begineers Guide
##### also for imtermediate
___
___
## Description of the method
* The __backtracking__ algorithm enumerates a set of partial candidates that, in principle, could be completed in various __ways to give all the possible solutions__ to the given problem. The completion is done incrementally, by a sequence of candidate extension steps.
___
* Conceptually, the partial candidates are represented as the _nodes of a tree structure_, the potential search tree. Each partial candidate is the parent of the candidates that differ from it by a single extension step; the leaves of the tree are the partial candidates that cannot be extended any further.
___
* The backtracking algorithm traverses this search tree _recursively_, from the _root down_, in _depth-first order_. At each node c, the algorithm checks whether c can be completed to a _valid solution_. If it cannot, the whole sub-tree rooted at c is __skipped (pruned)__. Otherwise, the algorithm (1) checks whether c itself is a valid solution, and if so reports it to the user; and (2) recursively enumerates all sub-trees of c. The two tests and the children of each node are defined by user-given procedures.
___
* Therefore, the actual search tree that is traversed by the algorithm is only a part of the potential tree. The total cost of the algorithm is the number of nodes of the actual tree times the cost of obtaining and processing each node. This fact should be considered when choosing the potential search tree and implementing the [pruning](https://en.wikipedia.org/wiki/Pruning "pruning wiki") test

# Pseudo code
In order to apply backtracking to a specific class of problems, one must provide the data P for the particular instance of the problem that is to be solved, and six procedural parameters, _root_, _reject_, _accept_, _first_, _next_, and _output_. These procedures should take the instance data P as a parameter and should do the following:
> c => partial candidate
> s => solution to partial candidate

1. `root(P)`: return the partial candidate at the root of the search tree.
1. `reject(P,c)`: return true only if the partial candidate c is not worth completing.
1. `accept(P,c)`: return true if c is a solution of P, and false otherwise.
1. `first(P,c)`: generate the first extension of candidate c.
1. `next(P,s)`: generate the next alternative extension of a candidate, after the extension s.
1. `output(P,c)`: use the solution c of P, as appropriate to the application.
The backtracking algorithm reduces the problem to the call `bt(root(P))`, where bt is the following recursive `function`:

>pseudo code is explained below
```python
  def bt(c): 
    if reject(P, c):#return True if  partial candidate is not worth completing
      return 
    if accept(P, c):#return  True if c is a solution
      output(P, c)#use the solution c of P, as appropriate to the application.
    s = first(P, c)#generate first first extension
    while s is not None:
      bt(s)
      s = next(P, s)#next alternative extension
```

# Usage considerations
> t => ancestor of __C__
* The __reject__ function should be a __boolean-valued__ function that returns `True` only if it is certain that no possible extension of _c_ is a valid solution for _P_. If the function cannot reach a definite conclusion, it should return `False`. An incorrect true result may cause the bt function to miss some valid solutions. The function may assume that `reject(P,t)` returned false for every ancestor _t_ of _c_ in the search tree.

* On the other hand, the efficiency of the backtracking algorithm depends on reject returning true for candidates that are as close to the root as possible. If reject always returns false, the algorithm will still find all solutions, but it will be equivalent to a brute-force search.

* The accept function should return true if _c_ is a complete and valid solution for the problem instance _P_, and false otherwise. It may assume that the partial candidate _c_ and all its ancestors in the tree have passed the reject test.

* The general pseudo-code above does not assume that the valid solutions are always leaves of the potential search tree. In other words, it admits the possibility that a valid solution for _P_ can be further extended to yield other valid solutions.

* The first and next functions are used by the backtracking algorithm to enumerate the children of a node _c_ of the tree, that is, the candidates that differ from _c_ by a single extension step. The call `first(P,c)` should yield the first child of _c_, in some order; and the call `next(P,s)` should return the next sibling of node _s_, in that order. Both functions should return a distinctive __"None"__ candidate, if the requested child does not exist.

* Together, the root, first, and next functions define the set of partial candidates and the potential search tree. They should be chosen so that every solution of _P_ occurs somewhere in the tree, and no partial candidate occurs more than once. Moreover, they should admit an efficient and effective reject predicate.

## Suduku Solver is the example problem for backtracking
![Example Question](https://upload.wikimedia.org/wikipedia/commons/8/8c/Sudoku_solved_by_bactracking.gif)

## Eight Queens Problem
![Example question](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d7/Chessboard480.svg/312px-Chessboard480.svg.png)