## Counfounding
Basic sturcture: A->Y, L->A, L->Y
- We refer to the bias caused by shared causes of treatment and outcome as confounding, it is due to the presence of a cause (L or U) that is shared by the treatment A and the outcome Y , which results in an open backdoor path between A and Y.

Counfounding by indication or channeling: A->Y, L->A, U->L, U->Y
- Both L and Y are caused by an unmeasured variable U.

Reverse causation when L is unkown: A->Y, L->Y, U->L, U->Y



```
In a causal DAG, a backdoor path between treatment and outcome that remains even if all arrows pointing from treatment to other variables (the descendants of treatment) are removed. 
That is, the path has an arrow pointing into treatment.
```

## 7.2 Counfounding and exchangeability

