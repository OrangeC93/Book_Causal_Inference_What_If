## 15.1 Outcome regression
We have described IP weighting, standardization, and g-estimation to estimate the average causal effect of smoking cessation (the treatment) A on weight gain (the outcome) Y . We also described how to estimate the average causal effect within subsets of the population, either by restricting the analysis to the subset of interest or by adding product terms in marginal structural models (Chapter 12) and structural nested models (Chapter 14). 
- Structural nested models: These models include parameters for the product terms between treatment A and the variables L, but no parameters for the variables L themselves. This is an attractive property of structural nested models because we are interested in the causal effect of A on Y within levels of L but not in the (noncausal) relation between L and Y . A method– g-estimation of structural nested models–that is agnostic about the functional form of the L-Y relation is protected from bias due to misspecifying this relation.
- Structural model <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a,c=0}|L]=\beta _{0}%2B\beta _{1}a%2B\beta_{2}aL%2B\beta_{3}L"> where <img src="https://render.githubusercontent.com/render/math?math=\beta_{2}"> and <img src="https://render.githubusercontent.com/render/math?math=\beta_{3}"> are vector parameters. The average causal effects of smoking cessation A on weight gain Y in each stratum of L are a function of <img src="https://render.githubusercontent.com/render/math?math=\beta_{1}"> and <img src="https://render.githubusercontent.com/render/math?math=\beta_{2}">, the mean counterfactual outcomes under no treatment in each stratum of L are a function of <img src="https://render.githubusercontent.com/render/math?math=\beta_{0}"> and <img src="https://render.githubusercontent.com/render/math?math=\beta_{3}">. The parameter <img src="https://render.githubusercontent.com/render/math?math=\beta_{3}"> is usually referred as the main effect of L, but the use of the word effect is misleading because <img src="https://render.githubusercontent.com/render/math?math=\beta_{3}"> may not have an interpretation as the causal effect of L (there may be confounding for L). The parameter <img src="https://render.githubusercontent.com/render/math?math=\beta_{3}"> simply quantifies how the mean of the counterfactual <img src="https://render.githubusercontent.com/render/math?math=Y^{a=0, c=0}"> varies as a function of L.

## 15.2 Propensity scores
Propensity score: π(L) measures the propensity of individuals to receive treatment A given the information available in the covariates L. If the distribution of π(L) were the same for the treated A = 1 and the untreated A = 0, then there would be no confounding due to L, i.e., there would be no open path from L to A on a causal diagram. Under exchangeability and positivity within levels of the propensity score π(L), the propensity score can be used to estimate causal effects using stratification (including outcome regression), standardization, and matching.

 ## 15.3 Propensity stratification and standardization
When our parametric assumptions for <img src="https://render.githubusercontent.com/render/math?math=E[Y|A,C=0, π(L)]"> are correct, plus exchangeability and positivity hold, the model estimates the average causal effects within all levels s of the propensity score <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1, c=0}|π(L)=s] - E[Y^{a=0, c=0}|π(L)=s]">. 

If we were interested in the average causal effect in the entire study population <img src="https://render.githubusercontent.com/render/math?math=E[Y^{a=1, c=0}] - E[Y^{a=0, c=0}]">, we would standardize the conditional means <img src="https://render.githubusercontent.com/render/math?math=E[Y|A,C=0, π(L)]"> by using the distribution of propensity score. The procedure is the same one described in Chapter 13 for continuous variables, except that we replace the variables L by the estimated π(L). Note that the procedure can naturally incorporate a product term between treatment A and the estimated π(L) in the outcome model. 

## 15.4 Propensity matching
There are many forms of propensity matching. All of them attempt to form a matched population in which the treated and the untreated are exchaneable because they have the same distribution of π(L).
- For example, one can match the untreated to the treated: each treated individual is paired with one (or more) untreated individuals with the same propensity score value. The subset of the original population comprised by the treated-untreated pairs (or sets) is the **matched population**.
- Other than exact match, a common approach is to define a closeness in propensity matching, which entails a bias-variance trade-off. If the closeness is too loose, the distribution of π(L) will differ between the treated and the untreated in the matched population, exchangeability fill not hold. On the other hand, exchangeability might be held but effect estimate may have wider 95% confidence intervals.
- Matching does not distinguish between random and structural nonpositivity.
- Propensity may yield a hard-to-describe subset of the study population in practice. 

## 15.5 Propensity models, structural models, predictive models
Propensity models: Propensity models are models for the probability of treatment A given the variables L used to try to achieve conditional exchangeability.

Structural models: Structural models describe the relation between the treatment A and some component of the distribution (e.g., the mean) of the counterfactual outcome <img src="https://render.githubusercontent.com/render/math?math=Y^{a}">, either marginally or within levels of the variables L.
- Marginal structural models: include parameters for treatment A, for the variables V that may be effect modifiers, and for product terms between treatment A and variables V.
  - If no covariates V are included, then the model is truly marginal.
  - If all variables L are included as possible effect modifiers then the marginal structural model becomes a faux marginal structural model.
- Structural nested models: include parameters for treatment and for product terms between treatment A and all variables in L that are effect modifiers.

## Code Chapter 15
```python
formula = (
    'qsmk ~ sex + race + age + I(age**2) + C(education)'
    '     + smokeintensity + I(smokeintensity**2) + smokeyrs + I(smokeyrs**2)'
    '     + C(exercise) + C(active) + wt71 + I(wt71**2)'
) ## no product term

model = sm.Logit.from_formula(formula, data=nhefs_all) 
res = model.fit(disp=0)

propensity = res.predict(nhefs_all)
nhefs['propensity'] = propensity[~nhefs_all.wt82_71.isnull()]

model = sm.OLS.from_formula('wt82_71 ~ qsmk + propensity', data=nhefs)
res = model.fit()
res.summary().tables[1]


def outcome_regress_effect(data):
    model = sm.OLS.from_formula('wt82_71 ~ qsmk + propensity', data=data)
    res = model.fit()
    
    data_qsmk_1 = data.copy()
    data_qsmk_1['qsmk'] = 1
    
    data_qsmk_0 = data.copy()
    data_qsmk_0['qsmk'] = 0
    
    mean_qsmk_1 = res.predict(data_qsmk_1).mean()
    mean_qsmk_0 = res.predict(data_qsmk_0).mean()
    
    return mean_qsmk_1 - mean_qsmk_0
    
def nonparametric_bootstrap(data, func, n=1000):
    estimate = func(data)
    
    n_rows = data.shape[0]
    indices = list(range(n_rows))
    
    b_values = []
    for _ in tqdm(range(n)):
        data_b = data.sample(n=n_rows, replace=True)
        b_values.append(func(data_b))
    
    std = np.std(b_values)
    
    return estimate, (estimate - 1.96 * std, estimate + 1.96 * std)
    
data = nhefs[['wt82_71', 'qsmk', 'propensity']]
info = nonparametric_bootstrap(
    data, outcome_regress_effect, n=2000
)


print('         estimate   95% C.I.')
print('effect    {:>5.1f}    ({:>0.1f}, {:>0.1f})'.format(info[0], info[1][0], info[1][1]))
```
