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
When exchangeability doesn't hold but conditional exchangeability does, as in a conditionally randomized experiment in which the probability of receivign treatment varies across values of L, the average causal effect can also be identified. Causal DAG allo w us to determine whether there exists a set of variables L for which conditional exchangeability holds, there're two mian approaches:
- The backdoor criterion applied to the causal DAG: A set of covariates L satisfies the backdoor criterion if all backdoor paths between A and Y are blocked by conditioning on L, and L contains no variables that are descendants of treatment A. Thus, by trying every subset of measured non-descendants of treatment, we can answer the question of whether conditional exchangeability holds for any subset.
```
Let us now relate the backdoor criterion (i.e., exchangeability) to confounding. The two settings in which the backdoor criterion is satisfied are 
1. No common causes of treatment and outcome. 
In Figure 6.2, there are no common causes of treatment and outcome, and hence no backdoor paths that need to be blocked. Then the set of variables that satisfies the backdoor criterion is the empty set and we say that there is no confounding. 
2. Common causes of treatment and outcome but a subset L of measured non-descendants of A suffices to block all backdoor paths. 
In Figure 7.1, the set of variables that satisfies the backdoor criterion is L. Thus, we say that there is confounding, but that there is no residual confounding whose elimination would require adjustment for unmeasured variables (which, of course, is not possible). For brevity, we say that there is no unmeasured confounding.

```


- The transformation of the causal DAG into a SWIG (section 7.5)



