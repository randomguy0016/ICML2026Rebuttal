# ICML 2026 Rebuttal (Submission number:9280)

## This anonymous repository contains additional tables and figures for ICML Submission 9280.

### Caption for Figure 3
we give Figure \ref{embedding} that visualizes the transformation of raw data (top row: blue for normal, pink for anomalies) via TPA-PD (pseudo dimensions) and TPA-HDE (high-dimensional embedding), with color intensity representing the magnitude of learned topological features. The visualization highlights two key effects: (1) enhanced separability, where anomalous regions (bright/dark hues) become distinct from normal ones in the embedding space, contrasting with their entanglement in raw data; and (2) topological discrimination, mapping structurally dissimilar regions (e.g., disconnected components) to spatially distant locations, effectively "untangling" complex geometries.

### Caption for Figure 4
Line plot of model accuracy across several baselines, illustrating performance improvements with the proposed method across different baselines.

### Caption for Figure 6 (Extensive Experiment)
Performance comparison (MSE) across different baseline models using original features versus the proposed TPA-feature.

### Experimental Setup

|    **Dataset**    | **Protein** | **Fall**  | **Trajectory** |  **PEMS04**   |
| :---------------: | :---------: | :-------: | :------------: | :-----------: |
|   Total Samples   |  (23279,3)  | (29337,3) |   (26770,2)    | (307,16992,3) |
|      Normal       |    20490    |   27888   |     21588      |       -       |
|      Anomaly      |    2789     |   1449    |      5182      |       -       |
| Enhanced Features |      3      |     6     |       4        |       4       |

### Hyperparameters

|     **Component**      |       **Parameter**        | **Value** |
| :--------------------: | :------------------------: | :-------: |
|        **TPA**         | Regularization $\\lambda$  |  $10^6$   |
|                        |       KNN Neighbors        |    10     |
|                        |  Optimization Iterations   |    10     |
|                        | Clustering Threshold ($c$) |    0.4    |
|                        |      Max Edge Length       |     5     |
|                        |         Optimizer          | L-BFGS-B  |
|      **NNG-MIX**       |    KNN Neighbors ($k$)     |     5     |
|                        |       Label Strategy       | minority  |
|         **BP**         |           Epochs           |    500    |
|                        |         Batch Size         |    16     |
|                        |         Optimizer          |   Adam    |
|      **XGBoost**       |         Max Depth          |     3     |
|                        |        N Estimators        |    100    |
|                        |       Learning Rate        |    0.1    |
|        **GAN**         |      Latent Dimension      |    100    |
|                        |           Epochs           |    50     |
|                        |         Batch Size         |    32     |
|   **Deep OD Models**   |           Epochs           |    100    |
|   (DevNet, DeepSAD,    |         Batch Size         |    64     |
| PReNet, RoSAS, FeaWAD) |       Learning Rate        | $10^{-3}$ |


### Notation

| Notation | Definition |
| --- | --- |
| General Machine Learning |  |
| $\mathcal{X} \subseteq \mathbb{R}^d$ | $d$-dimensional input feature space |
| $\mathcal{Y} = {0, 1}$ | Binary label space |
| $D = {(x_i, y_i)}_{i=1}^n$ | Training dataset with $n$ i.i.d. samples |
| $F: \mathbb{R}^d \to {0, 1}$ | Classifier (decision function) |
| $\mathcal{P}, \mathcal{D}$ | Joint probability distribution and data distribution |
| $\mathcal{A}$ | Learning algorithm (stochastic) |
| $\theta$ | Model parameters |
| $\mathbb{Q}$ | Distribution over model parameters $\theta$ |
| Topology and Decision Boundary |  |
| $\mathbb{M}$ | Decision boundary manifold: ${z \in \mathbb{Z} \mid p_{Z|F}(z|1) = p_{Z|F}(z|0)}$ |
| $p_Z$ | Probability density function over space $\mathbb{Z}$ |
| $X$ | Training set viewed as a point cloud |
| $X_\mu \subset X$ | $\mu$-subset of training set where $|X_\mu|/|X| = \mu$ |
| $\mu$ | Subsampling ratio (typically $\mu \le 0.5$) |
| $\tau$ | $(\tau, \mu)$-decision boundary variability (Def. \ref{def3}) |
| $AV(f_{\mathbb{Q}}, \mathcal{D})$ | Algorithmic decision boundary variability (Eq. \ref{eqn-6}) |
| Topological Prototype Augmentation (TPA) |  |
| $\mathbb{R}^m, \mathbb{R}^{\bar{m}}$ | Original ($m$-D) and embedded ($\bar{m}$-D) data spaces, $m < \bar{m}$ |
| $\bar{m}-m$ | Number of pseudo-dimensions added |
| $M$ | Number of topological component learners ${f_i}_{i=1}^M$ |
| $F$ | Meta-model (combining component learners) |
| $r \in \mathbb{R}^M$ | Meta-features vector from topological components |
| $\Sigma = \mathrm{diag}(\sigma)$ | Diagonal scaling matrix for meta-features ($\sigma \ge 0$) |
| $y_+, y_-$ | Indices for positive and negative classes |
| $n_+, n_-$ | Number of positive/negative training samples |
| $C_+, C_-$ | Constants related to positive/negative classes in generalization bound |
| High-Dimensional Embedding |  |
| $T_j$ | High-dimensional embedding transformation for triangle $j$ |
| $J_j$ | Deformation gradient for triangle $j$ (QR decomposition) |
| $W_j, \bar{W}_j$ | Edge vectors before and after embedding for triangle $j$ |
| $X_j = {x_{j1}, x_{j2}, x_{j3}}$ | Vertices of triangle $j$ in original space |
| $\bar{X}_j = {\bar{x}_{j1}, \bar{x}_{j2}, \bar{x}_{j3}}$ | Vertices of triangle $j$ in embedded space |
| $D_j$ | Index (incidence) matrix for triangle $j$ |
| $N_m$ | Total number of triangles from Delaunay triangulation |
| $N_v$ | Total number of vertices in point cloud |
| $N(i)$ | Set of $K$ nearest neighbors of vertex $i$ |
| $K$ | Number of nearest neighbors |
| $E_1, E_2, E_3$ | Objective function terms: deformation, embedding regularization, topological regularization (Eqs. \ref{eqn-16}, \ref{eqn-17}, \ref{eqn-18}) |
| $\rho_1, \rho_2$ | Regularization hyperparameters for $E_2$ and $E_3$ |
| Persistent Homology and TDA |  |
| $PD(i)$ | Persistence diagram for local neighborhood of node $i$ |
| $W_2(\cdot, \cdot)$ | 2-Wasserstein distance between persistence diagrams |
| $H(\cdot)$ | Homology group (implicit in persistent homology references) |
| Theoretical Analysis |  |
| $\mathbb{R}_{\text{exp}}(\mathcal{D}, \mathbb{Q})$ | Expected risk (generalization error) of classifier $f_{\mathbb{Q}}$ |
| $\mathbb{R}(\mathcal{D}, \mathcal{A}(X))$ | Generalization error of algorithm $\mathcal{A}$ on dataset $X$ |
| $\phi(\cdot)$ | Margin cost function: $\phi(z) = \max(0, 1-z)$ for $z \le 1$, else $0$ |
| $\Lambda$ | Data-independent constant in generalization bounds |
| $\zeta, \delta$ | Confidence parameters (failure probabilities) |
| $\varphi$ | Upper bound on topological variability near decision boundary (Lemma \ref{l4}) |
| $\Omega, \Delta$ | Intermediate variables in Theorem \ref{t2}: $\Omega = \varphi + \sqrt{\frac{\log(1/\delta)}{2(1-\mu)n}}$, $\Delta = \mu \log \frac{e}{\mu} + \frac{1}{n}\log \frac{2}{\delta}$ |
| Characteristic Lattice Algorithm (CLA) |  |
| $\delta$ (CLA context) | Side length of hypercubes in subsampling grid (Lemma \ref{l5}) |
| $X_{\delta}^*$ | Subsampled point cloud using CLA with grid size $\delta$ |

