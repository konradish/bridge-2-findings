# Noise Substitution: Theoretical Grounding

**Date**: 2026-03-09
**Context**: Connecting the dropout sweep findings to established regularization theory.

## Our Finding

Signal noise (σ=0.3 Gaussian in the memory channel) and dropout noise (Bernoulli masking to zeros) are substitutes. The optimal dropout rate for stochastic signal (~10-30%) is much lower than for deterministic signal (~80%). Combining high dropout with high noise degrades performance catastrophically.

## Literature Support

### 1. Gaussian Noise Injection = Tikhonov Regularization

Camuto et al., "Explicit Regularisation in Gaussian Noise Injections" (NeurIPS 2020, arXiv:2007.07368).

For sufficiently small noise σ, Gaussian noise injection is mathematically equivalent to Tikhonov regularization. The noise penalizes high-frequency components in the Fourier domain, especially in layers closer to the output. This is the same effect as L2 weight penalty.

**Implication**: Our noisy handcrafted signal (σ=0.3 Gaussian added to features) acts as an implicit Tikhonov regularizer on the memory channel. This is mathematically equivalent to adding weight decay on the memory-processing weights.

### 2. Dropout = Multiplicative Noise Regularization

Srivastava et al., "Dropout: A Simple Way to Prevent Neural Networks from Overfitting" (JMLR 2014).

Dropout (Bernoulli masking) and Gaussian multiplicative noise are equivalent forms of regularization. Wang & Manning (2013) showed dropout can be seen as Monte Carlo approximation of an implicit loss function, and Gaussian noise better approximates this function.

**Implication**: Our memory channel dropout (replacing signal with zeros) is another form of noise-based regularization. It's not additive noise (like the NoisyHandcrafted) but multiplicative/masking noise.

### 3. Combining Noise Sources = Over-Regularization Risk

"Navigating Noise: A Study of How Noise Influences Generalisation and Calibration" (arXiv:2306.17630, 2023).

Key finding: combining multiple noise sources requires careful balancing. Benefits don't consistently transfer across domains. Practitioners must carefully consider noise combinations.

**Implication**: Combining signal noise (additive Gaussian) with dropout noise (Bernoulli masking) can over-regularize. Our noisy_drop80 result (10% zeros, 0% noisy) is exactly this — doubly regularized, the optimizer can't find good solutions.

## The Substitution Mechanism

Both noise types serve the same function: preventing the agent from co-adapting with the memory signal. They do this by:
1. Making the signal unreliable (dropout: sometimes absent; noise: always varying)
2. Penalizing weight configurations that rely heavily on signal features

Since both achieve the same regularization effect, using both at high intensity is redundant and harmful:
- Each alone provides sufficient regularization
- Combined, they create an optimization landscape too noisy for CMA-ES with 5 eval episodes
- The fitness signal-to-noise ratio drops below what the optimizer needs

## Quantitative Mapping

Our total regularization budget can be roughly estimated as:

**Effective regularization ≈ f(signal_noise) + g(dropout_rate)**

Where both f and g are monotonically increasing. The optimal total regularization is bounded — too little → co-adaptation (NCL), too much → optimization failure.

For our setup:
- Deterministic signal (f=0): g must be ~0.8 (80% dropout) to prevent NCL
- Stochastic signal (f≈0.3): g should be ~0.1-0.3 (10-30% dropout)
- Both high (f=0.3, g=0.8): total exceeds optimum → collapse

## Prediction for LLM Commentator

The LLM produces naturally stochastic output. Its effective signal noise depends on:
- Temperature parameter
- Context window effects
- Embedding dimension (higher dim → more noise dimensions)

Estimated effective noise σ ≈ 0.2-0.5 (needs measurement). Predicted optimal dropout: 10-20%.

## References

- Camuto et al. (2020). "Explicit Regularisation in Gaussian Noise Injections." NeurIPS. arXiv:2007.07368
- Srivastava et al. (2014). "Dropout: A Simple Way to Prevent Neural Networks from Overfitting." JMLR 15.
- Wang & Manning (2013). "Fast Dropout Training." ICML.
- Nalisnick et al. (2019). "Dropout as a Structured Shrinkage Prior." ICML.
- "Navigating Noise" (2023). arXiv:2306.17630
