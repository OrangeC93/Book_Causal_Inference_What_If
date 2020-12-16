There are two qualitatively different reasons why causal inferences may be wrong: systematic bias and random variability. The previous three chapters described three types of systematic biases: 
- Selection bias, measurement bias， both of which may arise in observational studies and in randomized experiments
- Unmeasured confounding, which is not expected in randomized experiments

## 10.1 Identification vs estimation
A Wald confidence interval centered at <img src="https://render.githubusercontent.com/render/math?math=\hat{p}"> is only guaranteed to be valid in **large samples**. However, not all consistent estimators can be used to center a valid Wald confidence interval, even in large samples. Most users of statistics will consider an estimator unbiased if it can center a valid Wald interval and biased if it cannot.

## 10.2 Estimation of causal effects
Heretofore we have assumed that there is a larger group–the super-population–from which the study participants were randomly sampled. 

## 10.3 The myth of the super population
Here we will accept that individuals were randomly sampled from a super-population, and explore the consequences of random variability for causal inference in that context.

## 10.4 The conditionality "principle"

## 10.5 The curse of dimensionality
This is the curse of dimensionality: conditional on all 100 covariates the marginal estimator is still biased, but now the conditional estimator is uninformative. This shows that, just because conditionality is compelling in simple examples, it should not be raised to a principle since it cannot be carried through for high-dimensional models.

