# Intelligent Monitoring of Infrastructure
Developing a data-driven "Digital Twin" to predict and reconstruct structural vibrations in aging electrical grids using DMD, PINNs, and Optimal Sensing.
## The Challenge
Aging Infrastructure & Wind-Induced Fatigue Text: Overhead powerlines are the backbone of the energy grid, but they are under constant attack from Wind-Induced Vibrations (WIV), specifically Aeolian vibrations. These high-frequency oscillations cause cumulative fatigue, leading to mechanical wear and catastrophic failures—such as the 2018 Camp Fire in California.

Traditional mitigation (like passive dampers) is reactive and lacks adaptability. To move toward proactive asset management, we need a way to monitor these vibrations in real-time. However, placing sensors along every inch of a thousand-mile grid is physically and financially impossible.

## Data - Driven Modeling
Stable Reduced-Order Modeling via DMD Text: Physical simulations (FEM) are too slow for real-time use. I leveraged Dynamic Mode Decomposition (DMD) to build a linear, reduced-order model directly from time-series data.

### The Stability Challenge 
Naive DMD often produces unstable models (eigenvalues outside the unit circle).
### The Solution 
I integrated Tikhonov Regularization into the DMD framework. By adding a penalty term to the objective function, I stabilized the state-transition matrix without sacrificing the fidelity of the modal structures.

## Real-time Estimation
To track the state of the powerline in real-time under partial observability, I implemented two complementary filtering strategies:

Kalman Filter: Used for efficient, linear-Gaussian state reconstruction, fusing the DMD model's predictions with real-time sparse sensor data.

Particle Filter: Implemented as a robust, non-parametric alternative to handle non-linearities and non-Gaussian noise, ensuring reliability during anomalous vibration events.

## The Safety-Net
 Real-world sensors often fail or lose data packets. I applied Compressive Sensing (CS) to ensure the system remains operational during data loss.

Method: By exploiting the sparsity of vibration signals in the Discrete Cosine Transform (DCT) domain and solving an $\ell_1$-minimization problem (Basis Pursuit), I successfully reconstructed signals from as little as 6% of the original data.
