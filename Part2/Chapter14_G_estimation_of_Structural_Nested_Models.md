## 14.1 The causal question revisited
In this chapter we will use g-estimation to estimate the average causal effect of smoking cessation A on weight gain Y in each strata defined by the covariates L. This conditional effect is represented by <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a,c=0}|L] - E[Y^{a=0,c=0}|L]">.

## 14.2 Exchangeability revisited
When conditional exchangeability holds, knowing the value of <img src="https://render.githubusercontent.com/render/math?math=Y^{a=0}"> does not help differentiate between quitters and nonquitters with a particular value of L. That is, the conditional (on L) probability of being a quitter is the same for all values of the counterfactual outcome <img src="https://render.githubusercontent.com/render/math?math=Y^{a=0}">. Mathematically, we write <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|Y^{a=0}, L] = Pr[A=1|L]">.

## 14.3 Structural nested mean models
Under exchangeability, the structural model can be written as <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a} - Y^{a=0}|A=a,L] = \beta_{1} * a + \beta{2} * a * L">, which is referred as a **structural nested mean model**. 
- If there were no effect measure modification by L, these differences would be constant across strata, and our structural model for the conditional causal effect would be <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a} - Y^{a=0}|A=a,L] = \beta * a">.
- If there are effect modification by L, to allow for the causal effect to depend on L, we need to add a product term to the structual model <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a} - Y^{a=0}|A=a,L] = \beta * a + \beta * a * L">

Compared with IP weighting and standardization parametric models, structural nested models are semiparametric because they're agnostic about both the intercept and the main effect of L, that is, there is no parameter <img src="https://render.githubusercontent.com/render/math?math=\beta_{0}"> and no parameter <img src="https://render.githubusercontent.com/render/math?math=\beta_{3}"> for a term <img src="https://render.githubusercontent.com/render/math?math=\beta_{3} * L">. Therefore, the sturctural nested models make fewer assumptions and can be more robust to model misspecification than the parametric g-formula.

G-estimation can only be used to adjust for confounding, not selection bias. Thus, when using g-estimation, one first needs to adjust for selection bias due to censoring by IP weighting. In practice, this means that we first estimate nonstablized IP weights for censoring to create a pseudo-population inwhich nobody is censored, and then apply g-estimation to the pseudo-population: <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a, c=0} - Y^{a=0,c=0}|A=a,L] = \beta * a + \beta * a * L">

## 14.4 Rank preservation
