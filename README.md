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
 
