## 3.1 Identifiability Conditions

1. Consistensy: the values of treatment under comparison correspond to well-defined interventions that, in turn, correspond to the versions of treatment in the data 
2. Excahngeability: the conditional probability of receiving every value of treatment, though not decided by the investigators, depends only on measured covariates L 
3. Positivity: the probability of receiving every value of treatment conditional on L is greater than zero, i.e., positive

If the analogy between observational study and conditionally randomized experiment happens to be correct, then we can use the method: IP weighting or standardization to identify causal effects from observational studies. We therefore refer to these conditions as identifiability conditions or assumptions.

## 3.2 Exchangeability
In marginal randomized experiments, the treated and the untreated are exchangeable because the treated, had they remained untreated, would have experienced the same average outcome as the untreated did, and vice versa. This so because randomization ensures that the independent predictors of the outcome are equally distributed between the treated and untreated.

On the other hand, an imbalance in the distribution of independent outcome predictors L between the treated and the untreated is expected by design in conditionally randomized experiments in which the probability of receiving treatment depends on L.

Note: The crucial question for the observational study is whether L is the only outcome predictor that is unequally distributed between the treated and the untreated.Investigators can use their expert knowledge to enhance the plausibility of the conditional exchangeability assumption. They can measure many relevant variables L(e.g., determinants of the treatment that are also independent outcome predictors), and then assume that conditional exchangeability is approximately true within the strata defined by the combination of all those variables L. Unfortunately, no matter how many variables are included in L, there is no way to test that the assumption is correct, which makes causal inference from observational data a risky task.

## 3.3 Positivity
We must ensure that there is a probability greater than zero–a positive probability–of being assigned to each of the treatment levels. This is the positivity condition.

## 3.4 Consistency: First, define the counterfactual outcome
Consistency means that the observed outcome for every treated individual equals her outcome if she had received treatment, and that the observed outcome for every untreated individual equals her outcome if she had remained untreated, that is <img src="https://render.githubusercontent.com/render/math?math=Y^{a}=Y"> for every individual with A = a. 

Ideally, the protocols of randomized experiments will precisely specify the treatment values a assigned to each individual, so that their counterfactual outcomes <img src="https://render.githubusercontent.com/render/math?math=Y^{a}"> are well defined.

Example: Suppose that a colleague of ours wishes to quantify the causal effect of obesity A at age 40 on the risk of mortality Y by age 50 in a certain population.
- What exactly is meant by “the risk if all individuals had been obese”? because there are many different ways in which an individual could have become obese at age 40.
- Even if our colleague were able to define the duration, recency, and intensity of obesity A = 1, other aspects of the intervention would also need to be specified. In particular, our colleague would need to specify how to intervene on body weight to ensure that each individual experiences treatment value A = 1. 
- Under what kind of circumstances and how to define the counterfactual outcome <img src="https://render.githubusercontent.com/render/math?math=Y^{a=1}">

```
The articulation of causal questions is contingent on domain expertise and informal judgment. What we view as a scientifically meaningful causal question at present may turn out to be viewed as too vague in the future after learning that finer components of the treatment affect the outcome and therefore the magnitude of the causal effect. Years from now, scientists will probably refine our obesity question in terms of cellular modifications which we barely understand at this time. Again, the term sufficiently well-defined treatment relies on expert consensus, which by definition changes over time. 

```
## 3.5 Consistency: Second, link counterfactuals to the observed data
Ill-defined treatments like “obesity” complicate the interpretation of causal effect estimates (previous section), but so do sufficiently welldefined treatments that are absent in the data (this section). Detecting a mismatch between the treatment values of interest and the data at hand requires a careful characterization of the versions of treatment that operate in the population.

## 3.6 The target trial
Even though it's hard to precisely know the causal effect from an observational study in whic h ill defined versions of treatment prevent a proper considration of exchageability and positivity in obervational studies. BUT observational data may still be useful by focusing on non-causal prediction, for which the concept of target trial does not apply. That obese individuals have a higher mortality risk than nonobese individuals means that obesity is a predictor of–is associated with– mortality. This is an important piece of information to identify individuals at high risk of mortality.
