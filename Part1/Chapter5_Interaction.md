## 5.1 Interaction requires a joint intervention
Interventions on two or more treatments as joint interventions.
There is interaction between A and E on the additive scale in the population if <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1, e=1} = 1] - Pr[Y^{a=0, e=1} = 1] \neq Pr[Y^{a=1, e=0} = 1] - Pr[Y^{a=0, e=0} = 1]"> also equivalently <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1, e=1} = 1] - Pr[Y^{a=1, e=0} = 1] \neq Pr[Y^{a=0, e=1} = 1] - Pr[Y^{a=0, e=0} = 1]">

Note: The difference beween interaction and effect modification
- A variable V is a modifier of the effect of A on Y when the average causal effect of A on Y varies across levels of V, only invloves the conterfactual outcomes <img src="https://render.githubusercontent.com/render/math?math=Y^{a}">. 
- But the definition of interaction between A and E gives equal status to both treatments A and E, thus involves the counterfactual outcomes <img src="https://render.githubusercontent.com/render/math?math=Y^{a,e}">

## 5.2 Identifying interaction
- Suppose E are randomly and unconditionally assigned by the investigators, the positivity and consistency hold and the E = 1 or E = 0 are expected to be exchangeable, formally the marginal risk  <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1, e=1}=1]">is euqal to the conditional risk  <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1} = 1 | E=1]">, which conincide with the concept of effect modification.
- Suppose treatment E was not assigned by investigators. To assess the presence of interaction between A and E, one still needs to compute the four marginal risks <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a,e} = 1]">

## 5.3 Counterfactual response types and interaction 
The meaning of the term “interaction” is clarified by the classification of individuals according to their counterfactual response types (More details in book).

## 5.4 Sufficient causes
There are 9 possible sufficient causes with treatment components A = 1 only, A = 0 only, E = 1 only, E = 0 only, A = 1 and E = 1, A = 1 and E = 0, A = 0 and E = 1, A = 0 and E = 0, and neither A nor E matter. Each of these sufficient causes includes a set of background factors from U1,..., U8 and U0.

![image](/img/sufficient_component_causes.png)
## 5.5 Sufficient cause interaction
This 2nd concept of interaction is not based on counterfactual contrasts but rather on sufficient-component causes, and thus we refer to it as interaction within the sufficient-component-cause framework or, for brevity, **sufficient cause interaction**.

A sufficient cause interaction between A and E exists in the population if A and E occur together in a sufficient cause. Sufficient cause interactions can be synergistic or antagonistic:
- Synergism between treatment A and treatment E when A = 1 and E = 1 are present in the same sufficient cause.
- Antagonism between treatment A and treatment E when A = 1 and E = 0 (or A = 0 and E = 1) are present in the same sufficient cause.

## 5.6 Counterfactuals or sufficient-component causes
The counterfactual approach addresses the question “what happens?” The sufficient-component-cause approach addresses the question “how does it happen?”

To estimate causal effects more generally, the counterfactual framework will likely continue to be the one most often employed.
