## 4. Empirical Analysis of ETFs: XLRE Sector Exposure

This section presents a detailed empirical analysis of the XLRE (Real Estate Sector SPDR Fund) and its top holdings using statistical techniques such as daily returns computation, covariance matrix analysis, Principal Component Analysis (PCA), and Singular Value Decomposition (SVD). The analysis aims to uncover the underlying risk factors and co-movements within the real estate sector.

### Data Collection and Returns Computation

For this analysis, daily historical price data for the XLRE and its top 25 holdings (PLD, AMT, CCI, EQIX, PSA, SPG, DLR, WELL, O, EXR, REXR, VICI, SBAC, EQR, HST, KIM, WY, CUBE, MAA, ESS, FR, BXP, SLG, ARE, PEAK) were collected from Yahoo Finance for a 121 trading day period from 2025-01-08 to 2025-07-07. Daily log returns were computed from these adjusted closing prices.

**Importance of Returns:**
Daily returns, representing the percentage change in price, are fundamental in financial analysis. Unlike raw prices, returns are stationary, making them suitable for statistical modeling. They normalize the data across different assets, allowing for meaningful comparisons and aggregation. Returns are crucial for:
* **Risk Modeling:** Quantifying volatility and downside risk.
* **Portfolio Optimization:** Determining optimal asset allocations based on risk-return trade-offs.
* **Performance Attribution:** Decomposing portfolio performance into various contributing factors.
* **Co-movement Analysis:** Understanding how assets move together, which is essential for diversification.

### Covariance Matrix Analysis

The covariance matrix quantifies the degree to which the returns of different assets move in tandem. A positive covariance indicates that assets tend to move in the same direction, while a negative covariance suggests they move in opposite directions.

**Figure 1: Covariance Matrix of XLRE Holdings Daily Log Returns**
![Covariance Matrix](covariance_matrix_xlre.png)

The heatmap of the covariance matrix visually represents these relationships. In the real estate sector, it is common to observe generally positive covariances among holdings, indicating that sector-specific factors often drive the returns of individual companies within it. High positive values suggest strong co-movement, implying limited diversification benefits from simply combining these assets without further analysis.

### Principal Component Analysis (PCA)

PCA is a powerful dimensionality reduction technique that transforms a set of possibly correlated variables into a set of linearly uncorrelated variables called principal components. These components are ordered such that the first component explains the largest possible variance, and each subsequent component explains the highest remaining variance.

**Eigenvectors and Eigenvalues:**
* **Eigenvalues** (or `explained_variance_` in scikit-learn) represent the amount of variance explained by each principal component. Larger eigenvalues correspond to more significant components.
* **Eigenvectors** (or `components_` in scikit-learn) define the direction of the principal components in the original feature space. They indicate the weights or loadings of the original variables (asset returns) on each component.

**Variance Explained:**
Our PCA on the XLRE holdings returns revealed the following:
* **Component 1:** Explains 59.50% of the total variance.
* **Component 2:** Explains 13.23% of the total variance.
* **Component 3:** Explains 5.90% of the total variance.

This indicates that a significant portion of the sector's risk and return dynamics can be captured by a very small number of underlying factors.

**Figure 2: Scree Plot - PCA on XLRE Holdings Returns**
![PCA Scree Plot](pca_scree_plot_xlre.png)

The scree plot visually confirms this, showing a sharp drop in explained variance after the first few components, suggesting that these initial components are the most important drivers.
In the real estate sector, the first principal component typically represents the **overall market factor** affecting all real estate companies (e.g., interest rate sensitivity, economic growth outlook). The second and third components might capture **style factors** (e.g., growth vs. value, REIT vs. non-REIT real estate companies) or **sub-sector specific effects** (e.g., residential vs. commercial, data centers vs. retail). For instance, a high loading on a specific component for a particular REIT might indicate its sensitivity to that underlying factor.

### Singular Value Decomposition (SVD)

SVD is a matrix factorization technique that decomposes a matrix into three other matrices: $U$, $S$, and $V^T$. When applied to a mean-centered data matrix, SVD is closely related to PCA. The singular values (elements of $S$) are the square roots of the eigenvalues of the covariance matrix.

**Figure 3: Singular Values - SVD on XLRE Holdings Returns**
![SVD Singular Values Plot](svd_plot_xlre.png)

The plot of singular values shows a similar pattern to the PCA scree plot, with the first few singular values being significantly larger than the rest. Higher singular values correspond to more dominant latent factors influencing the dataset. SVD provides a numerically stable way to perform this decomposition and can be particularly useful in cases involving data compression or noise reduction.

### Comparison of PCA and SVD

While both PCA and SVD are powerful tools for dimensionality reduction and identifying latent factors, they approach the problem from slightly different angles:
* **PCA** directly operates on the covariance (or correlation) matrix, interpreting its eigenvectors as principal components and eigenvalues as explained variance. It focuses on finding directions of maximum variance.
* **SVD** decomposes the data matrix itself (typically mean-centered). The singular values from SVD are directly proportional to the square roots of the eigenvalues from PCA. The right singular vectors ($V^T$) are equivalent to the principal components (eigenvectors) when applied to mean-centered data.

**In essence, SVD offers a more numerically stable and general approach to matrix decomposition, and it provides an equivalent and often preferred method for performing PCA on mean-centered data.** Both methods consistently show that a small number of latent components explain the vast majority of variation in the XLRE holdings.

### Conclusion

This empirical analysis demonstrates that the movements of individual real estate sector ETFs are not independent but are largely driven by a few common underlying factors. PCA and SVD effectively identify these dominant factors (e.g., overall market level, specific sector trends). This insight is invaluable for:
* **Factor-Based Investing:** Constructing portfolios that target specific risk factors.
* **Risk Management:** Identifying and hedging the primary sources of risk in a portfolio.
* **Portfolio Simplification:** Reducing the complexity of a portfolio while retaining most of its information content.

By understanding these latent structures, investors can make more informed decisions, build more robust portfolios, and gain deeper insights into the dynamics of the real estate sector.