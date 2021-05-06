## 12.1 The causal question
Goal: estimate the average causal effect of **smoking cessation A** on **weight gain Y**.

Here we assume that the following 9 variables, all measured at baseline, are sufficient to adjust for confounding: 
- sex (0: male, 1: female)
- age (in years)
- race (0: white, 1: other)
- education (5 categories)
- intensity and duration of smoking (number of cigarettes per day and years of smoking) - physical activity in daily life (3 categories)
- recreational exercise (3 categories), and weight (in kg)

That is, **L represents a vector of 9 measured covariates**. 

## 12.2 Estimating IP weights via modeling
IP weighting creates a pseudo-population in which the arrow from the covariates L to the treatment A is removed.
- The pseudo-population is created by weighting each individual by the inverse of the conditional probability of receiving the treatment level that she indeed received. The individual-specific IP weights for treatment A are defined as <img src="https://render.githubusercontent.com/render/math?math=W^{A} = 1/f(A|L)">.
- If it's **dichotomous treatment A**, the denominator <img src="https://render.githubusercontent.com/render/math?math=f(A|L)"> of IP weight is the probability of quiting conditional on measured confounders, <img src="https://render.githubusercontent.com/render/math?math=Pr[A=0|L]">, which is known as the **propensity score**. 

Here we cannot estimated the quantity <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|L]"> nonparametrically (like we simply counted how many people were treated(A=1) in each stratum of L, and then divided this count by the number of individuals in the stratum) due to the **curse of dimensionality**.

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
- dischotomous A to continues Y

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
- It will be **saturated** if the **Treatment** is **dichotomous**, therefore sample averages computed in the pseudo-population were eough to stiamte the causal effect of interest. 

However when Treatment is **polytomous or continuous**:
- Example: continous treatment A “change in smoking intensity” defined as number of cigarettes smoked per day in 1982 minus number of cigarettes smoked per day at baseline. 
- Here, Treatment can take many values

**Example**: Let us say that we're interested in estimating the difference in average weight change under different changes in treatment intensity in the 1162 individuals who smoked 25 or fewer cigarettes per day at a baseline. Supppose we want to estimate the average causal effect of increasing smoking intensity by 20 cigarettes pery day compared to no change
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}]">
Step1: according to the (1)**marginal structural model** and the (2)assumption that we believe a **parabola** can describes the does-response curve
  - The marginal structural model will be <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}] = \beta_{0} %2B \beta_{1}a %2B \beta_{2}a^{2}">
  - Then <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}] = 20\beta_{1} %2B 400\beta_{2}">

Step2: we need to estimate stabilized weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A}=f(A)/f(A|L)">
  - For a continuous Treatment A, <img src="https://render.githubusercontent.com/render/math?math=f(A|L)"> is the probability density function(pdf), which is hard to estimate correctly. **That is the reason why using IP weighting for continuous treatments will often be dangerous.**
  - We need to use a **linear regression** model to estimate the **mean <img src="https://render.githubusercontent.com/render/math?math=E(A|L)"> and variance of residuals** for all combinations of values of L.
  - Code: [program 12.4](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb)
    - continous A to continous Y
Note: We could also consider a marginal structural model for a **dichotomous outcome**: "if interested in the causal effect of quitting smoking A (1: yes, 0: no) on the risk of death D (1: yes, 0: no) by 1982, one could consider a _marginal structural logistic model_"
- <img src="https://render.githubusercontent.com/render/math?math=logitPr[D^{a} = 1] = \alpha_{0} %2B \alpha_{1}a"> where <img src="https://render.githubusercontent.com/render/math?math=exp(\alpha_{1})"> is the causal odds ratio of death for quitting vs not quitting smoking
- Code: [program 12.5](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb)
  - dichotomous A to dichotomous Y

Conclusion: 
X\Y | dischotomous | continous | 
--- | --- | --- | 
dischotomous | marginal structural saturated logistic model (program 12.5) | marginal structural saturated linear model (program 12.2) | 
continous | marginal structural non-saturated logistic model | marginal structural non-saturated linear model (program 12.4) | 
- dischotomous X, ip weighting will be calcuated from a logistic regression 
- continous X, ip weighting will be calcuated from pdf

## 12.5 Effect modification and marginal structural models
[Difference between effects and confounders](https://s4be.cochrane.org/blog/2015/06/04/difference-effect-modification-confounding/#:~:text=Effect%20modification%20is%20all%20about,onto%20the%20market%2C%20Drug%20X)
- Effect modification is all about stratification and occurs when an exposure has a different effect among different subgroups. Effect modification is associated with the outcome but not the exposure.
  - For example, imagine you are testing out a new treatment that has come onto the market, Drug X. If Drug X works in females but does not work in males, this is an example of effect modification.
- Confounding occurs when a factor is associated with both the exposure and the outcome but does not lie on the causative pathway.
  - For example, if you decide to look for an association between coffee and lung cancer, this association may be distorted by smoking if smokers are unevenly distributed between the two groups. It may appear that there is an association between coffee and lung cancer, however if you were to consider smokers and non-smokers separately for each group this would in fact show no association.
Add **covariates V** (which may be non-confounders) in **a marginal structual model** to assess effect modification. 

Example: 
- Suppose it's hypothesized that the effect of smoking cessation varies by **sex V (1: woman, 0: man)**. To examine this hypothesis, we add the covariate V to our marginal structural mean model: <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}|V] = \beta_{0} %2B \beta_{1}a %2B \beta_{2}Va %2B \beta_{3}V">. If <img src="https://render.githubusercontent.com/render/math?math=\beta_{2} \neq 0"> additive effect modification is present.

Estimate the model parameters:
- Fit the linear regression model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A, V] = \theta_{0} %2B \theta_{1}a %2B \theta_{2}Va %2B \theta_{3}V"> via weighted least square IP weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A}(V) = f[A|V]/f[A|L]"> or <img src="https://render.githubusercontent.com/render/math?math=W^{A} = f[A]/f[A|L]">, We estimate <img src="https://render.githubusercontent.com/render/math?math=SW^{A}(V)"> using the same approach as for <img src="https://render.githubusercontent.com/render/math?math=SW^{A}">, except that we add the covariate V to the logistic model for the numerator of the weights.
- Note: the vector of **covariates L** needs to include **V** -- even if V is not a confounder -- and any other variables that are needed to ensure exchangeability within levels of V.

Code: [program 12.6](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb)
## 12.6 Censoring and missing data
Selecting only individual with nonmissing outcome values-- that is, censoring from the analysis those with missing values-- may introduce selection bias.
- Censoring C = 1, if body wight is unmeasured, and 0 if boday weight is measured. 

Under the null, selecting only uncensored individuals for the analysis is expected to induce bias when C is either a collider on a pathway between treatment A and the outcome Y, or the descendant of one such collider. 
- For example: (1)treatment A is associated with censoring C–5.8% of quitters versus 3.2% nonquitters were censored And (2)at least some predictors of Y are associated with C–the average baseline weight was 76.6 kg in the censored versus 70.8 in the uncensored.

IP weights 
- <img src="https://render.githubusercontent.com/render/math?math=W^{A,C} = W^{A}  W^{C}"> in which <img src="https://render.githubusercontent.com/render/math?math=W^{C} = 1/Pr[C=0|L,A]"> for the **uncensored individuals** and <img src="https://render.githubusercontent.com/render/math?math=W^{C} = 0"> for the **cencored individuals**. 
- <img src="https://render.githubusercontent.com/render/math?math=SW^{A,C} = SW^{A}  SW^{C}"> in which <img src="https://render.githubusercontent.com/render/math?math=SW^{C} = Pr[C=0|A]/Pr[C=0|L,A]"> for create a psuedo population of the same size as the original study population after censoring

Remember that the weights  <img src="https://render.githubusercontent.com/render/math?math=W^{C} = 1/Pr[C=0|L,A]"> create a pseudopopulation with the same size as that of the original study population before censoring, and in which there is no arrow from either L or A into C. 
- In our example, the estimates of IP weights for censoring  <img src="https://render.githubusercontent.com/render/math?math=W^{C}">  will create a pseudo-population with (approximately) 1566+ 63 = 1629 in which, under our assumptions, there is no selection bias because there is no selection. That is, we fit the weighted model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A,C=0] = \theta_{0} %2B \theta_{1}a"> with weights <img src="https://render.githubusercontent.com/render/math?math=W^{A, C}"> to estimate the parameters of the marginal structural model <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a,c=0}] = \theta_{0} %2B \theta_{1}a"> in the entire population.

If the result is same as not including cencered IP weighting, which suggests that there's either no selection bias by censoring or that our measured covariates are unable to eliminate it. 

Code: [program 12.6](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter12.ipynb)

## In summary
IP weighting creates a pseudo-population in which the distribution of the variables in L is the same in the treated and the untreated. Then, under the assumptions of exchangeability and positivity given L, we estimate <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a,c=0}]"> by simply computing <img src="https://render.githubusercontent.com/render/math?math=\bar{E}[Y|A=a,C=0]"> as the average outcome in the pseudo-population. If A were a continuous treatment, we would also need a structural model to estimate <img src="https://render.githubusercontent.com/render/math?math=\bar{E}[Y|A, C=0]"> in the pseudo-population for all possible values of A. 

Preference: https://zhuanlan.zhihu.com/p/347813287
