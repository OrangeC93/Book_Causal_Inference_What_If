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

## 6.3 Causal diagrams and conditional independence
Case1: Aspirin A affects the risk of heart disease Y because it reduces platelet aggregation B.
- A->[B]->Y
- Even though A and Y are marginally associated, A and Y are conditionally independent (unassociated) given B because the risk of heart disease is the same in the treated and the untreated within levels of B

Case2: Suppose the investigator restricts the study to nonsmokers (L = 1)
- [L]->A and [L]->Y
- Even though A and Y are marginally associated, A and Y are conditionally independent given L because the risk of lung cancer is the same in the treated and the untreated within levels of L:

Case3: Suppose that the investigators, who are interested in estimating the effect of haplotype A on smoking status Y , restricted the study population to individuals with heart disease (L = 1).
- A->[L] and Y->[L]
- A and Y are inversely associated conditionally on L = 1.

Case4: A->L, Y->L, L->[C]
- A and Y are also associated within levels of C because C is a common effect of A and Y
