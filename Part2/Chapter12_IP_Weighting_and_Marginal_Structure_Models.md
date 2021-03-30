## 12.1 The causal question
Goal: estimate the average causal effect of smoking cessation A on weight gain Y.

Here we assume that the following 9 variables, all measured at baseline, are sufficient to adjust for confounding: 
- sex (0: male, 1: female)
- age (in years)
- race (0: white, 1: other)
- education (5 categories)
- intensity and duration of smoking (number of cigarettes per day and years of smoking) - physical activity in daily life (3 categories)
- recreational exercise (3 categories), and weight (in kg)

That is, L represents a vector of 9 measured covariates. 

## 12.2 Estimating IP weights via modeling
IP weighting creates a pseudo-population in which the arrow from the covariates L to the treatment A is removed, which means:
- A and L are statistically independent 
- The mean <img src="https://render.githubusercontent.com/render/math?math=E_{ps}[Y|A=a]"> in the pseudo-population equals the standardized <img src="https://render.githubusercontent.com/render/math?math=E[Y|A=a, L=l]Pr[L=l]"> in the actual population.


The pseudo-population is created  by weighting each individual by the inverse of the conditional probability of receiving the treatment level that she indeed received. The individual-specific IP weights for treatment A are defined as <img src="https://render.githubusercontent.com/render/math?math=W^{A} = 1/f(A|L)">.If it's dichotomous treatment A, the denominator <img src="https://render.githubusercontent.com/render/math?math=f(A|L)"> of IP weight is the probability of quiting conditional on measured confounders, <img src="https://render.githubusercontent.com/render/math?math=Pr[A=0|L]">, which is known as the propensity score. 

Here we cannot estimated the quantity <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|L]"> nonparametrically (we simply counted how many people were treated(A=1) in each stratum of L, and then divided this count by the number of individuals in the stratum) due to the curse of dimensionality.

Basic steps:
- Obtain parametric estimates of <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|L]"> in each of the millions of strata defined by L
  - Fit a logistic regression model for the **A** with all **L** (9 confounders) included as covariates. 
- Computing the difference <img src="https://render.githubusercontent.com/render/math?math=\bar{E}_{ps}[Y|A=1] - \bar{E}_{ps}[Y|A=0]"> in the psuedo-population created by the estimated IP weights. 
  - Fit the linear mean model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A] = \theta_{0}%2B\theta_{1}A"> by weighted least squares, with individuals weighted by their estimated weights <img src="https://render.githubusercontent.com/render/math?math=\bar{W}">: <img src="https://render.githubusercontent.com/render/math?math=1/\bar{Pr}[A=1|L]"> for quitters and <img src="https://render.githubusercontent.com/render/math?math=1/(1-\bar{Pr}[A=1|L])"> for the non-quitters. 
  - The parameter estimates <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}"> was 3.4. That is, we estimated that quitting smoking A increase weight Y by <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}"> = 3.4 on average.
- Obtain confidence interval about the <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}">=3.4 we need a method that takes the IP weighting into account. There're 3 ways:
  - Use **statistical theory** to derive the corresponding variance estimator
  - Approximate the variance by nonparametric **bootstrapping**
  - Use the **robust variance estimator**(e.g., as used for GEE models with an independent working correlation) that is a standard option in most statistical software packages

Code: [Program 12.2](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb)

## 12.3 Stabilized IP weights
Concept: 
- Nonstabilized IP weights: <img src="https://render.githubusercontent.com/render/math?math=W^{A} = 1/f(A|L)"> 
- Stabilized IP weights: <img src="https://render.githubusercontent.com/render/math?math=SW^{A} =f(A)/f(A|L)">)  

The stabilizing factor <img src="https://render.githubusercontent.com/render/math?math=f(A)"> in the numerator is responsible for the narrower range of the <img src="https://render.githubusercontent.com/render/math?math=f(A)/f(A|L)"> weights. For example: 
- The IP weights <img src="https://render.githubusercontent.com/render/math?math=f(A)/f(A|L)"> range from 0.33 to 4.30
- Whereas the IP weights <img src="https://render.githubusercontent.com/render/math?math=1/f(A|L)"> range from 1.05 to 16.7
- Note: The mean of the stabilized weights is expected to be 1 because the size of the pseudo-population equals that of the study population (In data analyses one should always check that the estimated weights have mean have 1).

Reason to stabilized IP weights: 
- Even though nonstabilized and stabilized IP weights result in the same estimate, stabilized weights typically result in narrower 95% confidence intervals than nonstabilized weights.
- However, the statistical superiority of the stabilized weights can only occur when the (IP weighted) model is not saturated (the two-parameter model was saturated because treatment A could only take 2 possible values).

Code [Section 12.3 Program 12.3](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb) 

Referene: http://www.rebeccabarter.com/blog/2017-07-05-ip-weighting/

## 12.4 Marginal structure models
Marginal structual models: models for the marginal mean of a counterfactual outcome, like <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}] = \beta_{0} %2B \beta_{1}a">
- It will be saturated if the treatment is dichotomous, thus sample averages computed in the pseudo-population were eough to stiamte the causal effect of interest. 

However when treatment is **polytomous or continuous**:
- Example: continous treatment A “change in smoking intensity” defined as number of cigarettes smoked per day in 1982 minus number of cigarettes smoked per day at baseline. 
- Treatment can take many values

Here, supppose we want to estimate the average causal effect of inccreasing smoking intensity by 20 cigarettes pery day compared to no change
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}]">
According to the **marginal structural model** and the assumption that **we believe a parabola can describes the does-response curve**
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}] = \beta_{0} %2B \beta_{1}a %2B \beta_{2}a^{2}">
  - Then <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}] = 20\beta_{1} %2B 400\beta_{2}">
Then we need to estimate stabilized weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A}=f(A)/f(A|L)">
  - For a continuous treatment A, <img src="https://render.githubusercontent.com/render/math?math=f(A|L)"> is the probability density function, which is hard to estimate correctly. **That is the reason why using IP weighting for continuous treatments will often be dangerous.**
  - We need to use a linear regression model to estimate the mean and variance of residuals for all combinations of values of L.
  - Code: [program 12.4](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb)

We could also consider a marginal structural model for a dichotomous outcome: "if interested in the causal effect of quitting smoking A (1: yes, 0: no) on the risk of death D (1: yes, 0: no) by 1982, one could consider a _marginal structural logistic model_"
- Code: [program 12.5](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb)

## 12.5 Effect modification and marginal structural models
Add **covariates V** (which may be non-confounders) in **a marginal structual model** to assess effect modification. 

Example: 
- Suppose it is hypothesized that the effect of smoking cessation varies by sex V (1: woman, 0: man). To examine this hypothesis, we add the covariate V to our marginal structural mean model: <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}|V] = \beta_{0} %2B \beta_{1}a %2B \beta_{2}Va %2B \beta_{3}V">. If <img src="https://render.githubusercontent.com/render/math?math=\beta_{2} \neq 0"> additive effect modification is present.

Estimate the model parameters:
- Fit the linear regression model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A, V] = \theta_{0} %2B \theta_{1}a %2B \theta_{2}Va %2B \theta_{3}V"> via weighted least square IP weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A}(V) = f[A|V]/f[A|L]"> or <img src="https://render.githubusercontent.com/render/math?math=W^{A} = f[A]/f[A|L]">, We estimate <img src="https://render.githubusercontent.com/render/math?math=SW^{A}(V)"> using the same approach as for <img src="https://render.githubusercontent.com/render/math?math=SW^{A}">, except that we add the covariate V to the logistic model for the numerator of the weights.
- The vector of covariates L needs to include V -- even if V is not a confounder -- and any other variables that are needed to ensure exchangeability within levels of V.

## 12.6 Censoring and missing data
```
63 additional individuals who met the eligibility criteria but we excluded from the analysis because their weight in 1982 was not known, selecting only in non missing outcome values may introduce selection bias.
```
IP weights 
- <img src="https://render.githubusercontent.com/render/math?math=W^{A,C} = W^{A}  W^{C}"> in which <img src="https://render.githubusercontent.com/render/math?math=W^{C} = 1/Pr[C=0|L,A]"> for the uncensored individuals and <img src="https://render.githubusercontent.com/render/math?math=W^{C} = 0"> for the cencored individuals. 
- <img src="https://render.githubusercontent.com/render/math?math=SW^{A,C} = SW^{A}  SW^{C}"> in which <img src="https://render.githubusercontent.com/render/math?math=SW^{C} = Pr[C=0|A]/Pr[C=0|L,A]"> for create a psuedo population of the same size as the original study population after censoring


## In summary
IP weighting creates a pseudo-population in which the distribution of the variables in L is the same in the treated and the untreated. Then, under the assumptions of exchangeability and positivity given L, we estimate <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a,c=0}]"> by simply computing <img src="https://render.githubusercontent.com/render/math?math=\bar{E}[Y|A=a,C=0]"> as the average outcome in the pseudo-population. If A were a continuous treatment, we would also need a structural model to estimate <img src="https://render.githubusercontent.com/render/math?math=\bar{E}[Y|A, C=0]"> in the pseudo-population for all possible values of A. 

