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
- To obtain parametric estimates of <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|L]"> in each of the millions of strata defined by L, we fit a logistic regression model for the A (**probability of quitting smoking**) with all L(**9 confounders**) included as covariates. 
- Computing the difference <img src="https://render.githubusercontent.com/render/math?math=\bar{E}_{ps}[Y|A=1] - \bar{E}_{ps}[Y|A=0]"> in the psuedo-population created by the estimated IP weights. Fit the linear mean model <img src="https://render.githubusercontent.com/render/math?math=E[Y|A] = theta{0} + theta{1}*A"> by weighted least squares, with individuals weighted by their estimated weights <img src="https://render.githubusercontent.com/render/math?math=\bar{W}">: 1/<img src="https://render.githubusercontent.com/render/math?math=\bar{Pr}[A=1|L]"> for quitters and 1/(1- <img src="https://render.githubusercontent.com/render/math?math=\bar{Pr}[A=1|L]">) for the non-quitters. The parameter estimates <img src="https://render.githubusercontent.com/render/math?math=\bar{theta}"> was 3.4. T
