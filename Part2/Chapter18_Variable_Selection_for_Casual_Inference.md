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



