## 11.2 Parametric estimators of the conditional mean
A parametric conditional mean model is, through its a **priori restrictions**, adding information to compensate for the lack of sufficient information in the data.

## 11.3 Nonparametric estimators of the conditional mean

A nonparametric estimators of the conditional mean function as those that produce estimates from the data **without any a priori restrictions** on the conditional mean function. Generally, the model is saturated whenever the number of parameters in a conditional mean model is equal to the number of unknown conditional means in the population.

All methods for causal inference that we described in Part I of this book–standardization, IP weighting, stratification, matching–were based on nonparametric estimators of population quantities under a saturated model because they did not impose any a priori restrictions on the value of the effect estimates.

## 11.4 Smoothing
In realistic applications, models often include many different covariates so that the curves are really hyperdimensional surfaces. Regardless of the dimensionality of the problem, the concept of smoothing remains invariant: the **fewer parameters** in the model, the **smoother** the prediction (response) surface will be.

## 11.5 The bias-variance trade-off
Although less smooth models may yield a less biased estimate, they also result in a larger variance.

