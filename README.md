# econ3916-lab14-ols-diagnostics
# OLS Diagnostics: When the Standard Error Is Lying

## Objective
I tested how problems with a regression's errors affect its estimates and standard errors, and which diagnostics can and can't catch them.

## Methodology
- I simulated errors whose spread grows with x, and fitted one regression with classical and with robust (HC3) standard errors.
- I ran 400 simulated samples to check how often each 95% interval covered the true slope.
- I read four residual plots beside Breusch-Pagan and Jarque-Bera tests.
- I measured leverage, standardised residuals and Cook's distance, and deleted the most influential row.
- I fitted a California Housing regression with classical and HC3 standard errors.
- I wrote a function, hc3_se(), that gives the HC3 standard error for any regression on any slice of the data.
- I compared classical, HC3 and clustered standard errors on simulated workers grouped in firms.
- I built a regression that passes the diagnostics but is still wrong because of a missing confounder.

## Key Findings
- Both fits gave the same slope, 2.0147, but the standard errors were 0.0264 (classical) and 0.0290 (HC3): heteroskedasticity changes the standard error, not the estimate.
- Over 400 samples, the classical 95% interval covered the true slope 91.8% of the time and the robust one 93.5%, with Monte Carlo standard errors of 1.4% and 1.2%. Only the classical shortfall was clearly more than chance.
- Deleting one row out of 600 moved the slope only 0.58 of its own standard error, but cut the standard error by 33%.
- In California Housing, the HC3 standard error on AveRooms was 5.02 times the classical one.
- The HC3 standard error on AveRooms was 0.0121 with all districts and 0.0082 without the 965 at the 5.0 ceiling, which isn't by itself a reason to drop them.
- Five districts, 0.024% of the data, carried 92% of the total Cook's distance.
- With workers grouped in firms, the clustered standard error was 3.14 times the classical one, because workers in the same firm share a shock.
- A regression with a missing confounder passed Jarque-Bera and Cook's distance (Breusch-Pagan failed narrowly, by chance) but estimated a slope of 2.518 against a true 1.5: diagnostics can't detect a missing confounder.
