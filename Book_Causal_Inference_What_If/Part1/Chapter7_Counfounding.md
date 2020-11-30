## Counfounding
Basic sturcture: A->Y, L->A, L->Y （7.1）
- We refer to the bias caused by shared causes of treatment and outcome as confounding, it is due to the presence of a cause (L or U) that is shared by the treatment A and the outcome Y , which results in an open backdoor path between A and Y.

Counfounding by indication or channeling: A->Y, L->A, U->L, U->Y （7.2）
- Both L and Y are caused by an unmeasured variable U.

Reverse causation when L is unkown: A->Y, L->Y, U->L, U->Y （7.3）



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

## 7.3 Confouding and backdoor criterion
(7.4) A->Y, U1->L, U2->L, U1->Y, U2->A

In 7.1-7.3, L is a confounder because the causal effect can be identified by the standardized risk. In 7.2 and 7.3, L is not a common cause of A adn Y, yet we still say that L is a coufounder because it's needed to block the open backdoor path attribute to the unmeasured common cause U of A and Y.

BUT, in 7.4, L is not a counfounder and the causal effect can be identified via conditional mean. This is the first example we have seen for which unconditional exchangeability holds but conditional exchangeability does not: the average causal effect is identified, but generally not the conditional causal effects within levels of L. '

(7.5) L->A->Y, U1->L, U1->Y, U2->L, U2->A

The presence of the arrow creates an open backdoor path A<-l-<U1->Y because U1 is the common cause of A and Y, and so confounding exists. So There is neither unconditional exchangeability nor conditional exchangeability given L.

```
Conditioning on L would block that backdoor path but would simultaneously open a backdoor path on which L is a collider, which is called selection bias rather than counfounding. 
```

(7.6) L->A->Y, U1->L, U1->L1->Y, U2->L, L2->L2->A
A solution to the bias in 7.5 would be to measure either (1) A vairable L1 between U1 and either A or Y or (2) A vairable L1 between U1 and either A or Y. In the first case we would have conditional exchangeability given L1. In the second case we would have conditional exchangeability given both L2 and L.

## 7.4 Counfounding and confounders
The traditional approach misleads investigators into adjusting for variables when adjustment is harmful. In contrast, a structural approach starts by explicitly identifying the sources of confounding and then identifies a sufficient set of adjustment variables.

A structural approach to confounding emphasizes that causal inference from observational data requires a priori causal knowledge. Of course, there is no guarantee that the researchers’ causal DAG is correct and thus it is possible that, contrary to the researchers’ beliefs, their chosen set of adjustment variables fails to eliminate confounding or introduces selection bias. However, the structural approach to confounding has two important advantages.
- First, it prevents inconsistencies between beliefs and actions.
- Second, the researchers’ assumptions about confounding become explicit and therefore can be explicitly criticized by other investigators.


## 7.5 Single-world intervention graphs
Why we need SWIG:
There appears to be no obvious relationship between counterfactual independence and the absence of backdoor paths because counterfactuals are not included as variables on causal diagrams. Since graphs are so useful for evaluating independencies via d-separation, it seems natural to want to construct graphs that include counterfactuals as nodes, so that unconditional and conditional exchangeability can be directly read off the graph.

A SWIG is a graph that represents a counterfactual world created by **a single intervention**. In contrast, the variables on a standard causal diagram represent **the actual world**. On the SWIG,  <img src="https://render.githubusercontent.com/render/math?math=Y^{a=1}">is dseparated from A given L if and **only if** L is a non-descendant of A that blocks all backdoor paths from A to Y


![image](/img/swig_example.png)

## 7.6 Counfounding adjustment
In the absence of randomization, causal inference relies on the uncheckable assumption that we have measured a set of variables L that is a sufficient set for confounding adjustment, that is, a set of non-descendants of treatment A that includes enough variables to block all backdoor paths from A to Y . Under this assumption of conditional exchangeability given L, standardization and IP weighting can be used to compute the average causal effect in the population, BUT these methods are not the only ways. Methods that adjust for confounders L can be classified into two broad categories:
- G-methods: standardization, IP weighting, and g-estimation. These methods (the ‘g’ stands for ‘generalized.’) exploit conditional exchangeability given L to estimate the causal effect of A on Y **in the entire population or in any subset of the population**.
  - IP weighting achieves this by creating a pseudo-population in which treatment A is independent of the measured confounders L, that is, by “deleting” the arrow from L to A, which has obvious advantages when dealing with time-varing treatment, however stratification method may result in selection bias.
  - Stratification-based methods rather compute the conditional effect in a subset of the observed population, which is represented by adding a selection box. 
  - However, methods like difference in difference, instrumental variable estimation adn the front door criterion do not require conditional exchangeability, they require alternative assumptions that, like conditional exchangeability, are unvertifiable. Therefore, in practice, the validity of the resulting effect estimates is not guaranteed. Also, these methods cannot be generally employed for causal questions involving time-varying treatments. As a result, these methods are disqualified from consideration for many research problems.
- Stratification-based methods: Stratification (including restriction) and matching. These methods exploit conditional exchangeability given L to estimate the association between A and Y **in subsets defined by L**.

Note: Achieving conditional exchangeability may be an unrealistic goal in many observational studies but, as discussed in Section 3.2, expert knowledge about the causal structure can be used to get as close as possible to that goal. Therefore, in observational studies, investigators measure many variables L; (which are non-descendants of treatment) in an attempt to ensure that the treated and the untreated are conditionally exchangeable. The hope is that, even though common causes may exist (confounding), the measured variables L are sufficient to block all backdoor paths (no unmeasured confounding). However, there is no guarantee that this attempt will be successful, which makes causal inference from observational data a risky undertaking.To appropriately criticize study, the critic needs to engage in a truly scientific conversation.


