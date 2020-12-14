## 9.1 Measurement error
(9.1) <img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y

- The true treatment A affects both the outcome Y and the measured treatment <img src="https://render.githubusercontent.com/render/math?math=A^{*}">. 
- Node <img src="https://render.githubusercontent.com/render/math?math=U_A"> represent all factors other than A that determin the value of <img src="https://render.githubusercontent.com/render/math?math=A^{*}">, we refer to <img src="https://render.githubusercontent.com/render/math?math=U_{A}"> as the measurement error for A. Note, they are in unnecessary in discussion of confounding or selection bias

(9.2) <img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y -> <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> <- <img src="https://render.githubusercontent.com/render/math?math=U_Y">

- Then there is no guarantee that the measure of association between <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> and <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> will equal the measure of causal effect of A on Y.

- We say that there is measurement bias or information bias. In the presence of measurement bias, the identifiability conditions of exchangeability, positivity, and consistency are insufficient to compute the causal effect of treatment A on outcome Y.

## 9.2 The structure of measurement error
The structure of measurement error can be classified into two properties: independence and nondifference. 

- ✅ independent
  - In (9.2), according to the rules of d-separation, the measurement errors <img src="https://render.githubusercontent.com/render/math?math=U_A"> and <img src="https://render.githubusercontent.com/render/math?math=U_Y"> are **independent** because the path between them is blocked by colliders.

- ✅ nondifferential
(9.3) <img src="https://render.githubusercontent.com/render/math?math=U_{AY}"> -> <img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y -> <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> <- <img src="https://render.githubusercontent.com/render/math?math=U_Y"> <- <img src="https://render.githubusercontent.com/render/math?math=U_{AY}"> 
  - Both figures 9.2 and 9.3 represent settings in which the error for treatment <img src="https://render.githubusercontent.com/render/math?math=U_A"> is independent of the true value of the outcome Y, and the error for the outcome <img src="https://render.githubusercontent.com/render/math?math=U_Y"> is independent of the true value of treatment A, we then say the measurement error for the treatment is **nondifferential** with respect to the outcome, and that the measurement error for the outcome is nondifferential with respect to the treatment.

- ✅ independent differential (9.4) <img src="https://render.githubusercontent.com/render/math?math=U_A"> -> <img src="https://render.githubusercontent.com/render/math?math=A^{*}"> <- A -> Y -> <img src="https://render.githubusercontent.com/render/math?math=Y^{*}"> <- <img src="https://render.githubusercontent.com/render/math?math=U_Y">, A-> <img src="https://render.githubusercontent.com/render/math?math=U_Y"> 
  - Figure 9.4 shows an example of independent but differential measurement error in which the true value of the outcome affects the measurement of the treatment.

- dependent differential
  - Figures 9.6 and 9.7 depict measurement errors that are both dependent and differential, which may result from a combination of the settings described above.

Realistic causal diagrams need to simultaneously represent biases arising from confounding, selection, and measurement. The best method to fight bias due to mismeasurement is, obviously, to improve the measurement procedures.

## 9.3 Mismeasured confounders
(9.8) <img src="https://render.githubusercontent.com/render/math?math=L^{*}<-L->A->Y, L->Y">
- Investigators had data on the mismeasured variable <img src="https://render.githubusercontent.com/render/math?math=L^{*}"> rather than on the variable L. Unfortunately, the backdoor path A<-L->Y cannot be generally blocked by conditioning on <img src="https://render.githubusercontent.com/render/math?math=L^{*}">. The standardized or IP weighted risk ratio based on <img src="https://render.githubusercontent.com/render/math?math=L^{*}">, Y and A will generally differ from the cxausal risk ratio <img src="https://render.githubusercontent.com/render/math?math=Pr[Y^{a=1}=1]/Pr[Y^{a=0}=1]">. 

(9.9) <img src="https://render.githubusercontent.com/render/math?math=L^{*}<-L->A->Y, L<-U->Y">

- The causal diagram in Figure 9.9 shows an example of confounding of the causal effect of A on Y in which L is not the common cause shared by A and Y . Here too mismeasurement of L leads to measurement bias because the backdoor path A<-L<-U->Y cannot be generally blocked by conditioning on <img src="https://render.githubusercontent.com/render/math?math=L^{*}">.

Mismeasurement of confounders may also result in apparent **effect modification**. 

(9.10) A->Y->C-><img src="https://render.githubusercontent.com/render/math?math=C^{*}">, A->C
- It is also possible that a **collider C** is measured with error as represented in Figure 9.10. In this setting, conditioning on the mismeasured collider <img src="https://render.githubusercontent.com/render/math?math=L^{*}"> will generally introduce selection bias because <img src="https://render.githubusercontent.com/render/math?math=L^{*}"> is a common effect of the treatment A and the outcome Y .

## 9.4 Intention-to-treat effect: the effect of a misclassified treatment

