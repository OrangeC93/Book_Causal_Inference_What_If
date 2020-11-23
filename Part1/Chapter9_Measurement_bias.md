## 9.1 Measurement error
(9.1) <img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y

- The true treatment A affects both the outcome Y and the measured treatment <img src="https://render.githubusercontent.com/render/math?math=A^{*}">. 
- Node <img src="https://render.githubusercontent.com/render/math?math=U_A"> represent all factors other than A that determin the value of <img src="https://render.githubusercontent.com/render/math?math=A^{*}">, we refer to <img src="https://render.githubusercontent.com/render/math?math=U_{A}"> as the measurement error for A. Note, they are in unnecessary in discussion of confounding or selection bias

(9.2) <img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y -> <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> <- <img src="https://render.githubusercontent.com/render/math?math=U_Y">

- Then there is no guarantee that the measure of association between <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> and <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> will equal the measure of causal effect of A on Y.

- We say that there is measurement bias or information bias. In the presence of measurement bias, the identifiability conditions of exchangeability, positivity, and consistency are insufficient to compute the causal effect of treatment A on outcome Y.

## 9.2 The structure of measurement error
The structure of measurement error can be classified into two properties: independence and nondifference. 

- ✅✅ independent nondifferential
  - In (9.2), according to the rules of d-separation, the measurement errors <img src="https://render.githubusercontent.com/render/math?math=U_A"> and <img src="https://render.githubusercontent.com/render/math?math=U_Y"> are **independent** because the path between them is blocked by colliders.

- ✅ dependent nondifferential
(9.3) <img src="https://render.githubusercontent.com/render/math?math=U_{AY}"> -> <img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y -> <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> <- <img src="https://render.githubusercontent.com/render/math?math=U_Y"> <- <img src="https://render.githubusercontent.com/render/math?math=U_{AY}"> 
  - Both figures 9.2 and 9.3 represent settings in which the error for treatment <img src="https://render.githubusercontent.com/render/math?math=U_A"> is independent of the true value of the outcome Y, and the error for the outcome <img src="https://render.githubusercontent.com/render/math?math=U_Y"> is independent of the true value of treatment A, we then say the measurement error for the treatment is **nondifferential** with respect to the outcome, and that the measurement error for the outcome is nondifferential with respect to the treatment.
- ✅ independent differential
  - Figure 9.4 shows an example of independent but differential measurement error in which the true value of the outcome affects the measurement of the treatment.
- dependent differential
  - Figures 9.6 and 9.7 depict measurement errors that are both dependent and differential, which may result from a combination of the settings described above.

