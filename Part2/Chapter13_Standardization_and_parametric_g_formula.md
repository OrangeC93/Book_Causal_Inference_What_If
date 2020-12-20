## 13.1 Standardization as an alternative to IP weighting
Our analyses will also be based on NHEFS data from 1629 cigarette smokers aged 25-74 years who had a baseline visit and a follow-up visit about 10 years later. Of these, 1566 individuals had their weight measured at the follow-up visit and are therefore uncensored (C = 0). The average causal effect of smoking cessation can be expressed as the difference <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1, c=0}] - E[Y^{a=0, c=0}]">, that is, the difference in mean weight that would have been observed if everybody had been treated and uncensored compared with untreated and uncensored.

Standardized mean in the uncensored who received treatment level a is <img src="https://render.githubusercontent.com/render/math?math=\sum_{l}E[Y|A=a, C=0, L=l] * Pr[L=l]">. If some of the variables in L are continuous, one needs to replace Pr[L=l] by the probability density function (PDF) <img src="https://render.githubusercontent.com/render/math?math=f_{L}[l]"> and the above sum becomes as integral.

## 13.2 Estimating the mean outcome via modeling
To obtain parametric estimates of <img src="https://render.githubusercontent.com/render/math?math=E[Y|A=a, C=0, L=l] "> in each of the millions of strata defined by L, we fit a linear regression model for the mean weight gain with treatment A and all 9 confounders in L included as covariates.

## 13.3 Standardizing the mean outcome to the confounder distribution
