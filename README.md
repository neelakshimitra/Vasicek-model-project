# Vasicek-model-project

This project reproduces and extends the OLS and MLE-based estimation of the Vasicek interest rate model using US 3-month Treasury rate data (GS3M). It follows the methodology presented in the report Estimation and Application of the Vasicek Interest Rate Model (Buffoli & Rolfi, 2025) and aims to deepen understanding of mean-reverting interest rate models in both discrete and continuous time.


🧬 What This Project Covers

✅ OLS Estimation of Discretized Vasicek

Transforms the continuous Vasicek SDE into its Euler-discretized form:

r_{t+1} = α + β r_t + ε_t

Estimates α and β via OLS and backs out Vasicek parameters:

a = (1 - β) / dtb = α / (1 - β)σ = std(ε) / sqrt(dt)

Produces estimates consistent with Table 1 of the report.

Residual analysis (heteroscedasticity, autocorrelation) reveals theoretical violations, confirming the paper's critique that assumptions often fail in practice.

✅ MLE Estimation via Likelihood Maximization

Uses the exact conditional transition density:

r_{t+1} | r_t ∼ Normal(μ, Q)

μ = r_t e^{-a Δt} + b(1 - e^{-a Δt})Q = (σ^2 (1 - e^{-2aΔt})) / (2a)

Defines and minimizes the negative log-likelihood to obtain MLE estimates of a, b, and σ.

Statistically efficient under correct model assumptions.

📈 Simulation

Simulates future short-term interest rates using both OLS and MLE parameters:

r_{t+1} = r_t + a(b - r_t)Δt + σ √Δt · ε_t

Graphs compare simulated paths with historical GS3M rates.

Simulations deviate from observed data, affirming the report's claim that Vasicek models often underperform due to weak mean-reversion or structural breaks.

 🔍 Findings and Interpretation

This project replicated and interpreted the Vasicek interest rate model using both OLS and MLE estimation methods on US 3-month Treasury rate data (GS3M). The work builds on the methodology in the reference paper and compares the estimated model’s performance to historical observations.

📈 OLS Estimation Results

Regression: Fitted a basic OLS model to predict r_{t+1} from r_t.

Estimated parameters:

alpha ≈ 0.00048

beta ≈ 0.98183

R² ≈ 0.9903

Converted to Vasicek form:


a (speed of mean reversion): 4.5421

b (long-term mean): 0.0265

sigma (volatility): 0.0485

🔹 Key Graphs

Observed vs Fitted Δrₜ: Shows model fit over time.

Residual Plot: Indicates heteroscedasticity, supporting the paper’s observation that OLS residuals violate homoskedasticity.

Simulated Vasicek Path (OLS): Simulated rates deviated significantly from observed data, confirming OLS’s weakness in dynamic simulation.


🔧 MLE Estimation Results

Approach: Used Maximum Likelihood Estimation under the assumption that r_{t+1} | r_t ~ N(μ, Q), where μ and Q depend on the Vasicek parameters.

Estimated parameters:

a ≈ 5.07

b ≈ 0.0262

sigma ≈ 0.0536

🔹 Key Graphs

Simulated Vasicek Path (MLE): Closely followed historical interest rates. Demonstrated improved path realism and smoother convergence compared to the OLS simulation.


Interpretation

The results confirm the findings of the original report:

OLS provides statistically strong point estimates but performs poorly in simulating future rate paths.
MLE offers more realistic dynamics by properly capturing the variance structure, making it preferable for time-series simulation of stochastic processes.
This hands-on replication deepened understanding of how interest rate models can be estimated and tested both analytically and through simulation.


🗁 Outputs

vasicek_estimates.csv: OLS and MLE parameter estimates

vasicek_simulation.png: Simulation vs observed rates

vasicek_mle_params.npz: Reusable MLE parameters for modeling

📚 Reference

Buffoli, A., & Rolfi, D. (2025). Estimation and Application of the Vasicek Interest Rate Model.
