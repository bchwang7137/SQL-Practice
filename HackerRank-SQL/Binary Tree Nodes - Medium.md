# Binary Tree Nodes - Medium
[https://www.hackerrank.com/challenges/binary-search-tree-1/problem](https://www.hackerrank.com/challenges/binary-search-tree-1/problem)

You are given a table, _BST_, containing two columns: _N_ and _P,_ where _N_ represents the value of a node in _Binary Tree_, and _P_ is the parent of _N_.

![https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)

Write a query to find the node type of _Binary Tree_ ordered by the value of the node. Output one of the following for each node:

- _Root_: If node is root node.
- _Leaf_: If node is leaf node.
- _Inner_: If node is neither root nor leaf node.

```sql
SELECT n
     , CASE
        WHEN p IS NULL THEN 'Root'
        WHEN n IN (SELECT p FROM bst) THEN 'Inner'
        ELSE 'Leaf'
       END
FROM bst
ORDER BY n
;
```
