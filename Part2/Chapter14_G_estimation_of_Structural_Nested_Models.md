IP weighting, standardization, and g-estimation are often collectively referred to as g-methods because they are designed for application to generalized treatment contrasts involving treatments that vary over time.

There is a reason for introducing g-estimation later is that: describing g-estimation is facilitated by the specification of a structural model, even if the model is saturated. Models whose parameters are estimated via g-estimation are known as structural nested models. 

## 14.1 The causal question revisited
```
Sometimes one can be interested in the average causal effect in a subset of the population. 
For example, one may want to estimate the average causal effect in women.
```
To estimate the effect in a subset of the population one can use marginal structural models with product terms (see Chapter 12) or apply standardization to that subset only (Chapter 13).

In this chapter we will use g-estimation to estimate the average causal effect of smoking cessation A on weight gain Y in each strata defined by the covariates L. This conditional effect is represented by <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a,c=0}|L] - E[Y^{a=0,c=0}|L]">.

## 14.2 Exchangeability revisited
When conditional exchangeability holds, knowing the value of <img src="https://render.githubusercontent.com/render/math?math=Y^{a=0}"> does not help differentiate between quitters and nonquitters with a particular value of L. That is, the conditional (on L) probability of being a quitter is the same for all values of the counterfactual outcome <img src="https://render.githubusercontent.com/render/math?math=Y^{a=0}">. Mathematically, we write <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|Y^{a=0}, L] = Pr[A=1|L]">.

## 14.3 Structural nested mean models
Under exchangeability, the structural model can be written as <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a} - Y^{a=0}|A=a,L] = \beta_{1} * a + \beta{2} * a * L">, which is referred as a **structural nested mean model**. 
```
These models include parameters for the product terms between treatment A and the variables L, but no parameters for the variables L themselves. This is an attractive property of structural nested models because we are interested in the causal effect of A on Y within levels of L but not in the (noncausal) relation between L and Y .

(Page 192). 
```
- If there were no effect measure modification by L, these differences would be constant across strata, and our structural model for the conditional causal effect would be <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a} - Y^{a=0}|A=a,L] = \beta_{1} * a">.
- If there are effect modification by L, to allow for the causal effect to depend on L, we need to add a product term to the structual model <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a} - Y^{a=0}|A=a,L] = \beta_{1} * a + \beta_{2} * a * L">

Compared with IP weighting and standardization parametric models, structural nested models are semiparametric because they're agnostic about both the intercept and the main effect of L, that is, there is no parameter <img src="https://render.githubusercontent.com/render/math?math=\beta_{0}"> and no parameter <img src="https://render.githubusercontent.com/render/math?math=\beta_{3}"> for a term <img src="https://render.githubusercontent.com/render/math?math=\beta_{3} * L">. Therefore, the sturctural nested models make fewer assumptions and can be more robust to model misspecification than the parametric g-formula.

G-estimation can only be used to adjust for confounding, not selection bias. Thus, when using g-estimation, one first needs to adjust for selection bias due to censoring by IP weighting. In practice, this means that we first estimate nonstablized IP weights for censoring to create a pseudo-population inwhich nobody is censored, and then apply g-estimation to the pseudo-population: <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a, c=0} - Y^{a=0,c=0}|A=a,L] = \beta_{1} * a + \beta_{2} * a * L">

For continuous variables, the model needs to specify the dose-response function for the effect of treatment A on the mean outcome  Y. For example, <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a} - Y^{a=0}|A=a,L] = \beta_{1} * a + \beta_{2} * a^{2} + \beta_{3} * a * L + \beta_{4} * a^{2} * L">


## 14.4 Rank preservation
The additive rank-preserving model in this section makes a much stronger assumption than non-rank-preserving models: the assumption of constant treatment effect for all individuals with the same value of L.There is no reason why we would want to use such an unrealistic rank-preserving model in practice. 

And yet we use it in the next section to introduce g-estimation because g-estimation is easier to understand for rank-preserving models, and because the g-estimation procedure is actually the same for rank-preserving and nonrank-preserving models. Note that the (conditional additive) rank-preserving structural model is a structural mean model–the mean of the individual shifts from <img src="https://render.githubusercontent.com/render/math?math=Y^{a=0}"> to <img src="https://render.githubusercontent.com/render/math?math=Y^{a=1}">is equal to each of the individual shifts within levels of L.


## 14.5 G-estimation
![image](/img/g_estimate_1.png)

## 14.6 Structural nested models with two or more parameters
 
![image](/img/g_estimate_2.png)
