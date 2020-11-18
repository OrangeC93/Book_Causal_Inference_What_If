## The structure of selection bias
An association created as a result of the process by which individuals are selected into the analysis is referred to as selection bias. 
- Unlike confounding, this type of bias is not due to the presence of common causes of treatment and outcome, and can arise in both randomized experiments and observational studies. 
- Like confounding, selection bias is just a form of lack of exchangeability between the treated and the untreated. This

Examples:
- (8.1) A->Y->[C], A->[C]
  - Conditional on C will result in an assocation between A and Y. But due to **selection bias**, the association risk <img src="https://render.githubusercontent.com/render/math?math=Pr[Y=1|A=1, C=0]/Pr[Y=1|A=0, C=0]">does not equal the risk ratio <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1}=1]/Pr[Y^{a=0}=1]">. If the analysis doesn't conditioned on the common effect (collider) C, then the only open path between A and Y would be due to the causal effect of A on Y, that is the assciation would be causation.
- (8.2) A->Y->C->[S], A->C, conditioning on a varaible S affected by the collider C also opens the path A->C<-Y.
