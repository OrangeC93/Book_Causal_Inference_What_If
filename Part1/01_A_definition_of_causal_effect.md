## Individual causual effects
#### 1.1 Individual causal effects
Causal effect for individual i: <img src="https://render.githubusercontent.com/render/math?math=Y_{i}^{a=1} \neq Y_{i}^{a=0}">

Individual causal effects are defined as a contrast of the values of counterfactual outcomes, but only one of those outcomes is observed for each individual– the one corresponding to the treatment value actually experienced by the individual. All other counterfactual outcomes remain unobserved. Because of missing data, individual effects cannot be identified, that is, they cannot be expressed as a function of the observed data
#### 1.2 Average causal effects
Average causal effect in population: <img src="https://render.githubusercontent.com/render/math?math=E[Y_{i}^{a=1}] \neq E[Y_{i}^{a=0}]">

#### 1.3 Measures of causal effect
(1)Causal risk difference (2)Risk ratio (3)Odds ratio
![image](/img/measure_of_causal_effect.png)
```
Each effect measure may be used for different purposes. 
For example, imagine a large population in which 3 in a million individuals would develop the outcome if treated, and 1 in a million individuals would develop the outcome if untreated. The causal risk ratio is 3, and the causal risk difference is 0.000002. 
The causal risk ratio (multiplicative scale) is used to compute how many times treatment, relative to no treatment, increases the disease risk. The causal risk difference (additive scale) is used to compute the absolute number of cases of the disease attributable to the treatment. The use of either the multiplicative or additive scale will depend on the goal of the inference.
```

#### 1.4 Random variability
Source of random error: Sampling varaibility(Super probability cannot be compuated, only consistently estimated by the sample proportions, one cannot conclude with certainty that thee is or is not a causal effect) and Nondeterministic counterfactuals(As defined, the values of the counterfactual outcomes are fixed or deterministic for each individual, <img src="https://render.githubusercontent.com/render/math?math=Y^{a=1} = 1 and Y^{a=0} = 0">, However <img src="https://render.githubusercontent.com/render/math?math=Y^{a=1} and Y^{a=0}">)might be with probabilities, like 90%, 10%)

Later, we'll describe how our statistical estimates and confidence intervals for causal effects in super population are idential irrespective of whether the world is stochastic or deterministic at the level of individuals

#### 1.5 Causation versus assocation
![image](/img/CausationvsAssociation.png)
