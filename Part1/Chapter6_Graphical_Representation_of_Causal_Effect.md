## 6.1 Causal Diagrams
DAGs: directed acyclic graphs, directrd imply a direction, acyclic means there's no cycle that a vairable cannot cause itself, either directly or through another variable.
```
A defining property of causal DAGs is that, conditional on its direct causes, any variable on the DAG is independent of any other variable for which it is not a cause. This

```

## 6.2 Causal diagrams and marginal independence
- L->A, L->Y:  A and Y are accociated but not have a causal inference
- A->Y: A and Y are accociated and also has a causal inference
- A->L and Y->L: The common effect L is referred to as a collider because two arrowheads collide on this node, A and Y are not accociated and do not have a causal inference


In summary, two variables are (marginally) associated if one causes the other, or if they share common causes. Otherwise they will be (marginally) independent. 

## Causal diagrams and conditional independence
