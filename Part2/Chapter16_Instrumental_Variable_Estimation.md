## 16.1 The three instrumental conditions
- Z is associated with A
- Z does not affect Y except through its potential effect on A
- Z and Y do not share causes

Example1: 

![image](/img/16_1.png)

Example2: 
- Uz is unmeasured causal instrument
- Z is the measured surrogate or proxy instrument
- Z and Y have Uz as a common cause does not violate condition(iii) since Uz is a caudal instrument
![image](/img/16_2.png)

Example3: 
- Z-A association arises from conditioning ona common effect S of the unmeasured causal instrument Uz and proxy instrument Z.
- Both causal and proxy instrument can be used for IV estimation

![image](/img/16_3.png)

Back to the example: the effect of smoking cessation on weight change
- There's no randomization indicator in an observational study
- Consider: the price of cigarettes, it can be argued if it can meet the three instumental conditions
- Propose an instrument Z that takes value 1 wthen the average price of a pack of cigarettes in the US states where the individual was bron was greater than $1.5 and takes 0 otherwise
  - We need to verify that the (i) proposed instrument Z and the treatment A are associated, <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|Z=1] - Pr[A=1|Z=0] =6%">, in this case, Z and A are wekly associated, Z is often referred as a weak instrument 
  - We can only assume conditions (ii) and (iii) are hold

## 16.2 The usual IV estimated
For a continuous instrument Z the usual IV estimand is Cov(Y, Z)/Cov(A, Z) , where Cov means covariance.

For a dichotomous variable Z is an instrument, <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1}]-E[Y^{a=0}]"> is identified and equals to 
<img src="https://render.githubusercontent.com/render/math?math=(E[Y|Z=1]-E[Y|Z=0])/E[A|Z=1]-E[A|Z=0]">

How to understand the IV estimand, the numerator of IV estimand is the intention to treat effect and the denominator is a measure of adherence. 
- When there's a perfect compliance, the denominator is to 1 and the effect of A on Y equals to the effect of Z on Y. 
- As compliance worsens, the denominator tarts to get closer to 0 and the effect of A on Y becomes greater than the effect of Z on Y. The greater the rate of noncompliance, the greater the difference between the effect of A on Y and the effect of Z on Y. 

One way simply calculating the four sample average or fit two saturated linear models to estimate the difference in the denominator and numerator <img src="https://render.githubusercontent.com/render/math?math=E(A|Z) = \alpha_{0} %2B \alpha_{1}Z">, <img src="https://render.githubusercontent.com/render/math?math=E(Y|Z) = \alpha_{0} %2B \alpha_{1}Z">.

Another way: two-stage-least squared estimator
- The point estimate has a very large confidence interval, which is expected for the proposed instument because Z-A association is week and there's much uncertainty in the 1st stage model. We usually declare an instrument as week if the F-statistic from 1st stage is less than 10.
- two-stage-least-sqares estimator has variations , like using additive or multiplicative structural mean models, or the parameters of structural mean models can be estimated via g-estimation. 


Code: [Program 16.1, Program 16.2, Program 16.3](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter16.ipynb)

## 16.3 A fourth identifying condition: homogeneity
## 16.4 An alternative forth condition: monotonity
## 16.5 The three instumental conditions revisited
## 16.6 Instrumental variable estimation vs other methods
1. IV requires more modeling assumptions even if infinite data were available
2. Relatively minor violations of condition for IV may result in large biased of unpredictable or counterintuitive direction
3. The ideal setting for IV is more restrictive
