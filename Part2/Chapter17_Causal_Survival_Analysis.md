## Harzards and risks
The administrative end of follow-up: most follow-up studies have a date after which there is no information on any individuals.


For example: Of the 1629 individuals, only 318 individuals died before the end of 1992 (the administrative end of follow up), so the survival time of the remaining 1311 individuals is administratively censored.

Administrative censoring is a problem instrinct to survial analyses, but it is not the only type of ce soring that may occur in survival analyses, there're also non-administrative types of censoring, such as loss to follow (e.g.,drop from the study) and competing events. We could adjust for the selection bias introduced via standardization or IP weighting. 

Example: the month of death T can take values subsequent from 1 (January 1983) to 120 (December 1992). T is known for 102 treated (A = 1) and 216 untreated (A = 0) individuals who died during the follow-up, and is administratively censored (that is, all we know is that it is greater than 120 months) for the remaining 1311 individuals.

In survival analysis we need to use other measures that can accommodate administrative censoring. Some common measures are the survival probability, the risk, and the hazard.
- Risk: the proportion of individuals who survived through time K. The denominator of the risk–the number of individuals at baseline–is constant across times k and its numerator–all events between baseline and k–is cumulative. That is, the risk will stay flat or increase as k increases.
- Harzard: at any time k, we can also calculate the proportion of individuals who develop the event among those who had not developed it before k. The denominator of the hazard–the number of individuals alive at k–varies over time t and its numerator includes only recent events–those during interval k. That is, the hazard may increase or decrease over time. Technically, this's the discrete intervals as opposed to measured continously.

## 17.2 From hazard to risk
The new dataset: (1)each row of the database corresponds to a person-time, the 1st row contains the informtion for person1 at k=0, etc. (2) define a time-varying indicator of event Dk, for each person at each month k, the indicator Dk takes value 1 if T<=k and 0 if T>k. 

![image](/img/lr_harzard.png)

- <img src="https://render.githubusercontent.com/render/math?math=\theta_{0,k}"> is a time-varying intercept that can be estimated by some flexible function of time such as <img src="https://render.githubusercontent.com/render/math?math=\theta_{0,k} = \theta_{0} %2B + \theta_{4}k %2B \theta_{5}k^{2}">
- The flexible time-varying treatment A and the product terms between treatment and time allow the harzard ratio to vary over time. 

Code: [Program 17.2](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter17.ipynb)
