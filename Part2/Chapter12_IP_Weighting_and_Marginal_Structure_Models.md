## 12.1 The causal question
Goal： estimate the average causal effect of smoking cessation A on weight gain Y.

The associational difference is generally different from the causal difference. The former will not generally have a causal interpretation if quitters and non-quitters differ with respect to characteristics that affect weight gain.

Here we assume that the following 9 variables, all measured at baseline, are sufficient to adjust for confounding: 
- sex (0: male, 1: female)
- age (in years)
- race (0: white, 1: other)
- education (5 categories)
- intensity and duration of smoking (number of cigarettes per day and years of smoking) - physical activity in daily life (3 categories)
- recreational exercise (3 categories), and weight (in kg)

That is, L represents a vector of 9 measured covariates. 

## 12.2 Estimating IP weights via modeling
IP weighting creates a pseudo-population in which the arrow from the covariates L to the treatment A is removed. More precisely:
- A and L are statistically independent 
- The mean <img src="https://render.githubusercontent.com/render/math?math=E_{ps}[Y|A=a]"> in the pseudo-population equals the standardized <img src="https://render.githubusercontent.com/render/math?math=E[Y|A=a, L=l]Pr[L=l]"> in the actual population.

Here we cannot estimated the quantiy <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|L]"> nonparametrically due to the curse of dimensionality: we simply counted how many people were treated(A=1) in each stratum of L, and then divided this count by the number of individuals in the stratum. 

Basic steps:
- To obtain parametric estimates of <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|L]"> in each of the millions of strata defined by L
  - We fit a logistic regression model for the A (**probability of quitting smoking**) with all L(**9 confounders**) included as covariates. 
- Computing the difference <img src="https://render.githubusercontent.com/render/math?math=\bar{E}_{ps}[Y|A=1] - \bar{E}_{ps}[Y|A=0]"> in the psuedo-population created by the estimated IP weights. 
  - Fit the linear mean model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A] = \theta_{0} + \theta_{1}*A"> by weighted least squares, with individuals weighted by their estimated weights <img src="https://render.githubusercontent.com/render/math?math=\bar{W}">: 1/<img src="https://render.githubusercontent.com/render/math?math=\bar{Pr}[A=1|L]"> for quitters and 1/(1- <img src="https://render.githubusercontent.com/render/math?math=\bar{Pr}[A=1|L]">) for the non-quitters. The parameter estimates <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}"> was 3.4. That is, we estimated that quitting smoking increase weight by <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}"> = 3.4 on average
- Obtain confidence interval about the <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}">=3.4 we need a method taht takes the IP weighting into account.
  - Use statistical theory to derive the corresponding variance estimator
  - Approximate the variance by nonparametric bootstrapping
  - Use the robust variance estimator (e.g., as used for GEE models with an independent working correlation) that is a standard option in most statistical software packages

## 12.3 Stabilized IP weights
Concept: 
- Nonstabilized IP weights: <img src="https://render.githubusercontent.com/render/math?math=W^{A} = 1/f(A|L)"> 
- Stabilized IP weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A} =f(A)/f(A|L)">)  

The stabilizing factor <img src="https://render.githubusercontent.com/render/math?math=f(A)"> in the numerator is responsible for the narrower range of the <img src="https://render.githubusercontent.com/render/math?math=f(A)/f(A|L)"> weights. For example: 
- The IP weights <img src="https://render.githubusercontent.com/render/math?math=f(A)/f(A|L)"> range from 0.33 to 4.30
- Whereas the IP weights <img src="https://render.githubusercontent.com/render/math?math=1/f(A|L)"> range from 1.05 to 16.7
- Note: The mean of the stabilized weights is expected to be 1 because the size of the pseudo-population equals that of the study population (In data analyses one should always check that the estimated weights have mean have 1).

Reason to stabilized IP weights: 
- Even though nonstabilized and stabilized IP weights result in the same estimate, stabilized weights typically result in narrower 95% confidence intervals than nonstabilized weights.
- However, the statistical superiority of the stabilized weights can only occur when the (IP weighted) model is not saturated (the two-parameter model was saturated because treatment A could only take 2 possible values).

## 12.4 Marginal structure models

Marginal structual models: Models for the marginal mean of a counterfactual outcome, <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}] = \beta_{0} + \beta_{1}*a">
- A (nonsaturated) marginal structural  mean model for a continuous treatment A.

Recall the basic concept:
- We used IP weighting to construct a pseudo-population, and then fit the model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A] = \theta_{0} + \theta_{1}*A"> to the pseudo-population data by using IP weighted least squares. Under our assumptions, association is causation in the pseudo-population. That is, the parameter <img src="https://render.githubusercontent.com/render/math?math={\theta}_{1}">  from IP weighted associational model can be endowed with the same causual interpretation as the parameter <img src="https://render.githubusercontent.com/render/math?math={\beta}_{1}"> from the structual model.

Example: continous treatment A “change in smoking intensity” defined as number of cigarettes smoked per day in 1982 minus number of cigarettes smoked per day at baseline.
- Marginal structural model: we believe a parabola can describes the does-response curve
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}] = \beta_{0} + \beta_{1}*a + \beta_{2}*a^{2}">
- Want to estimate the average causal effect of increasing smoking intensity by 20 cigarettes per day compared with no change
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}]">
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}] = 20\beta_{1} + 400\beta_{2}">
- Estimate stabilized weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A}=f(A)/f(A|L)">
  - For a continuous treatment A, <img src="https://render.githubusercontent.com/render/math?math=f(A|L)"> is the probability density function, which is hard to estimate correctly 
  - We need to use a linear regression model to estimate the mean and variance of residuals for all combinations of values of L.

