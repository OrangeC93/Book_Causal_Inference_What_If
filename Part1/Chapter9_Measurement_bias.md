## Measurement error

## 9.2 The structure of measurement error
<img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y

- The true treatment A affects both the outcome Y and the measured treatment <img src="https://render.githubusercontent.com/render/math?math=A^{*}">. 
- Node <img src="https://render.githubusercontent.com/render/math?math=U_A"> represent all factors other than A that determin the value of <img src="https://render.githubusercontent.com/render/math?math=A^{*}">, we refer to <img src="https://render.githubusercontent.com/render/math?math=U_{A}"> as the measurement error for A. Note, they are in unnecessary in discussion of confounding or selection bias

<img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y -> <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> <- <img src="https://render.githubusercontent.com/render/math?math=U_Y">

- Then there is no guarantee that the measure of association between <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> and <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> will equal the measure of causal effect of A on Y.

- We say that there is measurement bias or information bias. In the presence of measurement bias, the identifiability conditions of exchangeability, positivity, and consistency are insufficient to compute the causal effect of treatment A on outcome Y.
