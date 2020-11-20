## The structure of selection bias
An association created as a result of the process by which individuals are selected into the analysis is referred to as selection bias. But more generally, selection bias can be defined as the bias resulting from conditioning on the common effect of two variables, one of which is eithe the treatment or associated with the treatment, and the other is either the outcome of associated with the outcome. 
- Unlike confounding, this type of bias is (1) not due to the presence of common causes of treatment and outcome, and (2) can arise in both randomized experiments and observational studies. 
- Like confounding, selection bias is just a form of lack of exchangeability between the treated and the untreated. 

Examples:
- (8.1) A->Y->[C], A->[C]
  - Conditional on C will result in an assocation between A and Y. But due to **selection bias**, the association risk <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|A=1, C=0]/Pr[Y=1|A=0, C=0]">does not equal the risk ratio <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1}=1]/Pr[Y^{a=0}=1]">. If the analysis doesn't conditioned on the common effect (collider) C, then the only open path between A and Y would be due to the causal effect of A on Y, that is the assciation would be causation.
- (8.2) A->Y->C->[S], A->C, conditioning on a varaible S affected by the collider C also opens the path A->C<-Y.
- Both (8.1) and (8.2) depict examples of selection bias in which the bias arises because of conditioning on a common effect of treatment and outcome:(1) This bias arises regardless of whether there's an arrow from A to Y.
- More variance structure oselection bias (8.3 - 8.6)

## 8.2 Examples of selection bias
1. Differential loss to follow up: also reffered to as bias due to informative censoring.
2. Missing data bias, nonresponse bias: they are reluctant to provide information or because they miss study visits, regardless of the reasons why data on Y are missing, restricting the analysis to individuals with complete data C=0 may result in bias.
3. Healthy worker bias
4. Self selection bias, volunteer bias
5. Selction affected by treatment received before study entry: C represents selection into the study 1:no, 0:yes, treatment A took place befor the study started, if treatment affects the probability of being selected into the study, then selection bias is expected.

These examples show that selection bias may occur in retrospective studies as well as prospective studies. 

⭐ Hence a key difference between confounding and selection bias: ✅ randomization protects against confounding, but not against ❌ selection bias when the selection occurs **after** the randomization. On the other hand, no bias arises in randomized experiments from selection into the study before treatment is assigned. 

## 8.3 Selection bias and confounding
In this and the previous chapter, we describe two reasons why the treated and the untreated may not be exchangeable: (1) Confounding: the presence of common causes of treatment and outcome, and (2) Selection Bias: conditioning on common effects of treatment and outcome (or causes of them). 

Although some statistians use selection bias for both reasons, but we still recommend adopting a structural approach of classification of sources of non-exchangeability:
- The structure of the problem frequently guides the choice of analytical methods to reduce or avoid the bias.
- It could help study design.
- Selection bias resulting from conditioning on pre-treatment variables (e.g., being a firefighter) could explain why certain variables behave as “confounders” in some studies but not others.

## 8.4 Selection bias and censoring
(8.3) Y<-U->L->[C]<-A: is an example of selection bias that results from conditioning on the censoring variable C, which is a common effect of treatment A and a cause U of the outcome Y , rather than of the outcome itself. According to the rules of d-separation, conditioning on the collider C opens the path A->C<-L<-U->Y and thus association flows from treatment A to outcome Y.

If the censoring C is now viewed as a treatment, the goal of the analysis is to compute the causal effect of a joint intervention on A and C, To eliminate the selection bias for the effect of treatment A, we need to adjust for confounding for the effect of the treatment C.

## 8.5 How to adjust for selection bias
In the previous chapter, we have described IP weights to adjust for counfounding, <img src="https://render.githubusercontent.com/render/math?math=W^A = 1/f(A/L)"> and selection bias <img src="https://render.githubusercontent.com/render/math?math=W^C = 1/Pr(C=0|A,L)">. When both confounding and selection bias exist, the product weight <img src="https://render.githubusercontent.com/render/math?math=W^A"> <img src="https://render.githubusercontent.com/render/math?math=W^C"> can be used to adjust simultaneously for both biases under assumption describe in Chapter 12 and Part 3

Example: （8.3）
![image](/img/adjust_selection_bias_eg.png)
```
There are 20 individuals with heart disease (L = 1) who were assigned to wasabi supplementation (A = 1). 
Of these, 4 remained uncensored and 16 were lost to follow-up. 
That is, the conditional probability of remaining uncensored in this group is 1/5, Pr[C=0|L=1,A=1]=4/20=0.2. 
  16 censored individuals receive a zero weight (i.e., they do not contribute to the analysis).
  4 uncensored individuals receive a weight of 5, which is the inverse of their probability of being uncensored (1/5).
  IP weighting replaces the 20 original individuals by 5 copies of each of the 4 uncensored individuals.
```
Rather, one might attempt to remove selection bias by **stratification** (i.e., by estimating the effect measure conditional on the L variables) rather than by **IP weighting**. Stratification could yield unbiased conditional effect measures within levels because conditioning on L is sufficient to block the backdoor path from C to Y . That is, the conditional risk ratio:
 <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|A=1,C=0,L=l]/Pr[Y=1|A=0,C=0,L=l]"> can be interpreted as the effect of treatment among the uncensored with L = l. 
 
But sometimes, Stratification doesn't wokr in 8.4 and 8.6 because conditioning on L will opens the path from A to Y because L is a collider on that path. In cantrast, IP weighting appropriately adjusts for selection bias under Figures 8.3-8.6 because this approach is not based on estimating effect measures conditional on the covariates L, but rather on estimating unconditional effect measures after reweighting the individuals according to their treatment and their values of L.

## 8.6 Selection without bias
In summary, conditioning on a collider always induces an association between its causes, but this association could be restricted to certain levels of the common effect. In other words, it is theoretically possible that selection on a common effect does not result in selection bias when the analysis is restricted to a single level of the common effect. Collider stratification is not always a source of selection bias.

```
Conditioning on a collider can result in selection bias in theory but not always if the analysis is restricted to a single level of the common effect.
```
