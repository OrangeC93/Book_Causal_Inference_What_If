## 17.1 Harzards and risks
The administrative end of follow-up: most follow-up studies have a date after which there is no information on any individuals.
- Example: the month of death T can take values subsequent from 1 (January 1983) to 120 (December 1992). T is known for 102 treated (A = 1) and 216 untreated (A = 0) individuals who died during the follow-up, and is administratively censored (that is, all we know is that it is greater than 120 months) for the remaining 1311 individuals.
  - Survival curves code: [Program 17.1](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter17.ipynb)

Administrative censoring is a problem instrinct to survial analyses, but it is not the only type of ce soring that may occur in survival analyses, there're also non-administrative types of censoring, such as loss to follow (e.g.,drop from the study) and competing events. We could adjust for the selection bias introduced via standardization or IP weighting. 

In survival analysis we need to use other measures that can accommodate administrative censoring. Some common measures are the survival probability, the risk, and the hazard.
- Risk <img src="https://render.githubusercontent.com/render/math?math=Pr[T>k]">: the proportion of individuals who survived through time K, the risk will stay flat or increase as k increases.
  - The denominator: the number of individuals at baseline, which is constant across times k 
  - The numerator: all events between baseline and k, which is cumulative. 
- Harzard <img src="https://render.githubusercontent.com/render/math?math=Pr[T=k|T>k-1]">: at any time k, calculate the proportion of individuals who develop the event among those who had not developed it before k. The hazard may increase or decrease over time. Technically, this's the discrete intervals as opposed to measured continously.  
  - The denominator: the number of individuals alive at k–varies over time t
  - The numerator: includes only recent events–those during interval k

## 17.2 From hazard to risk
To parametricdally estimate the hazard is to fit a logitic rgression for <img src="https://render.githubusercontent.com/render/math?math=Pr[D_{k}=1|D_{k-1}=0]">, that, at each k, is restricted to individuals who survived through k.

The new dataset called person-time data formmat: (1)each row of the database corresponds to a person-time, the 1st row contains the informtion for person1 at k=0, etc. (2)define a time-varying indicator of event <img src="https://render.githubusercontent.com/render/math?math=D_{k}">, for each person at each month k, the indicator <img src="https://render.githubusercontent.com/render/math?math=D_{k}"> takes value 1 if T<=k and 0 if T>k. 

![image](/img/lr_harzard.png)

- <img src="https://render.githubusercontent.com/render/math?math=\theta_{0,k}"> is a time-varying intercept that can be estimated by some flexible function of time such as <img src="https://render.githubusercontent.com/render/math?math=\theta_{0,k} = \theta_{0} %2B + \theta_{4}k %2B \theta_{5}k^{2}">
- The flexible time-varying treatment A and the product terms between treatment and time allow the harzard ratio to vary over time. 

Code: [Program 17.2](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter17.ipynb)

## 17.3 Why censoring matters
Define a time-varying indicator <img src="https://render.githubusercontent.com/render/math?math=C_{k}"> for censoring by time k. For each person at each month k, the indicator <img src="https://render.githubusercontent.com/render/math?math=C_{k}"> takes value 0 if the administrative end of follow-up is greater than k and takes value 1 otherwise.

Under randomly assigned censoring, the survival at k is <img src="https://render.githubusercontent.com/render/math?math=\sum_{m=1}^kPr[D_{m}=0|D_{m-1}=0, C_{m}=0, A=a]"> for <img src="https://render.githubusercontent.com/render/math?math=k"> < <img src="https://render.githubusercontent.com/render/math?math=k_{end}">, the estimation procedure is th same as described above (1) use a nonparametric estimate of or (2) fit a logistic model for, the cause-specific hazard <img src="https://render.githubusercontent.com/render/math?math=Pr[D_{k%2B1}=0|D_{k}=0, C_{k%2B1}=0, A=a]">

## 17.4 IP weighting of marginal structurdal models
Firstly, estimate the stablized IP weight <img src="https://render.githubusercontent.com/render/math?math=SW_{A}"> for each individual in the study population, in which the variables in L are independent from the treatment A, which eliminates confounding by those variables. 

Second, using person-time data formate, fit a hazards model that individuals are weighted by the estimated weights.

In our example, L includes the variables sex, age, race, education, intensity and duration of smoking, physical activity in daily life, recreational exercise, and weight. The 120-month survival estimates were 80.7% under smoking cessation and 80.5% under no smoking cessation; difference 0.2% (95% confidence interval from −4.1% to 3.7% based on 500 bootstrap samples). That is, after adjustment for the covariates  via IP weighting, we found little evidence of an effect of smoking cessation on mortality at any time during the follow-up.


Code: [Program 17.3](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter17.ipynb)

## 17.5 The parametric g-formula, standardization
First, estimate the conditional survivals <img src="https://render.githubusercontent.com/render/math?math=Pr[D_{k+1}=0|L=l, A=a]"> with the variables in L as covariates using our administratively censored data. 

Second, compute their weighted average over all values l of the covariates L.

In our example, the 120- month survival estimates were 80.4% under smoking cessation and 80.6% under no smoking cessation; difference 02% (95% confidence interval from −4.6% to 4.1%). That is, after adjustment for the covariates L via standardization, we found little evidence of an effect of smoking cessation on mortality at any time during the follow-up.

Code: [Program 17.4](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter17.ipynb)
## 17.6 G-estimation of structural nested models
Code: [Program 17.5](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter17.ipynb)
