# Problem Set 4: The Model That Fit Too Well

ECON 3916 · Applied Data Analytics. I inherited a store revenue model whose handover note said "R-squared 0.94. Validated." and that had been over-forecasting the biggest stores. In `Econ_3916_PS4.ipynb` I simulate a 400-store panel, reproduce the inflated R², diagnose why the model fails (non-linearity, heteroskedasticity, influential stores, a leaky validation step), and rebuild it with a cross-validated model whose stated accuracy holds on new data.

## Handover note: Store Revenue Forecast (v2)

**What it predicts.**
The model predicts monthly store revenue (in \$'000) based on floor area, foot traffic, local median income, and years open. It uses a piecewise-linear spline for floor area to account for slower revenue growth at larger stores.

**Expected prediction error.**
Nested cross-validation gives an expected RMSE of about **\$25k per store per month**, with a 95% range of **\$22k to \$29k** and an R² of about **0.93**. The model also had an RMSE of \$23.9k on a new simulated month. However, predictions are less accurate for larger stores because their revenue is more variable.

**Limitations.**
The model may not work well for stores outside the observed size range of 6k to 86k sq ft because it must extrapolate beyond the data. It may also become less accurate if the store population or the relationship between revenue and its predictors changes, such as in a new market. The model still over-predicts revenue for the largest 10% of stores by about \$21k per month, although this is an improvement from about \$42k with the old model. These forecasts should be checked against actual revenue.

**Next steps.**
I would try weighted least squares to account for the higher noise among large stores, add prediction intervals that are wider for larger stores, and check prediction errors every month against the expected \$25k RMSE. I removed `staff_count` because it did not improve prediction, not simply because it had a high VIF.
