# 1. Introduction to Difference-in-Differences
## Why DiD?
- **No need for exogeneous treatment assignment!**
    - Selection on unobservables is allowed
    - Time trend is allowed.
- **All that matters is PT.**
- DiD estimator = time difference + group difference
    - Selection issue and trend are all captured.

## 2x2 DiD setup
- 2 groups
    - $G=2$: Treated at period 2
    - $G = \infty$: Untreated by periods 2
- 2 time periods
    - $t=1$: Before treatment
    - $t=2$: After treatment
- The canonical 2×2 DiD estimator: 
    - $\widehat{\theta}_n^{DiD} =\left( \overline{Y}_{g=2, t=2} - \overline{Y}_{g=2, t=1}\right) - \left( \overline{Y}_{g=\infty, t=2} - \overline{Y}_{g=\infty, t=1}\right)$

## Potential outcomes and assumptions
- Treatment effect: $Y_{i,t}(2) - Y_{i,t}(\infty)$
    - TE is about individual level; in DiD, we focus on ATT.
- How to find TE?
    - Assume no heterogeneity: Constant treatment effect across units and times (+ no-anticipation) $\implies$ PO = observed data.
    - **However, causal inference is all about heterogeneity!**
- Assumptions are in the next lecture.

## Causal Parameters of Interest
- 2x2 DiD setup:
    - $ATT = \mathbb{E}[Y_{i,t=2}(2) - Y_{i,t=2}(\infty) \mid G_i = 2] $: We are missing one counterfactual; $Y_{i,t=2}(\infty)$ for $G_i = 2$.
    - $ATU$: We are missing one counterfactual
    - $ATE$: We are missing two (all) counterfactualss
- General setup:
    - $ATT(g,t)$: We are missing one counterfactual; $Y_{i,t}(\infty)$ for $G_i = g$.
    - $ATT(g^\prime,g,t\mid g^*)$: We are missing two counterfactuals; $Y_{i,t}(g)$ and $Y_{i,t}(g^\prime)$  for $G_i = g^*$.

## Note:
- [Fernando's note on 2x2 $\neq$ TWFE](https://friosavila.github.io/playingwithstata/main_jwdid.html)

---
# 2. Classical 2x2 DiD Setup (Part 1)
## Assumptions (identification) in DiD
- SDO $\implies$ selection bias.
- Assumptions:
    1. SUTVA
        - My PO is deteremined solely by my treatment status; it is not affected by other's treatment status.
        - **SUTVA $\implies$ switching equation.**
    1. No-anticipation assumption
        - Zero treatment effect in the pre-treatment periods.
        - **No-anticipation $\implies$ untreated PO for treated groups; $Y_{i,t}(g) = Y_{i,t}(\infty) \  \forall \  t<g$**
    1. Parallel trend assumption
        - W/o treatment, everyone has the same evolution of the outcomes over time.
        - $\mathbb{E}\left[Y_{i, t=2}(\infty) \mid G_{i}=2\right]-\mathbb{E}\left[Y_{i, t=1}(\infty) \mid G_{i}=2\right]=\mathbb{E}\left[Y_{i, t=2}(\infty) \mid G_{i}=\infty\right]-\mathbb{E}\left[Y_{i, t=1}(\infty) \mid G_{i}=\infty\right]$
        - **DiD identification**
- SUTVA + no-anticipation + PT $\implies$ ATT is identified by DiD formula.
    - In other words, we can compute the counterfactual outcome, $Y_{i,t=2}(\infty)$ for $G_i = 2$.

## Estimating ATT in 2x2 DiD setup
1. After replacing population expectations in **ATT estimand** by their sample analogues, we get **ATT estimator**.
    - **The canonical 2×2 DiD estimator = "brute-force" DiD estimator = DiD by hand.**
1. $Y_{i, t}=\alpha_{0}+\gamma_{0} 1\left\{G_{i}=2\right\}+\lambda_{0} 1\left\{T_{i}=2\right\}+\beta_{0}^{twfe}\left(1\left\{G_{i}=2\right\} \cdot 1\left\{T_{i}=2\right\}\right)+\varepsilon_{i, t}$
    - **$\beta_0^{twfe}$ = the canonical 2×2 DiD estimator.**
    - **In practice, we use TWFE regression to estimate ATT in DiD.**
    - Unit fixed effect vs. group dummy in TWFE regression:
        - Group dummy is aggregated.
        - **In the balanced panel data, regression with group dummy and regression with unit fixed effects give numerically the same DiD coefficient.**
            - Analysis with unit-level shock and unit fixed effects gives us the same results. (??) I don't think this is intuitive.
        - **Not true for repeated cross-sectional or unbalanced panel data.**  
            - e.g., in the repeated cross-sectional data, we cannot even have state dummies; cannot estimate the model; single obs for state, model is saturated, and the model end up with zero degree of freedom.

## Inference: Cluster
- Cluster at least at the cross-sectional level (unit level) in order to allow for auto-correlation for the outcomes for the same units across time periods.
- **Large # of clusters $\implies$ CLT $\implies$ standard inference procedures (w/o additional strong distributional assumptions e.g., normality assumptions)**
- Classical approach of doing inference is all about how to sample observations from population.

## Sampling
- Panel data sampling scheme
    - In general, we have more precise estimators with panel data.
- Repeated cross-section data sampling scheme
    - **In RCS data, cluster at the sampling level; cluster in the sampling type of uncertainty.**
    - e.g., If you sample schools from super-population, cluster at school. Students at each school are clustered.

## Details about estimation and inference
- Large sample properties of the 2x2 DiD estimator in the panel data case:
    1. **Concsistency of the DiD estimator**
        - DiD estimator converges in probability the true ATT under SUTVA, no-anticipation, and PT.
    1. **Asymptotic normality of the DiD estimator**
        - **Panel data: 2 infulence functions (for each group); smaller variance than RCS data; this is why panel data give more precise estimator.**
        - **Repeated cross-sectional data: 4 influence functions (for each group and time).**
        - Reliable inference about the ATT w/o distributional assumptions.
## PS2:
- TWFE with group dummy vs with state fixed effects:
    - **They have different SE b/c of different degree of freedom adjustment.** (The # of independent variables is different.)
        - Only one group dummy to estimate vs. every state dummies to estimate.
    - **When data is large, it does not really matter.**
    - **In this example, there is no right and wrong; just different ways.**

---
# 3. Classical 2x2 DiD Setup (Part 2) - Clustering and Inference
## Clustering from sampling perspective
- With repeated cross-sectional data, we don't really cluster; we observe each unit only once!
- With balanced/unbalanced panel, we cluster in individual level; we observe units before and after treatment.


## Clustering at different level than unit level (more aggregated level)
- For example, cluster at the treatment assignment level.
- Which level to cluster is not an easy choice; there are a lot of debates on it.
    - **Choice of cluster level depends on your sampling scheme, type of uncertainty you are trying to reflect, ...**

## Large # of clusters: Cluster-Robust inference via Multiplier bootstrap
- **If you have many # of clusters, you can cluster at more aggregated level.**
- Multiplier bootstrap procedure for clustering:
    - Use the influence functions.

## Small # of clusters: Model-based and alternative approaches
- **If you have small # of clusters, you have a few options (w/ assumptions) to cluster at aggregate level.**
- Less than 42 is usually considered as small # of clusters.
- **Small # of clusters $\implies$ CLT does not work well $\implies$ inference is not correct.**
    - We need assumptions!
- Model-based approach: 
    - Assume there exist common cluster-level shocks, $\nu_{j,t}$; and they are iid across clusters. (I did not really understand.)
    - Therefore, no heterogeneous TE; iid $\nu_{j,t}$ = homoegeneous TE.
- Alternative approaches:
    - Condition on shocks, $\nu_{j,t}$ (I did not really understand.)
        - e.g., Card and Krueger (1994)
    - Randomization-based inference
        - Sharp null of no treatment effects for all units

## Note:
- Model-baed and alternative approaches are hard to understand.

---
# 4. Role of Covariates in DiD
## Assumptions (identification)
- Assumptions:
    1. **Conditional PTA**: PT holds conditional on pre-treatment covaraites
        - It allows for covaraite-specific trends.
        - Control only for **pre-treatment covariates**: why? Treatment could affect covariates; and then, post-treatment covariates are mediators! We shouldn't control them.
    2. **Strong overlap assumption (common support assumption)**
        - Given X, there are some treated and untreated.
- SUTVA + no-anticipation + conditional PT + common support $\implies$ ATT is identified by DiD formula.
- ATT with covariates:
    - $ATT(X) \equiv \mathbb{E}[Y_{t=2}(2)-Y_{t=2}(\infty)\mid G = 2, X]$ =  covariate-specific ATT = strata-specific ATT
    - $ATT \equiv \mathbb{E}[ATT(X)\mid G = 2]$ = integration of ATT(X) over the conditional distribution of X given G=2.

## Simple TWFE estimation (parametric approach)
- **The simeple TWFE regression is biased b/c it does not satisfy the conditional PT assumption.**
    - ATT(X) = ATT: Homogeneous ATT b/w covariate subpopulations.
- Why? ANS: **This regression does not capture the heterogeneous trends**; $\alpha_{0,2}$ does not interact with trends; e.g., $1(T_i = 2)*X_i$.
    - ***Need to interact covaraites with dummies to get unbiased ATT(X): $1(G_i = 2)*1(T_i = 2)*X_i$ ???***
    - ***Does the interaction b/w time and covariates term help fix the bias in the TWFE?***  Maybe this imposes very strong parametric assumption?
- Example: Simulation

## Semi- and non-parametric DiD procedures
- **Separate identification from estimation and inference!**
    1. Regression-adjusted DiD estimator
        - Idea: **Compute the brute-force DiD estimator conditional on covaraites w/ parametric, semi-parametric, or non-parametric estimation method.**
        - Issue: How to model the outcome evolution (trend)? e.g., linear vs. quadratic trend.
        - Panel data and stationary RCS data $\implies$ simpler DiD formula.
    1. Inverse probability weighting DiD estimator
        - Idea: **IPW matching in the second difference of DiD (Scott covered it!)**
        - Issue: How to model the propencity score model? Does common support assumption hold?
        - **IPW is usually not very precise (high SE).**
    1. Doubly Robust DiD estimator
        - Idea: **Regression-adjusted DiD estimator + IPW DiD estimator (Matheus Facure covered it!)**
        - Issue: How to model the outcome evolution? Does common support assumption hold?
        - Always use DR DiD estimator!
            -  As long as one of them are correct, I get my ATT.
            - If both models are kind of correct, it still helps to get ATT. Because this problem has a product structure, (small mistake)\*(small mistake) = even smaller mistake. e.g., 0.5*0.3 = 0.15.
        - **This opens a gate for us to do ML w/ DiD.** For example, use ML models to estimate outcome model or IPW model. ML models make mistakes; product of mistakes helps us to move forward.
- Example: Simulation

## Notes:
- Why use notation for repeated cross-sectional version (more aggregated approach) for TWFE? 
    - ANS: **This is a general expression that can be applied to balanced/unbalanced panel data and repeated cross-sectional data.** For panel data (fixed effects), change the group fixed effects to unit fixed effects. Simple!
    - W/ fixed effects, $\alpha_i$ absorbs $X_i$. So the TWFE w/ covariates will be the same as the one w/o covariates.
- Panel data always have more precise estimators than cross-sectional data.
- Stationary RC data samples from the same underlying distribution across time.

## PS3
- Question: The effect of weekly benefit amounts on the duration of time out of work and the total medical costs.
- 2x2 DiD setup w/ repeated cross-sectional data.
    - No individual fixed effect; treatment group dummy instead.
- In the R code, "cluster = ~id" does not cluster my standard errors b/c it is not a panel data. **Pedro strongly recommends that we use the cluster option no matter what; it helps me to be cautious about clustering choice.** 
    - In this example, my effective sample size is "id". 
    - This reminds me that I am doing approximations replying on large number of units.
- Level-duration = change in level (the # of weeks) vs. log(duration) = % change
    - Regression coefficients have different interpretation; log of outcome variable $\implies$ PT assumption is in relative terms.
- PT in level or log?
    - In this example, treatment effect is significant only in log.
    - Do we need PT in log only for identification? Or need PT both in log and level? There are lot of discussion in the literature.
- Pedro's paper (aren't they obvious?):
    1. If there is no trend, it is possible that PT holds regardless of the functional form of outcome.
    1. If treatment assignment is random, PT holds regardless of the functional form of outcome.
    1. If no trend for some population + random treatment assignment for some population, PT holds regardless of the functional form of outcome.
- The paper includes the types of injuries in the regression, but Pedro thinks we should not include them b/c they are colliders.
    - e.g., the policy change affects how workers are careful about injury; this could affect the type of injury in the work place.
    - Treatment affects them.
- ***Is the paper using biased TWFE model?***
---
# 5. DiD w/ Multiple Time Periods (Part 1)
## DiD setup w/ multiple time periods
- 2 groups:
    - The same as before. 
- Multiple time periods:
    - Pre-treatment periods: $t=1,2, ..., g-1$
    - Post-treatment periods: $t = g, g+1, ..., T$
- The # of cross-sectional units are more than time periods.

## Parameters of interest
- Average TE at time $t$ among treated at time $g$.
- Two different notations for ATT:
    1. $ATT(g,t)= ATT(t) = \mathbb{E}\left[Y_{i,t}(g) - Y_{i,t}(\infty) \mid G_i = g\right]$.
        - Why $ATT(g,t)= ATT(t)$? We have only two groups.
    1. $ATT(g,g+e)$ $=$ $ATT(g,t)$ in event time $e$.
- By averaging $ATT(g,t)$  over $t$, we can get one-dimensional parameter.

## Identification
- No-Anticipation $\implies$ $ATT(g,t) = 0 \ \forall t<g$.
- Post-treatment PT:
    - $\forall t\geq g, \ \mathbb{E}\left[Y_{i, t}(\infty) \mid G_{i}=g\right]-\mathbb{E}\left[Y_{i, t-1}(\infty) \mid G_{i}=g\right]=\mathbb{E}\left[Y_{i, t}(\infty) \mid G_{i}=\infty\right]-\mathbb{E}\left[Y_{i, t-1}(\infty) \mid G_{i}=\infty\right]$
- Assumptions: SUTVA + No-Anticipation + ***post-treatment PT***.
- $ATT(g,t)= \left( \mathbb{E}\left[Y_{i,t}\mid G_i = g\right] - \mathbb{E}\left[Y_{i,g-1}\mid G_i = g\right] \right) - \left(  \mathbb{E}\left[Y_{i,t}\mid G_i = \infty\right] - \mathbb{E}\left[Y_{i,g-1}\mid G_i = \infty \right] \right)$
    - We get "long-difference" approach to DiD; baseline period is fixed as $g-1$.
    - We just need two time periods, $t$ and $g-1$, to compute $ATT(g,t)$ just like we did in 2x2 DiD estimator.
    - We are trying to get what we want using minimum set of assumptions. That is why we fix the baseline time period as $g-1$.
    - Very easy to transform this problem to regression!


## Estimation
1. The brute-force DiD estimator
1. **TWFE DiD estimator with subsetting**
    - ***Subset the data to have only $t$ and $g-1$ for $t\geq g$; and run the TWFE regression like 2x2 case.***
    - **Multiple testing issue!**
    - Note that in practice, we don't do that; this is what Pedro recommends. In practice, we use standard TWFE regressions w/o subsetting data. See the lecture 6.

## Inference
- Infrerence for each $ATT(g,t)$ is the same as the 2x2 case.
- Inference across all $ATT(g,t)$'s, we need some corrections for multiple testing.

## Covariates
- Assumptions: Conditional post-treatment PT + Strong Overlap Assumption
- Semi- and non-parametric DiD procedures:
    1. Regression-adjusted DiD estimator; 
    1. IPW DiD estimator; 
    1. DR DiD estimator

## Remark on pre-treatment period
- Idea: If pre-trends are parallel, post-treatment trends may be more likely to
be parallel
- “Pre-test” for reliability of parallel trends.
    - Run TWFE regression or semi- and non-parametric DiD procedures for $t<g$.

## Remark on  inference
- Testing $ATT(g,t)$ for each point of $(g,t)$ vs. tesing all of it together (multiple testing)
- Methods:
    1. Simultaneous Inference
    1. Simultaneous confidence intervals: Multiplier Bootstrap procedure

---
# 6. DiD w/ Multiple Time Periods (Part 2)
## In practice, we use standard TWFE regressions
1. **TWFE DiD estimator without subsetting**
    - Assumption: Everywhere PT.
        - If we have only post-treatment PT, this estimation is biased; selection bias.
    - $\beta^{TWFE}$ $=$ average of post-treatment $ATT(g,t)$'s.
    - TWFE = regression w/ group dummies (See my proof)
1. **TWFE with dynamics (event-study DiD)**
    - We care about dynamics of TE within a specific time window.
    - Pedro's recommendation: Include all possible leads and lags possible. And then you can drop some later.

## Pre-testing assumptions
### 0. No violation
- PT assumptions:
    1. Post-treatment PT $\implies$ **long-differecne ATT ($g-1$ as the baseline period)**
    1. Everywhere PT $\implies$ **short-difference ATT (no baseline period) for pre-treatment; and long-difference ATT for post-treatment.**
- How to pre-test your assumptions? Check all the pre-treatment coefficients.
    1. Whether they are near zero.
    2. Whether their CI's are not wide and covers zero.
- If so, our assumptions are PLAUSIBLE. It does NOT mean that our assumptions are valid. **PT assumption is about the future (counterfactual), and so it is untestable.** Parallel pre-trends $\neq$ valid design. Pre-testing is not perfect!
    - Why we want to check pre-trends? **With linearity and smoothness, dramatic changes before and after treatment are very unlikely.** However, it still could happen!
- If the coefficient is very far from zero but its CI covers zero, then be cautious! It is hard to decide whether linear trends vs. flat line. See Roth (2022)

### 1. Violation of the no-anticipation assumption (We still have PT)
- Pretty easy; change the treatment assigned date to the anticipated one.
    - Treatment date is not the starting date; it is the date when the units actually respond to the treatment ancitipation.
- Assumptions (change in treatment date):
    1. Limited-anticipation
    1. Stronger PT
### 2. Violation of the PT assumption (We still have no-anticipation assumption)
- Key point: Without PT, the untreated group is not informative for the treated group; once PT is violated, post-treatment coefficients are biased.
    - Pre-treatment PT is not necessary nor sufficient for anything; **what really matters is the post-treatment PT (counterfactual outcomes for treated) for unbiased estimation.**
 - In practice, people typically go with ***everywhere PT***; w/o pre-treatment PT, people don't believe in post-treatment PT.
- If we know the nature of the PT violation, we might be able to estimate ATT. However, Pedro does not believe that we know the nature of the violation in practice. Either linear or quadratic trend does not sound right to him. He rather do sensitivity analysis if he does not believe in PT.
- In non-parametric fashion, we cannot relax PT assumption unless we add lot of structures in the model. We won't cover it.
- Some theoretical ideas:
    1. No pre-treatment PT; but yes post-treatment PT $\implies$ unbiased DiD estimate.
        - Non-parallel pre-treatment trend may not be bad!
    1. Yes pre-treatment PT; but no post-treatment PT. $\implies$ biased DiD estimate.
### 3. Everything is violated
- Very tricky; both violations could cancel each other. The day might look great. Be careful.
## Note:
- Power issues: Even no rejection of pre-trends, there maybe lack of power.
- Contextual knowledge matters the  most!
    - Good institutional knowledge
    - Good modeling assumptions
    - Good understanding of economic theory
    - Data is always limited.
---
# 7. DiD with Variation in Treatment Timing (Part 1)

## TWFE setup with variation in treatment timing
- Example: Medicaid Expansion
- Staggered design: Treatment is irreversible; once treated, forever treated.
- Different groups have different treatment timing.
    - Early-treated, later-treated, and never-trated
- **Forbidden comparision uses later-treated as treated group and  early-treated as comparision group.**
    - **This is the problem; we do not have any PT assumption for that case.**
## Static TWFE regression
### 1. Goodman-Bacon Decomposition
- Example: Effect of ACA Medicaid Expansion on Health Insurance rate
- Assumption-free decomposition
- $\widehat{\beta}$ is a weighted sum of different group comparision DiD estimates
- Weights depend on the two things:
    1. The sample size of each DiD's time window.
    1. Variance of treatment assignment timing within each of the window.
- **Negative weight for the forbidden comparision case.**
    -  If the weight for this group is zero, we are good.
    - ***When you do DiD in practice, you are gonna use already-treated group as treated group, and later-treated group as control group. We can make it right by giving negative weight to that DiD coefficient. WHY?*** 
    - [See Fernando's note](https://friosavila.github.io/playingwithstata/main_csdid.html)
- TE hetrogeneity/dynamics $\implies $ not easy-to-interpret causal parameter of interest in TWFE regressions. Why?
    - After treatment, already-treated units have completely different path copmared with later-treated units.
    - DiD is not designed for this type of comparision; we don't have assumption for that.
- OLS is hungry for variation; it always looks for all possible variation in treatment status in order to minimize MSE.
    - When we use DiD, we want to use not every variation in the data but some variation that we like; some are more plausible than others.


### 2. de Chaisemartin and D’Haultfoeuille decomposition
- Assumptions: SUTVA, no-anticipation, and strong unconditional PT.
- ${\beta}$ is an expected value of a weighted average of unit-specific TE estimates
- Negative weight for the forbidden comparision case.
- Although everyone has positive TEs, $\beta$ could be negative!

### 3.  Notes on weights
- Two problems of weights:
    1. Negative weights
    2. The distribution of weights of different DiD's (who is gonna  be weighted more and who is gonna get weighted less); weights are convex b/c they are in b/w 0 and 1.
-  We have dynamics and do not have never-treated group $\implies$ negative weights.
    1. If TEs do not evolve over time (yes level shift; but no trend shift), we do not have negative weights.
    1. If we have a never-treated group with reasonable size, it is rare to have negative weights.


## Dynamic (event-study) TWFE regression
### Sun and Abraham (2021)
- Example: Simulation
- Event-study TWFE is still very hard to interpret!
- DiD coefficient on a given lead or lag can be contaminated by effects from other periods.
    - **Contamination effect from post-treatment periods to pre-treatment periods.**
    - Pedro thinks it is even worse than static TWFE regressions b/c pre-treatment coefficients are contaminated so that we cannot use them to pre-test our assumptions.
- **No bias in event-study TWFE if**
    1. **Homogeneous TE**; and
    1. **Properly trimmed time periods** (valid comparison group)
- Sources of bias:
    1. Heterogeneity in dynamics (we have different $\mu_g$'s in the simmulation)
    1. Not trimmed data (in the simulation, no valid comparison group after 2004 b/c everyone is treated)
- Even with homogeneity TE + dynamics, DiD coefficients could be contamintaed.
- Note that we have to drop two even-times:
    1. t = -1 as a baseline.
    2. **t = the very first time period; so we can avoid perfect multi-collinearity problem when everybody is treated eventually.** Why?
- The simulation example is extreme (not much heterogeneity but dynamics are so strong, so it is so biased).
    - In practice, if we don't have so much dymaics, bias will be much smaller.




## Note
- Treatment effect heterogeneity:
    1. Each unit has different TE.
    1. TE evolves over time.
- Generally, saturated event-study TWFE gives us a better result than not-saturated one.
---
# 8. DiD with Variation in Treatment Timing (Part 2)
## So what to do? (solution)
- Question of interest vs. estimation method.
    - Parameter of interest and how to estimate it vs. does my regression specification give me what I want
    - As long as there is no treatment timing variation, we get the same answer no matter what;  $ATT(g,t) = \beta$
- With treatment timing variation, $ATT(g,t) \neq \beta$
- Separate identification, aggregation, and estimation/inference steps!
- Example: Medicaid Expansion
- Callway-Sant'Anna DiD estimator: 
    - Let's go back to the principles
    - Compute multiple 2x2 ATT's
    - And aggregate them using our own weights.


## Three steps of Callway-Sant'Anna DiD estimator
### 1. Identification
#### (1) Without covariates
- Assumptions (SUTVA is implicitly assumed):
    1. No-Anticipation
    1. PT
        - Never-treated PT: Never-treated as control
        - Not-yet-treatd PT: Not-yet-treated, or never-treated + not-yet-treated as control
- With multiple g's (different treatment timings), we could have spill-over effect:
    - Violation of SUTVA
    - Violation of no-anticipation (easy fix)
- $ATT(g,t)$ Estimand: $ATT_{unc}^{never}(g,t)$ and $ATT_{unc}^{ny}(g,t)$
#### (2) With covariates
- Assumption: Conditional PT
    - Conditional never-treated PT
    - Conditional not-yet-treatd PT
- Doubly Robust DiD estimand: $ATT_{dr}^{nev}(g,t)$ and $ATT_{dr}^{ny}(g,t)$

### 2. Aggregation
- Time average of ATT
- Cohort average of ATT
- Event-study average of ATT
### 3. Estimation and inference
- Estimation: Plug-in principle using regression adjustment, IPW, or DR estimands.
- Inference: Same idea as before

## ACA Medicaid Expansion Example
- Why TWFE and CS have the similar results in this example?
    1. Not much dynamics.
    2. Large group of never-treated units.
- Note: **The weight for the forbidden comparison is very small in general.**
- Few # of clusters = some treated groups are very small (2015 treated group has only 3 states)
     - When groups are small, it is hard to talk about PT b/c it is noisy.
- Then, CI's are not reliable.
- ES TWFE does not allow for heterogeneity; no simulatneous CI; multiple testing issue.
- CS event-study specification collapses each $ATT(g,t)$; the same effective sample size as regression specification; yes heterogeneity; yes multiple testing.


## Note:
- DiD is all about $ATT(g,t)$.
- There are many papers on DiD with staggered treatment timing.
    - All very similar but different in terms of how to deal with PT and covarites.
- Bias vs. efficiency
    - CS estimator tries to minimize assumptions $\implies$ cautious about bias
    - Using more pre-treatment periods $\implies$ cautious about efficiency

## PS4
- In the event-study regression, we have to drop two time periods: baseline and the very first period.
    - ***In both R and Stata, never-treated units are treated as baseline. Why?***

---
# Extra Lecture 1: When is Parallel Trends Sensitive to Functional Form?
## Intro
- (Def) **PT is NOT sensitive to functional form of Y $\equiv$ When PT holds for Y, it also holds for g(Y) for any monotonic fnc g.**
- Questions:
    1. Under what conditions is the PT NOT sensitive to functional form of output?
    1. If it is sensitive, which functional form to use for output? e.g., earnings in levels, logs, or percentiles.
- **Functional form matters in DiD b/c of no restriction on treatment assignment.**
    - When we have random treatment assignment, fucntional form of outcome does not matter.

## Summary of Roth and Sant'Anna (2021)
- The treadeoff b/w functional form sensitivity assumption and distributional assumption.
- (Thm 1)  **CDF PT $\iff$ PT is insensitive to funcitonal form.**
- (Thm 2) **CDF PT $\iff$ randomized treatment, stationary untreated PO, or mixtures of the two.**
- Tests for null that PT is insensitive to functional form.
    - Idea: CDF is an increasing fnc.
    - Again, CDF PT is not verifiable but falsifiable.
- Example: Minimum wage changes and employment-to-population ratios for 25c wage-bins


## Note:
- Switching equation implicitly assumes SUTVA.
---
# Extra Lecture 2: Machine Learning meets DiD (DiD with Covariates)
## Use ML to do DiD with covariates
- 2x2 DiD with panel data
- Assumptions: The same three assumptions as DiD with covariates design
- ATT: Same semi- and non-parametric DiD procedures
    1. Regression-adjusted DiD estimator
    1. Inverse probability weighting DiD estimator
    1. Doubly Robust DiD estimator
- Parametric vs. non-parametric vs. ML
    - In the non-parametric world, given that the identification assumptions (NOT modeling assumptions) hold, all three methods give the same answer.
        - Which one to choose among them?
    - In the parametric world, we have huge benefit from DR DiD by modeling both of outcome regressions and PS under the identification assumptions.
    - ML?

## High-dimensional problem and ML
- Issues of high-dimensional setup: More information on covariates $\implies$ conditional PT is more plausible; but we have issues w/ common support.
    - \# of obx > \# of covariates (\# of all potential interactions of covariates)
    - Which convariates to include
    - Functional form of outcome regression and PS
- Solution:  ML can help with model selection.
- Assumption:  Approximate sparsity
    - We assume that among all of the possible covariates (all of possible transformations), a few of them are important.
    - We assume that outcome revolution of non-treated units and/or the propensity score are approximately sparse.
- Sometimes some covariates kind of matter but the computer says it does not matter; omitting them could be a mistake.
    - We allow our procedure to make mistakes; model selection is imperfect; DR DiD is recommended!
    - Then, we have to choose some estimation techniques that are more suitable for our problem.
- After picking up the relevant covariates (model selection), doing inference is trickier!
    - Why? ML procedure does not care about causality (or post-model selection); it is all about prediction. They don't care about inference.
    - We care about counter-factual analysis and inference (CI's and SE's). So we have to take the model selection seriously.
- LASSO is very good with approximate sparsity assumption.
    - Panalized OLS
    - Panalized MLE


## Problems with LASSO
- Choice of panalty parameters
    - Theory-driven way
    - Cross-validation
- Downward bias:
    -Some of beta's don't shrink enough to be zero $\implies$ bias in LASSO.
- Two-step procedure to reduce bias:
    1. Use LASSO only for model selection (drop some covariates);
    2. Post-LASSO: Run parametric model using the selected variables.

## Example
- Example: Simulation
- Requirements to use ML in the first step
    1. Neyman Orthogonality condition = a sort of Double-Robust estimator.
    1. The class of function that my true model belongs to is not so complex (no-overfitting).
        - Assumption on the complexity of the model; or
        - Cross-fitting.
- Model selection is tricky; Double-robust procedure guarantees valid inference after model selection.
## Nots:
- Always use double robust method!
- If weak common support, use output regression as long as you are willing to do extrapolation.