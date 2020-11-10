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
## 3.5 Consistency: Second, link counterfactuals to the observed data
## 3.6 The target trial
