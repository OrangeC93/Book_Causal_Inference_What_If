## 15.1 Outcome regression
we have described IP weighting, standardization, and g-estimation to estimate the average causal effect of smoking cessation (the treatment) A on weight gain (the outcome) Y . We also described how to estimate the average causal effect within subsets of the population, either by restricting the analysis to the subset of interest or by adding product terms in marginal structural models (Chapter 12) and structural nested models (Chapter 14). 
- Take structural nested models. These models include parameters for the product terms between treatment A and the variables L, but no parameters for the variables L themselves. This is an attractive property of structural nested models because we are interested in the causal effect of A on Y within levels of L but not in the (noncausal) relation between L and Y . A method– g-estimation of structural nested models–that is agnostic about the functional form of the L-Y relation is protected from bias due to misspecifying this relation.

- On the other hand, if we were willing to specify the L-Y association within In Chapter 12, we referred to this levels of L, we would consider the structural model
<img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|Y^{a=0}, L] = Pr[A=1|L]">.
 
## 15.2 Propensity scores
Propensity score: π(L) measures the propensity of individuals to receive treatment given the information available in the covariates L. If the distribution of π(L) were the same for the treated A = 1 and the untreated A = 0, then there would be no confounding due to L, i.e., there would be no open path from L to A on a causal diagram.


Under exchangeability and positivity within levels of the propensity score π(L), the propensity score can be used to estimate causal effects using stratification (including outcome regression), standardization, and matching.

 
