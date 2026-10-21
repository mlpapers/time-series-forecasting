# Time Series Forecasting

## Forecast targets and information

- **[Forecast origin and horizon](https://otexts.com/fpp3/toolbox.html)** (book). Forecasts use information available at a stated origin to predict later observations. Evaluate the horizons actually needed; one-step accuracy need not identify the best multi-step forecaster.

- **[Local and global forecasting](https://arxiv.org/abs/2008.00444)** (2020). Local models fit each series separately; global models share a function across series. Montero-Manso and Hyndman show that global models need not assume similar series; approximation capacity and estimation error remain separate concerns.

- **[Known and unknown future covariates](https://otexts.com/fpp3/dynamic.html)** (book). Calendar variables may be known ahead; future weather measurements may not. Regression forecast intervals conditional on assumed covariates omit their uncertainty. Report what was available at each forecast origin.

## Statistical foundations and decomposition

- **[Naïve and seasonal naïve](https://otexts.com/fpp3/toolbox.html)** (book). Predict the last observation or the last observation at the matching seasonal position. Essential reference forecasts: improvements over a weak neural baseline do not establish gains over these task-specific alternatives.

- **[Exponential smoothing and ETS](https://otexts.com/fpp3/exponential-smoothing.html)** (book). Updates level, trend and seasonal components with decaying weights. State-space formulations specify error models and prediction intervals; additive and multiplicative components impose different data and variance assumptions.

- **[ARIMA and seasonal ARIMA](https://otexts.com/fpp3/arima.html)** (book). Models autocorrelation after differencing, with autoregressive and moving-average terms. Differencing addresses stochastic trends; seasonal terms model recurring lag dependence. Residual diagnostics matter alongside information criteria.

- **[Automatic ETS and ARIMA selection](https://www.jstatsoft.org/article/view/v027i03)** (2008). Hyndman and Khandakar combine unit-root tests, information criteria and search to automate selection. Provides statistical baselines; automatic order selection does not guarantee adequate residuals or future accuracy.

- **[STL and decomposition-based forecasting](https://otexts.com/fpp3/decomposition.html)** (book). Separates trend, seasonality and remainder; forecast the seasonally adjusted series and restore seasonality. STL permits changing seasonal patterns, but the forecasting step still needs an assumption about future seasonality.

- **[Dynamic harmonic regression](https://otexts.com/fpp3/dynamic.html)** (book). Uses Fourier terms for seasonal patterns with ARIMA errors for remaining temporal dependence. Useful for long or multiple seasonal periods; the number of Fourier terms controls seasonal flexibility.

- **[Vector autoregression](https://otexts.com/fpp3/advanced.html)** (book). Predicts several series from their own and each other’s lagged values. Captures linear cross-series dynamics; parameter count grows with series count and lag order. Predictive lag relationships do not by themselves establish causal effects.

- **[Intermittent demand: Croston](https://otexts.com/fpp3/practical.html)** (book). Smooths nonzero demand sizes and interarrival times separately, then takes their ratio. The original estimator is biased and supplies no model-based prediction intervals; sparse counts require more than ordinary error metrics.

## Global neural and probabilistic models

- **[DeepAR](https://arxiv.org/abs/1704.04110)** (2017). Trains an autoregressive recurrent network across related series with a likelihood objective. Samples future trajectories recursively; the likelihood and available covariates determine the forecast distribution’s support and conditioning.

- **[Deep state-space models](https://proceedings.neurips.cc/paper/2018/hash/5cf68969fb67aa6082363a6d4e6468e2-Abstract.html)** (2018). Uses a shared recurrent network to parameterize a linear state-space model for each series. Combines cross-series learning with structured latent dynamics and probabilistic inference, rather than predicting each horizon independently.

- **[DeepVAR and Gaussian copulas](https://arxiv.org/abs/1910.03002)** (2019). Couples recurrent dynamics to a low-rank Gaussian-copula distribution for multivariate forecasting. Models cross-series dependence; marginal calibration alone cannot establish that joint scenarios or aggregate forecasts are accurate.

- **[N-BEATS](https://arxiv.org/abs/1905.10437)** (2019). Uses residual fully connected blocks with backcast and forecast branches. Generic learned bases and constrained trend/seasonal bases are distinct variants; an interpretable decomposition is an architectural choice, not a property of every N-BEATS model.

- **[N-HiTS](https://arxiv.org/abs/2201.12886)** (2022). Combines input pooling at multiple scales with hierarchical interpolation of forecast outputs. Extends residual forecasting toward long horizons without attention; pooling and interpolation control which temporal detail is retained.

- **[Temporal Fusion Transformer](https://arxiv.org/abs/1912.09363)** (2019). Combines recurrent processing, variable-selection gates and attention for multi-horizon quantiles. Separates static, observed-past and known-future inputs; attention and gate weights describe model behavior, not causal effects.

- **[TiDE](https://arxiv.org/abs/2304.08424)** (2023). Uses dense encoder–decoder blocks with past observations and dynamic covariates. Supplies a non-attention baseline for long-horizon forecasting; its linear-system analysis has assumptions beyond the nonlinear benchmark implementation.

- **[TSMixer](https://arxiv.org/abs/2303.06053)** (2023). Alternates MLP mixing across time and features. Compares temporal-only and cross-variate processing; gains from mixing variables depend on the data’s cross-series information, not the multivariate label alone.

## Attention, patches and normalization

- **[Informer](https://arxiv.org/abs/2012.07436)** (2020). Uses sparse attention, attention distillation and a decoder producing multiple future steps together. Targets long-sequence computational cost; efficient attention alone does not establish improved forecast accuracy.

- **[Autoformer](https://arxiv.org/abs/2106.13008)** (2021). Combines progressive trend/seasonal decomposition with an autocorrelation mechanism that aggregates recurring subseries. Encodes periodic structure explicitly instead of relying solely on pointwise attention.

- **[PatchTST](https://arxiv.org/abs/2211.14730)** (2022). Tokenizes local time windows as patches and shares transformer weights across channels processed independently. Preserves local patterns while shortening token sequences; cross-variable dependence is not explicitly modeled in the core architecture.

- **[iTransformer](https://arxiv.org/abs/2310.06625)** (2023). Treats each variate’s history as a token and applies attention across variates. Reverses the usual time-token arrangement; differs from PatchTST’s channel-independent processing rather than simply using a newer attention layer.

- **[Reversible instance normalization](https://github.com/ts-kim/RevIN)** (2021). Normalizes each series instance and restores its scale at the output. Reduces sensitivity to shifting means and variances; it does not guarantee robustness to changes in dynamics or conditional relationships.

- **[Linear-baseline challenge](https://arxiv.org/abs/2205.13504)** (2022). Zeng et al. find simple linear models outperform the tested long-horizon transformers on nine datasets. Supports matched linear baselines and lookback tuning; does not show that attention cannot help forecasting.

## Pretrained forecasting representations

- **[TimesFM](https://arxiv.org/abs/2310.10688)** (2023). Pretrains a decoder-only model on time-series patches for zero-shot forecasting. Variable context and horizon support concerns the model interface; unseen-series evaluation still requires checking pretraining overlap.

- **[Chronos](https://arxiv.org/abs/2403.07815)** (2024). Scales and quantizes observations into tokens, then trains language-model architectures on time-series sequences. Sampling produces probabilistic forecasts; numerical tokenization differs from transferring a text-pretrained language model.

- **[Moirai](https://arxiv.org/abs/2402.02592)** (2024). Uses multiple patch sizes, variate-independent attention and a mixture distribution head across frequencies and dimensions. Pretrains on LOTSA; the paper separates in-distribution evaluation from held-out-dataset forecasting.

- **[Lag-Llama](https://arxiv.org/abs/2310.08278)** (2023). Uses lagged values in a decoder-only transformer with a probabilistic output head. Studies zero-shot and fine-tuned forecasting; Student-t outputs in the original model restrict distributional shape.

- **[Time-LLM](https://arxiv.org/abs/2310.01728)** (2023). Reprograms time-series patches into representations consumed by a frozen text language model, with prompt context. This transfer mechanism differs from Chronos; whether the language backbone adds value requires component ablations.

- **[Language-backbone ablations](https://arxiv.org/abs/2406.16964)** (2024). Tan et al. remove or replace language backbones in three LLM forecasters; simpler variants match or improve forecasts with less compute. Evidence concerns those architectures and tasks, not all uses of language with time series.

## Forecast combinations and tabular learners

- **[Feature-based forecast model averaging](https://www.sciencedirect.com/science/article/pii/S0169207019300895)** (2020). Learns combination weights from time-series features and training-series forecast errors. Transfers a weighting rule to new series; differs from choosing one model or training a single global forecaster.

- **[Global boosted trees and forecast averaging](https://www.sciencedirect.com/science/article/pii/S0169207021001813)** (2022). The M5 winner averages direct and recursive LightGBM forecasts trained on several data pools. Combines cross-series learning with different multi-step strategies; gains cannot be assigned to the tree learner alone.

## Coherence, uncertainty and scoring

- **[Minimum-trace reconciliation](https://robjhyndman.com/papers/MinT.pdf)** (2017). Projects base forecasts onto aggregation constraints using forecast-error covariance. Minimizes total variance among linear unbiased reconciliations under its assumptions; covariance estimation affects practical performance.

- **[Probabilistic forecast reconciliation](https://robjhyndman.com/publications/coherentprob/)** (2023). Maps joint forecast distributions or samples onto aggregation constraints; learns weights with energy or variogram scores. Extends point reconciliation: coherent means alone do not specify a coherent joint distribution.

- **[Proper scoring rules](https://sites.stat.washington.edu/raftery/Research/PDF/Gneiting2007jasa.pdf)** (2007). Scores such as log score and CRPS evaluate forecast distributions, rewarding truthful reporting in expectation. Assess calibration and sharpness together; point-error improvements do not establish better uncertainty estimates.

- **[Target-consistent forecast scores](https://arxiv.org/abs/0912.0902)** (2009). Choose the target before ranking forecasts: squared loss elicits a mean, absolute loss a median, and pinball loss a quantile. Asymmetric decision costs can require a different target; changing metrics can change the optimal forecast.

- **[EnbPI](https://proceedings.mlr.press/v139/xu21h.html)** (2021). Builds sequential prediction intervals from ensemble residuals. Approximate marginal coverage relies on error dependence and estimation assumptions; it is not unconditional finite-sample coverage under arbitrary time-series shift.

## Comparative evidence and evaluation

- **[M4 competition](https://purehost.bath.ac.uk/ws/portalfiles/portal/192035784/IJF_2019_M4_Conclusions_post_print_.pdf)** (2020). Across 100,000 series, a hybrid of exponential smoothing and recurrent networks won the point-forecast competition; combinations were prominent. These mostly univariate tasks differ from covariate-rich retail forecasting in M5.

- **[M5 accuracy competition](https://doi.org/10.1016/j.ijforecast.2021.11.013)** (2022). Evaluates 42,840 hierarchical Walmart sales series with covariates. Top submissions predominantly used global LightGBM models and combinations; this retail result does not establish a universal ranking over statistical and neural forecasters.

- **[M5 robustness across test periods](https://eprints.lancs.ac.uk/id/eprint/159736/)** (2021). Re-evaluation finds global LightGBM bottom-up forecasts strong at product level but less robust after aggregation across test periods. Cross-series error correlations affect totals; one test window cannot establish stable rankings.

- **[Monash forecasting archive](https://arxiv.org/abs/2105.06643)** (2021). Collects diverse datasets and baseline results for univariate and multivariate forecasting. Reusing its datasets requires matching horizons, splits and aggregation; dataset count alone does not make two reported averages comparable.

- **[GIFT-Eval](https://arxiv.org/abs/2410.10393)** (2024). Benchmarks pretrained and conventional forecasters across domains, frequencies and horizons. Includes pretraining data intended to avoid test overlap; zero-shot results must be read with the evaluated model’s actual training exposure.

- **[fev-bench](https://arxiv.org/abs/2509.26468)** (2025). Adds covariates, multivariate tasks and pairwise statistical comparisons to foundation-model evaluation. Results identify covariate support as valuable; rankings depend on task coverage, failures and known pretraining overlap.

- **[Rolling-origin evaluation](https://otexts.com/fpp3/toolbox.html)** (book). Fit preprocessing and models using only data available before each origin; score relevant horizons across multiple origins. Tune on earlier validation periods and retain a final test period. Random window splits can leak future information.

- **[Scaled errors and aggregation](https://otexts.com/fpp3/toolbox.html)** (book). MASE/RMSSE scale errors by training naïve differences; constant training series can give zero denominators. Report scaling, horizon weights and aggregation: product-level scores and aggregate-demand scores measure different errors.

## Software

- **[StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/index.html)** (documentation). Implements statistical forecasters including AutoARIMA, AutoETS and intermittent-demand methods, with forecasting and cross-validation interfaces. Useful for matched statistical baselines; inspect each model’s exogenous-input support.

- **[GluonTS](https://ts.gluon.ai/stable/)** (documentation). Provides probabilistic forecasting models, dataset transformations and evaluation tools. Keep training windows, covariates, likelihoods and sampling settings explicit when comparing its models with point-forecast libraries.

## Related topics

[Anomaly detection](https://github.com/mlpapers/anomaly-detection) · [Continual learning](https://github.com/mlpapers/continual-learning) · [Model predictive control](https://github.com/mlpapers/model-predictive-control) · [Evaluation](https://github.com/mlpapers/evaluation) · [Bayesian inference](https://github.com/mlpapers/bayesian-inference) · [Models](https://github.com/mlpapers/models)
