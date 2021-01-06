## 12.1 The causal question
Goal： estimate the average causal effect of smoking cessation A on weight gain Y.

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
- Obtain parametric estimates of <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|L]"> in each of the millions of strata defined by L
  - We fit a logistic regression model for the A (**probability of quitting smoking**) with all L(**9 confounders**) included as covariates. 
  ```python
  ## program 12.2
  def logit_ip_f(y, X):
    """
    Create the f(y|X) part of IP weights
    from logistic regression
    
    Parameters
    ----------
    y : Pandas Series
    X : Pandas DataFrame
    
    Returns
    -------
    Numpy array of IP weights
    
    """
    model = sm.Logit(y, X)
    res = model.fit()
    weights = np.zeros(X.shape[0])
    weights[y == 1] = res.predict(X.loc[y == 1])
    weights[y == 0] = 1-res.predict(X.loc[y == 0])
    return weights
  ```
- Computing the difference <img src="https://render.githubusercontent.com/render/math?math=\bar{E}_{ps}[Y|A=1] - \bar{E}_{ps}[Y|A=0]"> in the psuedo-population created by the estimated IP weights. 
  - Fit the linear mean model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A] = \theta_{0}%2B\theta_{1}A"> by weighted least squares, with individuals weighted by their estimated weights <img src="https://render.githubusercontent.com/render/math?math=\bar{W}">: 1/<img src="https://render.githubusercontent.com/render/math?math=\bar{Pr}[A=1|L]"> for quitters and 1/(1- <img src="https://render.githubusercontent.com/render/math?math=\bar{Pr}[A=1|L]">) for the non-quitters. The parameter estimates <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}"> was 3.4. That is, we estimated that quitting smoking increase weight by <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}"> = 3.4 on average.
  ```python
  ## program 12.2
  X_ip = nhefs[[
    'constant',
    'sex', 'race', 'age', 'age^2', 'edu_2', 'edu_3', 'edu_4', 'edu_5',
    'smokeintensity', 'smokeintensity^2', 'smokeyrs', 'smokeyrs^2', 
    'exercise_1', 'exercise_2', 'active_1', 'active_2', 'wt71', 'wt71^2']]

  denoms = logit_ip_f(nhefs.qsmk, X_ip)
  weights = 1 / denoms
  
  ## main model, weighted least squares gives the right coefficients, but the standard error is off.
  denoms = logit_ip_f(nhefs.qsmk, X_ip)
  wls = sm.WLS(y, X, weights=weights) 
  res = wls.fit()
  res.summary().tables[1]
  ```
- Obtain confidence interval about the <img src="https://render.githubusercontent.com/render/math?math=\bar{\theta}">=3.4 we need a method that takes the IP weighting into account. There're 3 ways:
  - Use statistical theory to derive the corresponding variance estimator
  - Approximate the variance by nonparametric bootstrapping
  - Use the robust variance estimator (e.g., as used for GEE models with an independent working correlation) that is a standard option in most statistical software packages
  ``` python
  ## program 12.2
  gee = sm.GEE(
      nhefs.wt82_71,
      nhefs[['constant', 'qsmk']],
      groups=nhefs.seqn,
      weights=weights
  )
  res = gee.fit()
  res.summary().tables[1]

  est = res.params.qsmk
  conf_ints = res.conf_int(alpha=0.05, cols=None)
  lo, hi = conf_ints[0]['qsmk'], conf_ints[1]['qsmk']

  print('           estimate   95% C.I.')
  print('theta_1     {:>6.2f}   ({:>0.1f}, {:>0.1f})'.format(est, lo, hi))
  ```
## 12.3 Stabilized IP weights
Concept: 
- Nonstabilized IP weights: <img src="https://render.githubusercontent.com/render/math?math=W^{A} = 1/f(A|L)"> 
- Stabilized IP weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A} =f(A)/f(A|L)">)  
``` python
## program 12.3
s_weights = np.zeros(nhefs.shape[0])
s_weights[qsmk] = qsmk.mean() * weights[qsmk]    # `qsmk` was defined a few cells ago
s_weights[~qsmk] = (1 - qsmk).mean() * weights[~qsmk]
```
The stabilizing factor <img src="https://render.githubusercontent.com/render/math?math=f(A)"> in the numerator is responsible for the narrower range of the <img src="https://render.githubusercontent.com/render/math?math=f(A)/f(A|L)"> weights. For example: 
- The IP weights <img src="https://render.githubusercontent.com/render/math?math=f(A)/f(A|L)"> range from 0.33 to 4.30
- Whereas the IP weights <img src="https://render.githubusercontent.com/render/math?math=1/f(A|L)"> range from 1.05 to 16.7
- Note: The mean of the stabilized weights is expected to be 1 because the size of the pseudo-population equals that of the study population (In data analyses one should always check that the estimated weights have mean have 1).

Reason to stabilized IP weights: 
- Even though nonstabilized and stabilized IP weights result in the same estimate, stabilized weights typically result in narrower 95% confidence intervals than nonstabilized weights.
- However, the statistical superiority of the stabilized weights can only occur when the (IP weighted) model is not saturated (the two-parameter model was saturated because treatment A could only take 2 possible values).

## 12.4 Marginal structure models
Marginal structual models: models for the marginal mean of a counterfactual outcome (the outcome variable of this model is counterfactual and hence generally unobserved, therefore the model cannot be fit to the data of any real world study), like <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}] = \beta_{0} %2B \beta_{1}a">
(this is a saturated marginal structural mean model for a dichotomous treatment A)

Recall the basic concept:
- We used IP weighting to construct a pseudo-population, and then fit the model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A] = \theta_{0} %2B \theta_{1}A"> to the pseudo-population data by using IP weighted least squares. Under our assumptions, association is causation in the pseudo-population. That is, the **parameter <img src="https://render.githubusercontent.com/render/math?math={\theta}_{1}">  from IP weighted associational model** can be endowed with the same causual interpretation as the **parameter <img src="https://render.githubusercontent.com/render/math?math={\beta}_{1}"> from the structual model**.

Example: continous treatment A “change in smoking intensity” defined as number of cigarettes smoked per day in 1982 minus number of cigarettes smoked per day at baseline. We are interested in estimating the difference in average weight change under different changes in treatment intensity in the 1162 individuals who smoked 25 or fewer cigarettes per day at baseline.

- Marginal structural model: we believe a parabola can describes the does-response curve
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}] = \beta_{0} %2B \beta_{1}a %2B \beta_{2}a^{2}">
- Want to estimate the average causal effect of increasing smoking intensity by 20 cigarettes per day compared with no change
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}]">
  - <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=20}] - E[Y^{a=0}] = 20\beta_{1} %2B 400\beta_{2}">
- Estimate stabilized weights <img src="https://render.githubusercontent.com/render/math?math=SW^{A}=f(A)/f(A|L)">
  - For a continuous treatment A, <img src="https://render.githubusercontent.com/render/math?math=f(A|L)"> is the probability density function, which is hard to estimate correctly. we need to use a linear regression model to estimate the mean and variance of residuals for all combinations of values of L.
  ```python
  ## program 12.5
  fAL = scipy.stats.norm.pdf(
    A,                        # A
    A_pred,                   # mu = E[A|L]
    np.sqrt(res.mse_resid)    # sigma)
  fA = scipy.stats.norm.pdf(A, A.mean(), A.std())
  sw = fA / fAL
  
  ## fit marginal structural model
  y = intensity25.wt82_71
  X = pd.DataFrame(OrderedDict((
    ('constant', np.ones(y.shape[0])),
    ('A', A),
    ('A^2', A**2))))

  model = sm.GEE(
      y,
      X,
      groups=intensity25.seqn,
      weights=sw
  )
  res = model.fit()
  
  ## get confidence interval
  from statsmodels.regression._prediction import get_prediction
  pred_inputs = [
    [1, 0, 0],       # no change in smoking intensity
    [1, 20, 20**2],  # plus 20 cigarettes / day]
  pred = get_prediction(res, exog=pred_inputs)
  summary = pred.summary_frame().round(1)
  summary[["mean", "mean_ci_lower", "mean_ci_upper"]]
  ```
  - For a dichotomous outcome: "if interested in the causal effect of quitting smoking A (1: yes, 0: no) on the risk of death D (1: yes, 0: no) by 1982, one could consider a _marginal structural logistic model_"
 ```python
 model = sm.GEE(
    nhefs.death,
    nhefs[['constant', 'qsmk']],
    groups=nhefs.seqn,
    weights=s_weights,
    family=sm.families.Binomial()
)
res = model.fit()
res.summary().tables[1]

## odd ratio
est = np.exp(res.params.qsmk)
conf_ints = res.conf_int(alpha=0.05, cols=None)
lo = np.exp(conf_ints[0]['qsmk'])
hi = np.exp(conf_ints[1]['qsmk'])

print('           estimate   95% C.I.')
print('odds ratio  {:>6.2f}   ({:>0.1f}, {:>0.1f})'.format(est, lo, hi))
 ```

## 12.5 Effect modification and marginal structural models
Add covariates V (which may be non-confounders) in a marginal structual model to assess effect modification. Suppose it is hypothesized that the effect of smoking cessation varies by sex V (1: woman, 0: man). To examine this hypothesis, we add the covariate V to our marginal structural mean model: <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a}|V] = \beta_{0} %2B \beta_{1}a %2B \beta_{2}Va %2B \beta_{3}V">. If <img src="https://render.githubusercontent.com/render/math?math=\beta_{2} \neq 0"> additive effect modification is present.

Estimate the model parameters:
- Fit the linear regression model via weighted least square IP weights.
- The vector of covariates L needs to include V -- even if V is not a confounder -- and any other variables that are needed to ensure exchangeability within levels of V
- <img src="https://render.githubusercontent.com/render/math?math=SW^{A}(V) = f[A|V]/f[A|L]"> or <img src="https://render.githubusercontent.com/render/math?math=SW^{A}(V) = f[A]/f[A|L]">
```python
## Create the numerator of the IP weights. Reuse the basic weights for the denominator.
numer = logit_ip_f(nhefs.qsmk, nhefs[['constant', 'sex']])
sw_AV = numer * weights

## 
nhefs['qsmk_and_female'] = nhefs.qsmk * nhefs.sex

model = sm.WLS(
    nhefs.wt82_71,
    nhefs[['constant', 'qsmk', 'sex', 'qsmk_and_female']],
    weights=sw_AV
)
res = model.fit(cov_type='cluster', cov_kwds={'groups': nhefs.seqn})
res.summary().tables[1]
```

## 12.6 Censoring and missing data
```
63 additional individuals who met the eligibility criteria but we excluded from the analysis because their weight in 1982 was not known, selecting only in non missing outcome values may introduce selection bias.
```
IP weights 
- <img src="https://render.githubusercontent.com/render/math?math=W^{A,C} = W^{A}  W^{C}"> in which <img src="https://render.githubusercontent.com/render/math?math=W^{C} = 1/Pr[C=0|L,A]"> for the uncensored individuals and <img src="https://render.githubusercontent.com/render/math?math=W^{C} = 0"> for the cencored individuals. 
- <img src="https://render.githubusercontent.com/render/math?math=SW^{A,C} = SW^{A}  SW^{C}"> in which <img src="https://render.githubusercontent.com/render/math?math=SW^{C} = Pr[C=0|A]/Pr[C=0|L,A]"> for create a psuedo population of the same size as the original study population after censoring

```python
## censor feature
nhefs_all['censored'] = nhefs_all.wt82.isnull().astype('int')

## IP weights for treatmen
X_ip = nhefs_all[[
    'constant', 'sex', 'race', 'edu_2', 'edu_3', 'edu_4', 'edu_5', 
    'exercise_1', 'exercise_2', 'active_1', 'active_2',
    'age', 'age^2', 'wt71', 'wt71^2',
    'smokeintensity', 'smokeintensity^2', 'smokeyrs', 'smokeyrs^2'
]]
ip_denom = logit_ip_f(nhefs_all.qsmk, X_ip)
ip_numer = logit_ip_f(nhefs_all.qsmk, nhefs_all.constant)
sw_A = ip_numer / ip_denom

## IP weights for censoring
# same as previous, but with 'qsmk' added
X_ip = nhefs_all[[
    'constant', 'sex', 'race', 'edu_2', 'edu_3', 'edu_4', 'edu_5', 
    'exercise_1', 'exercise_2', 'active_1', 'active_2',
    'age', 'age^2', 'wt71', 'wt71^2',
    'smokeintensity', 'smokeintensity^2', 'smokeyrs', 'smokeyrs^2',
    'qsmk'
]]
ip_denom = logit_ip_f(nhefs_all.censored, X_ip)
ip_numer = logit_ip_f(
    nhefs_all.censored,
    nhefs_all[['constant', 'qsmk']]
)
sw_C = ip_numer / ip_denom
sw_C[nhefs_all.censored == 1] = 1

## create the combined IP weights
sw_AC = sw_A * sw_C

wls = sm.WLS(
    nhefs.wt82_71,
    nhefs[['constant', 'qsmk']],
    weights=sw_AC[nhefs_all.censored == 0]
) 
res = wls.fit(cov_type='cluster', cov_kwds={'groups': nhefs.seqn})
```
## In summary
IP weighting creates a pseudo-population in which the distribution of the variables in L is the same in the treated and the untreated. Then, under the assumptions of exchangeability and positivity given L, we estimate <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a,c=0}]"> by simply computing <img src="https://render.githubusercontent.com/render/math?math=\bar{E}[Y|A=a,C=0]"> as the average outcome in the pseudo-population. If A were a continuous treatment, we would also need a structural model to estimate <img src="https://render.githubusercontent.com/render/math?math=\bar{E}[Y|A, C=0]"> in the pseudo-population for all possible values of A. 

