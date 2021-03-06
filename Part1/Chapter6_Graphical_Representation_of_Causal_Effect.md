## 6.1 Causal Diagrams
DAGs: directed acyclic graphs, directrd imply a direction, acyclic means there's no cycle that a vairable cannot cause itself, either directly or through another variable.
```
A defining property of causal DAGs is that:
Conditional on its direct causes, any variable on the DAG is independent of any other variable for which it is not a cause. 

```

## 6.2 Causal diagrams and marginal independence
- A->Y: A and Y are accociated ✅ and has a causal inference✅
- Common cause: L->A, L->Y
  - A and Y are accociated ✅ but not have a causal inference ❌
- Common effect:A->L and Y->L
  - The common effect L is referred to as a collider because two arrowheads collide on this node, A and Y are not accociated ❌ and do not have a causal inference ❌, but if we conditioning on L, A and Y are associated (we'll talk about it later)

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


There is another possible source of association between two variables that we have not discussed yet: chance or random variability. Unlike the structural reasons for an association between two variables–causal effect of one on the other, shared common causes, conditioning on common effects–random variability results in chance associations that become smaller when the size of the study population increases.

## 6.4 Positivity and consistency in causal diagrams
```
Positivity is roughly translated into graph language as the condition that the arrows from the nodes L to the treatment node A are not deterministic.

The first component of consistency–well-defined interventions–means that the arrow from treatment A to outcome Y corresponds to a possibly hypothetical but relatively unambiguous intervention.
```
## 6.5 A structural classification of bias

- One source of bias is the lack of exchangeability between the treated and the untreated. <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1}=1] - Pr[Y^{a=0}=1] \neq Pr[Y=1|A=1] - Pr[Y=1|A=0]">, causes for generating the lcak of exchangeability:
  - Common causes: When the treatment and outcome share a common cause, the association measure generally differs from the effect measure. Many epidemiologists use the term **confounding** to refer to this bias.
  - Conditioning on common effects: This structure is the source of bias that many epidemiologists refer to as selection bias.

- Another source of bias: measurement error.

## 6.6 The structure of effect modification
Causal diagrams are **less helpful** to illustrate the concept of effect modification. Causal diagram in does not necessarily indicate the presence of effect modification by V.
- The causal effect of treatment A on mortality Y is in the same direction (i.e., harmful or beneficial) in both stratum V = 1 and stratum V = 0.
- The direction of the causal effect of treatment A on mortality Y in stratum V = 1 is the opposite of that in stratum V = 0 (i.e., there is qualitative effect modification).
- Treatment A has a causal effect on Y in one stratum of V but no causal effect in the other stratum, e.g., A only kills individuals with V = 0.

The variable s is a surrogate effect modifier whereas the variable V is a causal effect modifier. Surrogate effect modifiers can be associated with the causal effect modifier by structures including common causes, conditioning on common effects, or cause and effect(see examples in figure 6.13, 6.14, 6.15).
