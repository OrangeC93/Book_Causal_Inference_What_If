## 2.1 Randomization
Exchangeability means that the counterfactual outcome and the actual treatment are independent, or <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A"> for all a. Randomization is expected to produce exchangeability. When the treated and the untreated are exchangeable, we sometimes say that treatment is exogenous.

Caution: <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A"> is different from <img src="https://render.githubusercontent.com/render/math?math=Y \perp\!\!\!\perp A">. For example, in a randomized experiment in which exchangeability <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A"> holds and the treatment has a causal effect on outcome, then <img src="https://render.githubusercontent.com/render/math?math=Y \perp\!\!\!\perp A"> does not hold because the treatment is associated with the observed outcome.

## 2.2 Conditional randomization
Conditional exchangebility: <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A|L"> for all a. 
For marginal randomized experiments the causal risk raio equals to the associational risk ratio because exchangeability ensures that the counterfactual risk under treatment level a.
For conditionally randomized experiment, there're two options:
- Compute the average causal effect in each of these subsets or strata of the population, called stratification. If the stratumspecific causal risk ratio in different subset L=1 and L=0, we say that the effect of treatment is modified by L, or that there's effect modification by L.
- We can compute the average causal effect 
<img src="https://render.githubusercontent.com/render/math?math=Pr[Y^(a=1) = 1]/ Pr[Y^(a=0) = 1]"> in the entire population.

## 2.3 Standardization
