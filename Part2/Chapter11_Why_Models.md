## 11.2 Parametric estimators of the conditional mean
A parametric conditional mean model is, through its a **priori restrictions**, adding information to compensate for the lack of sufficient information in the data, eg the linear regression. 

code: [Section 11.2 11.2 program](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter11.ipynb)
## 11.3 Nonparametric estimators of the conditional mean
A nonparametric estimators of the conditional mean function as those that produce estimates from the data **without any a priori restrictions** on the conditional mean function. 

**Santurated Models**
- Models which do not impose restriction on the distrubtion of the data are saturated models. 
- A saturated model has the same number of unknowns on both sides of the euqal sign.
- Eg.  <img src="https://render.githubusercontent.com/render/math?math=E[Y|A=a]"> for a dichotomous treatment

code: [Section 11.3](https://github.com/OrangeC93/Book_Causal_Inference_What_If/blob/main/code/chapter11.ipynb)
## 11.4 Smoothing
In realistic applications, models often include many different covariates so that the curves are really hyperdimensional surfaces. 

Regardless of the dimensionality of the problem, the concept of smoothing remains invariant: the **fewer parameters** in the model, the **smoother** the prediction (response) surface will be.

## 11.5 The bias-variance trade-off
Although less smooth models may yield a less biased estimate, they also result in a larger variance.

