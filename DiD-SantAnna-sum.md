# 1. Intro to DiD

# 2. Classical 2x2 DiD Setup
- Setup: Two groups and two time periods.
- Assumptions:
# 3. DiD with Covariates
- Assumption: Conditional PTA.
- Control only for pre-treatment covaraites
- Simple TWFE estimation is biased; we need to saturate the TWFE regression.
- Semi- and non-parametric DiD procedures:
    1. Regression-adjusted DiD estimator
    1. IPW DiD estimator
    1. DR DiD estimator
# 4. DiD with Multiple Time Periods
- Setup: Two groups and multiple time periods.
- Assumptions: SUTVA + No-Anticipation + ***post-treatment PT***.
    - Long-difference $ATT(g,t)$.
- w/ subsetting data: keep only $t$ and $g-1$ for $t\geq g$, and run TWFE 2x2 regression.
    - This is not recommened b/c of multiple testing issue.
- We can add covariates.
- W/o subsetting data (This is what we do in practice):
    1. TWFE w/ **everywhere PT assumption**
        - $\beta^{TWFE}$ $=$ average of post-treatment $ATT(g,t)$'s.
        - This is b/c TWFE = 2x2 DiD regression w/ group dummies (See my proof)
    1. Event-study TWFE
        - Fully saturated regression recovers  $ATT(g,g+e)$'s.
- Pre-testing:
    - We could test two PT assumptions: Post-treatment PT or everywhere PT.
    - How to pre-test your assumptions? Check all the pre-treatment coefficients.
        1. Whether they are near zero.
        2. Whether their CI's are not wide and covers zero.
    - Why we want to check pre-trends? **With linearity and smoothness, dramatic changes before and after treatment are very unlikely.** However, it still could happen!
    - Some theoretical ideas:
        1. No pre-treatment PT; but yes post-treatment PT $\implies$ unbiased DiD estimate.
            - Non-parallel pre-treatment trend may not be bad!
        1. Yes pre-treatment PT; but no post-treatment PT. $\implies$ biased DiD estimate.
- Violation of assumptions:
    - No-Anticipation assumption violation: Change the treatment assigned date to the anticipated one. (And also change slightly identification assumptions.)
    - PT violation: No easy fix.
    - Both no-Anticipation and PT violation: No easy fix.
# 5. DiD with Variation in Treatment Timing
- Setup: Multiple groups and multiple time periods.