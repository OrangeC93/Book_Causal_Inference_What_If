## Definition of effect modification
A null average causal effect in the population does not imply a null average causal effect in a particular subset of the population. Let consider another situation: What is the average causal effect of A on Y in women(V=1)? And in men(V=2)?

- Additive effect modification: <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1}-Y^{a=0}|V=1] \neq E[Y^{a=1}-Y^{a=0}|V=0]">
- Multiplicative effect modification: <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1}|V=1]/E[Y^{a=0}|V=1] \neq E[Y^{a=1}|V=0]/E[Y^{a=0}|V=0]">

There is **qualitative effect** modification because the average causal effects in the subsets  V = 1 and V = 0 are in the opposite direction.


## 4.2 Stratification to identify effect modification
Stratification: the causal effect of A on Y is computed in each stratum of V . For dichotomous V , the stratified causal risk differences are:
<img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1} = 1|V=1] - Pr[Y^{a=0} = 1|V=1]"> or <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1} = 1|V=0] - Pr[Y^{a=0} = 1|V=0]">

The procedure the compute the conditional risk in each stratum v has two stages: 
  1. stratification by V 
  2. standardization by L or IP weighting with weights depending on L, Step 2 can be ignored when V is equal to the varaibles L that needed for conditional exchangeability.

Example: What is the average causal effect of A on Y in Greek(V=1)? And in Roman(V=2) where L represents the condition? 
- We have shown that, in our study population, nationality V modifies the effect of heart transplant A on the risk of death Y . 
- If one would then find effect modification by nationality. An intervention to improve the quality of heart surgery in Rome could eliminate the modification of the causal effect by passport-defined nationality. Whenever we want to emphasize this distinction, we will refer to nationality as a **surrogate effect modifier**, and to quality of care as a **causal effect modifier**. 
- However, our use of the term effect modification by V does not necessarily imply that V plays a causal role in the modification of the effect.

## 4.3 Why care about effect modification
1. The average causal effect in a population depends on the distribution of individual causal effects in the population. There is generally no such a thing as “the average causal effect of treatment A on outcome Y (period)”, but “the average causal effect of treatment A on outcome Y in a population with a particular mix of causal effect modifiers.”

```
The extrapolation of causal effects computed in one population to a second population is referred to as transportability of causal inferences across populaitions.
```

2. Identify the groups of individuals that would benefit most from an intervention.
3. Help understand the biological, social or other mechanisms leading to the outcome.

## 4.4 Stratification as a form of adjustment
But stratification is not always used to identify effect modification by V . In practice stratification is often used as an alternative to standardization (and IP weighting) to adjust for L. Calculate the risk ratios 
<img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|A=1, L=l] / Pr[Y=1|A=0, L=l]"> for both l = 0 and l = 1 (Under conditional exchagebility given L, the risk ratio in the subset L=l measures the average causal effect in the subste L=l), which are called *conditinal effect measure*

Note: Each of them quantifies the average causal effect in a nonoverlapping subset of the population but, in general, none of them quantifies the average causal effect in the entire population. Therefore, we did not consider stratification when describing methods to compute the average causal effect of treatment in the population in Chapter 2. Rather, we focused on standardization and IP weighting.

 
## 4.5 Matching as another form of adjustment
Matching is another adjustment method. The goal of matching is to construct a subset of the population in which the variables L have the same distribution in both the treated and the untreated.
- Often one chooses the group with fewer individuals (the untreated in our example) and uses the other group (the treated in our example) to find their matches.
- Also, matching needs not be one-to-one (matching pairs), but it can be one-to-many (matching sets).

## 4.6 Effect modification and adjustment methods
- Compute marginal or conditional effect: standardization and IP weighting
- Compute conditional effects in certain subsets of population: Stratification/restriction and Matching

All four approaches require exchangeability and positivity but the subsets of the population in which these conditions need to hold depend on the causal effect of interest.
