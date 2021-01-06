## 13.1 Standardization as an alternative to IP weighting
Our analyses will also be based on NHEFS data from 1629 cigarette smokers aged 25-74 years who had a baseline visit and a follow-up visit about 10 years later. Of these, 1566 individuals had their weight measured at the follow-up visit and are therefore uncensored (C = 0). The average causal effect of smoking cessation can be expressed as the difference <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1, c=0}] - E[Y^{a=0, c=0}]">, that is, the difference in mean weight that would have been observed if everybody had been treated and uncensored compared with untreated and uncensored.

Main idea: under exchangeability and positivity conditional on the variables in L, the standardized mean outcome in the uncensored treated is a consistent estimator of the mean outcome if **everyone had been treated and had remained uncensored** <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1, c=0}]">.

Standardized mean in the uncensored who received treatment level a is <img src="https://render.githubusercontent.com/render/math?math=\sum_{l}E[Y|A=a, C=0, L=l]Pr[L=l]">. If some of the variables in L are continuous, one needs to replace <img src="https://render.githubusercontent.com/render/math?math=Pr[L=l]"> by the probability density function (PDF) <img src="https://render.githubusercontent.com/render/math?math=f_{L}[l]"> and the above sum becomes as integral.

## 13.2 Estimating the mean outcome via modeling
To obtain parametric estimates of <img src="https://render.githubusercontent.com/render/math?math=E[Y|A=a, C=0, L=l] "> in each of the millions of strata defined by L, we fit a linear regression model for the mean weight gain with treatment A and all 9 confounders in L included as covariates.

## 13.3 Standardizing the mean outcome to the confounder distribution
Steps: expansion of dataset, outcome modeling, prediction, and standardized by averaging.

- Expansion of Dataset: (add a product term AL to make the model saturated)
  - First block: same as the original dataset (Y, A, L, AL)
  - Second block: set value A to 0 (untreated) for all rows, delete the outcome for all individuals (Y, 0, L, 0)
  - Second block: set value A to 1 (treated) for all rows (Y, 1, L, L)

- Outcome modeling:
  - Use the first block(actual data) to fit a regression model for the mean outcome Y given A and L

- Prediction:
  - Use the parameter estimates from the first block to predict the outcome values for all rows in the second and third blocks
  - The predicted outcome values for the second block are the mean estimates for each combination of values of L and A = 0, and the predicted values for the third block are the mean estimates for each combinations of values of L and A = 1

- Averaging: we compute the average of all predicted values in the second block (precisely the standardized mean outcome in the untreated) and third block (precisely the standardized mean outcome in the treated)

- Confidence interval: use bootstrap to calculate the confidence interval on the previous estimate

## 13.4 IP weighting or standardization
- Large differences between the IP weighted and standardized estimate will alert us to the presence of serious model misspecification in at least one of the estimates. Small differences do not guarantee absence of serious model misspecification, but will be reassuring–though logically possible, it is unlikely that badly misspecified models resulting in bias of similar magnitude and direction for both methods.
- Often there is no need to choose between IP weighting and the parametric g-formula. When both methods can be used to estimate a causal effect, just use both methods. 
- Both IP weighting and standardization are estimators of the g-formula, a general method for causal inference first described in 1986. We say that standardization is a plug-in g-formula estimator because it simply replaces the conditional mean outcome in the g-formula by its estimates.

## 13.5 How seriously do we take our estimates?
Observational effect estimates are always open to serious crticism, the validity of our estimates for the target population requires many conditions: 
- First, the identifiability conditions of exchangeability, positivity, and consistency (Chapter 3) need to hold for the observational study to resemble the target trial.
- Second, all variables used in the analysis need to be correctly measured. Measurement error in the treatment A, the outcome Y , or the confounders L will generally result in bias (Chapter 9).
- Third, all models used in the analysis need to be correctly specified (Chapter 11).

Therefore a healthy skepticism of causal inferences drawn from observational data is necessary.

## Code Chapter 13 
Program 13.4: Use bootstrap to calculate causal effect and the confidence interval

``` python
boot_samples = []
common_X = [
    'one', 'sex', 'race', 'edu_2', 'edu_3', 'edu_4', 'edu_5', 
    'exercise_1', 'exercise_2', 'active_1', 'active_2',
    'age', 'age^2', 'wt71', 'wt71^2',
    'smokeintensity', 'smokeintensity^2', 'smokeyrs', 'smokeyrs^2'
]

for _ in range(2000):
    sample = nhefs.sample(n=nhefs.shape[0], replace=True)
    
    y = sample.wt82_71
    X = sample[common_X + ['qsmk', 'qsmk_x_smokeintensity']] ## add a product term to make the model saturated
    block2 = sample[common_X + ['zero', 'zero']] ## if every one is untreated
    block3 = sample[common_X + ['one', 'smokeintensity']] ## if every one is untreated
    
    result = sm.OLS(y, X).fit()
    
    block2_pred = result.predict(block2)
    block3_pred = result.predict(block3)
    
    boot_samples.append(block3_pred.mean() - block2_pred.mean())

std = np.std(boot_samples)

lo = est_diff - 1.96 * std
hi = est_diff + 1.96 * std

print('               estimate   95% C.I.')
print('causal effect   {:>6.1f}   ({:>0.1f}, {:>0.1f})'.format(est_diff, lo, hi))
```
