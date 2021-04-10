## 18.1 The differenct goals of variable selection

When an association measure between a treatment and an outcome  may be partly or fully explained by confounders, adjustment for these confounders needs to be incorporated into the data analysis. Otherwise, the association measure cannot be interpreted as a causal effect measure.

## 18.2 Variables that induce or amplify bias
**Selection bias under the null**

![image](/img/18_1.png)

A-Y association adjusted for L is expected to be non-null even though the causal effect of treatment A on the outcome Y is null.

Or when L is a descendant of the collider B

![image](/img/18_2.png)



**Selection bias under the alternative or off the null**

![image](/img/18_3.png)

adjusting for L in Figure 18.3 results in selection bias only when A has a nonnull causal effect on Y


**Overadjustment for mediators**

![image](/img/18_4.png)

The A-Y association adjusted for the mediator L, or its descendants, will differ from the effect of treatment A on the outcome Y because the adjustment blocks the component of the effect that goes through L.

**In summary:**

The bias-inducing variables discussed above share a common feature: they are affected by treatment and therefore they are post-treatment variables. One might then think that we should always avoid adjustment for variables that occur after treatment .

However

![image](/img/18_5.png)

The variable K is a post-treatment variable, but it can be used to block the backdoor path Figure 18.5 between treatment A and outcome Y . Therefore, the A-Y association adjusted for L is an unbiased estimator of the effect of A on Y , whereas the unadjusted A-Y association is a biased estimator. The take home message is that causal graphs do not care about temporal order. Thus, when A does not affect L, the analysis must be the same whether L is temporally before or temporally after A.

**Adjustment for variables L that are temporally prior to treatment A**

![image](/img/18_6.png)

**bias amplification**

![image](/img/18_7.png)

That is, the A-Y association adjusted for Z may be further from Bias amplification is guaranteed if the effect of A on Y than the A-Y association not adjusted for Z. Z chould be used as instrumeental variables.


## 18.3 Causal Inference and machien learning
Our next problem is to estimate the causal effect in practice when X is very high-dimensional. 

Depending on the adjustment method that we choose, the variables X will be used in different ways. When using the plug-in g-formula (standardization), we will estimate the mean outcome Y conditional on the variables X, which we refer to as b(x); when using IP weighting, we will estimate the probability of treatment A conditional on the variables X, which we refer to as π(x). We can produce estimates b(x) and π(x) via the sort of parametric models (e.g., linear and logistic regression) that we have described in Part II of this book.



But the use of predictive machine learning algorithms(lasso, tree, deeplearning etc..) to estimate b(x) and π(x) raises two serious concerns.
- Firstly, machine learning do not guarantee that the selected variables will eliminate counfouding
- Secondly, machine learning are statistical black boxes with largely unknown statistical properties, even if a doubly robust estimator is unbiased, the variance of the resulting estimate may be wrong. 

Thus, the use of doubly robust estimators is key to combining causal inference with machine learning, but it is not sufficient.



## 18.4 Doubly robust machine learning estimators
The doubly robust estimator needs to incorporate two procedures, **sample splitting** and **ross-fitting**.

Sample slitting: 
- Split into two halves: an estimation sample and a training sample
- Apply predictive algorithm to the training sample to obtain esimators of b(x) and π(x) for conditional expectations of outcome and treatment
- Compute the doubly robust estimaotr of the average causal effect in the estimation sample using the 
b(x) and π(x) 


As a result, our confidence interval will be wider than the one we would have obtained if we had been able to use the entire sample of n individuals. A way to overcome this problem is cross-fitting.

Cross fitting:
- Repeat the procedutre but swapping the roles of the estimation and training halves of the study population
- Compute the average of the two doubly robust estimates from each half of the population. This average will be our doubly robust estimate of the effect in the entire study population. A 95% confidence interval around this estimate can be constructed by bootstrapping, either by adding and subtracting 1.96 times the bootstrap standard error or by using the 2.5 and 97.5 percentiles of the bootstrap estimates as the bounds of the interval


## 18.3 Variable selection is a difficult problem 
Suppose that we obtain a doubly robust machine learning estimate of the causal effect, as described in the previous section, only to find out that its (correct) variance is too big to be useful.
Since we do not like very wide 95% confidence intervals, even if they are correct, we may be tempted to throw out the variables in X that are causing the “problem” and then repeat the data analysis. Using the data to discard covariates in X that are associated with treatment, but not so much with the outcome, makes it no longer possible to guarantee that the 95% confidence interval around the effect estimate is valid.



The tension between including all potential confounders to eliminate bias and excluding some variables to reduce the variance is hard to resolve.

