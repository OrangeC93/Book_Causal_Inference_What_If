## 2.1 Randomization
Exchangeability means that the counterfactual outcome and the actual treatment are independent, or <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A"> for all a. Randomization is expected to produce exchangeability. When the treated and the untreated are exchangeable, we sometimes say that treatment is exogenous.

Caution: <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A"> is different from <img src="https://render.githubusercontent.com/render/math?math=Y \perp\!\!\!\perp A">. For example, in a randomized experiment in which exchangeability <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A"> holds and the treatment has a causal effect on outcome, then <img src="https://render.githubusercontent.com/render/math?math=Y \perp\!\!\!\perp A"> does not hold because the treatment is associated with the observed outcome.

## 2.2 Conditional randomization
Conditional exchangebility: <img src="https://render.githubusercontent.com/render/math?math=Y^{a} \perp\!\!\!\perp A|L"> for all a. 
For marginal randomized experiments the causal risk raio equals to the associational risk ratio because exchangeability ensures that the counterfactual risk under treatment level a.
For conditionally randomized experiment, there're two options:
- Compute the average causal effect in each of these subsets or strata of the population, called stratification. If the stratumspecific causal risk ratio in different subset L=1 and L=0, we say that the effect of treatment is modified by L, or that there's effect modification by L.
- We can compute the average causal effect 
<img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1} = 1]/ Pr[Y^{a=0} = 1]"> in the entire population.

## 2.3 Standardization
The standardized risks in the treaated and the untreated are equal to the counterfactual risk under treatment and no treatment, respectively. Therefore, the risk ratio 
<img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1} = 1]/ Pr[Y^{a=0} = 1]"> can be computed by standardization <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|L=l, A=1]*Pr[L=l]/ Pr[Y=1|L=l, A=1]*Pr[L=l]"> 

For example: the investigators used a random procedure to assign hearts (A = 1) with probability 50% to the 8 individuals in noncritical condition (L = 0), and with probability 75% to the 12 individuals in critical condition (L = 1).

<img src=/img/heart_eg.png width="40%" height="50%">

- <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|L=0, A=1]= Pr[Y^{a=1}|L=0]=1/4"> and <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|L=0, A=0]= Pr[Y^{a=0}|L=0]=1/4">
- <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|L=1, A=1]= Pr[Y^{a=1}|L=1]=2/3"> and <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|L=1, A=0]= Pr[Y^{a=0}|L=1]=2/3">
- Therefore  <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1}=1]"> = 1/4 * 0.4+2/3 * 0.6, same for <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=0}=1]">, now that we can compute the causal risk ratio.

## 2.4 Inverse probability weighting
The two trees are a simulation of what would have happened had all individuals in the population been untreated and treated, respectively. These simulations are correct under conditional exchangeability. Both simulations can be pooled to create a hypothetical population in which every individual appears as a treated and as an untreated individual. This hypothetical population, twice as large as the original population, is known as the pseudo-population.

<img src=/img/ip_weighted2.png width="40%" height="50%">
Below shows the entire pseudo-population. Under conditional exchangeability in the original population, the treated and the untreated are (unconditionally) exchangeable in the pseudo-population because the L is independent of A.

<img src=/img/ip_weighted.png width="30%" height="40%">
Both standardization and IP weighting can be viewed as procedures to build a new tree in which all individuals receive treatment a. Each method uses a different set of the probabilities to build the counterfactual tree: IP weighting uses the conditional probability of treatment A given the covariate L, standardization uses the probability of the covariate L and the conditional probability of outcome Y given A and L.
