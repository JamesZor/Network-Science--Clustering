# Southern Women Dataset Analysis

This project demonstrates the application of network science concepts to the classic Southern Women dataset, illustrating various analytical techniques and their interpretations.

## Dataset Overview

The Southern Women dataset, collected by Davis et al. [1] in the 1930s, records the attendance of 18 women at 14 informal social events in Natchez, Mississippi. This dataset serves as an excellent example for studying bipartite networks and social structures.

![Bipartite graph representation](figures/bipartite_graph_plot.png)

*Figure 1: Bipartite graph representation of the Southern Women dataset. Open circles represent women, shaded circles represent events.*

## Incidence Matrix

The incidence matrix is a fundamental representation of bipartite networks. For our dataset with $l = |V|$ events and $n = |U|$ women, the incidence matrix $\mathbf{B} \in \mathbb{N}_{+}^{l \times n}$ is defined as:

$$
\mathbf{B}_{ij} = \begin{cases}
1 & \text{if woman } j \text{ attended event } i, \\
0 & \text{otherwise.}
\end{cases}
$$

![Affiliation matrix](figures/incidence_matrix_plot.png)

*Figure 2: Affiliation matrix of the Southern Women dataset.*

The incidence matrix B exhibits a notable block structure, which can be represented as:

$$
\mathbf{B} = \begin{bmatrix}
    \mathbf{A}_1& \mathbf{0} \\
    \mathbf{0} & \mathbf{A}_2
\end{bmatrix}
$$

where $\mathbf{A}_i$ are non-zero submatrices, and $\mathbf{0}$ represents (near) zero submatrices.

## One-Mode Projections

One-mode projections allow us to analyze relationships within a single set of nodes. For the women's projection:

$$
\mathbf{R} = \mathbf{B}^T \mathbf{B}
$$

Where $\mathbf{R}_{ij}$ represents the number of events both women $i$ and $j$ attended.

![One-mode projections](figures/bipartite_projection.png)

*Figure 3: One-mode projections of the Southern Women network.*

For the events projection:

$$
\mathbf{R}' = \mathbf{B}\mathbf{B}^T
$$

## Density

The density $\rho$ of a bipartite graph is calculated as:

$$
\rho_b = \frac{|E|}{|U| \times |V|}
$$

For our dataset, $\rho_b = 0.3532$.

![Density comparison](figures/bipartite_matrices_comparison.png)

*Figure 4: Affiliation matrices with varying cluster numbers, demonstrating the effect on density.*

For a bipartite graph with $k$ clusters, we can approximate the upper bound on density as:

$$
\rho_b \approx \frac{1}{k}
$$

## Centrality Measures

We explore several centrality measures:

1. **Degree Centrality**: $C_D(v) = \frac{deg(v)}{n - 1}$
2. **Eigenvector Centrality**: $\mathbf{Ax} = \lambda\mathbf{x}$
3. **Katz Centrality**: $\mathbf{x} = \alpha(\mathbf{I} - \beta\mathbf{A})^{-1}\mathbf{1}$

![Centrality measures](figures/centralities_bipartite_graph.png)

*Figure 5: Centrality measures for the Southern Women dataset.*

## Clustering

We compare various clustering algorithms, including Louvain, Girvan-Newman, Label Propagation, and spectral clustering methods.

| Algorithm | Category | Time Complexity | Requires k |
|-----------|----------|-----------------|------------|
| Louvain [2] | Graph-based | $O(N \cdot \log{N})$ | No |
| Girvan-Newman (GN) [3] | Edge betweenness | $O(|V|\cdot|E|^2)$ | No |
| Label Propagation (LP) [4] | Graph-based | $O(\cdot|E|)$ | No |
| Leading Eigenvector (LE) [5] | Graph-based | $O((|V|+|U|)^2 + |E|)$ | No |
| Spectral Clustering (SC) [6] | Graph-based | $O(k \cdot |V|^2)$ | Yes |
| K-means (KM) [7] | Traditional | $O(k \cdot |U| \cdot |V| )$ | Yes |
| K-medoids (KM+) [8] | Traditional | $O(k \cdot |U|^2 \cdot |V|)$ | Yes |
| BGC [9] | Specialized | $O((|E| + |U| \cdot k )\cdot \beta)$ | Yes |
| FNEM [9] | Specialized | $O(|E|\cdot \beta + |U|\cdot\beta^2 + |U|\cdot k^2 )$ | Yes |
| SNEM [9] | Specialized | $O(|E|\cdot \beta +|U|\cdot\beta^2 + |U|\cdot k)$ | Yes |

*Table 1: Overview of clustering algorithms. Note: $\beta$ is the dimensionality of low-rank approximation [9], and $N =|U \cup V|$.*

## Results and Evaluation

We evaluate clustering results using metrics such as Accuracy (Acc), F1 score (F1), Normalized Mutual Information (NMI), and Adjusted Rand Index (ARI).

| Method | Acc (k=2) | F1 (k=2) | NMI (k=2) | ARI (k=2) | Time (ms) |
|--------|-----------|----------|-----------|-----------|-----------|
| Louvain | 0.67 | 0.80 | 0.57 | 0.45 | 11.20 |
| Girvan Newman | 0.89 | 0.91 | 0.66 | 0.68 | 91.58 |
| Label Propagation | 0.61 | 0.54 | 0.16 | 0.03 | 1.43 |
| K-means | 1.00 | 1.00 | 1.00 | 1.00 | 3,344.13 |
| K-medoids | 0.78 | 0.77 | 0.39 | 0.27 | 1,007.48 |
| BGC | 0.50 | 0.33 | 0.00 | 0.00 | 6.76 |
| FNEM | 0.50 | 0.33 | 0.00 | 0.00 | 52.33 |
| SNEM | 0.50 | 0.33 | 0.00 | 0.00 | 39.69 |
| LE | 0.50 | 0.33 | 0.00 | 0.00 | 10.41 |
| SC | 1.00 | 1.00 | 1.00 | 1.00 | 4.46 |

*Table 2: Evaluation metrics for clustering methods (k=2)*

## Conclusion

This analysis demonstrates the application of various network science techniques to the Southern Women dataset, showcasing the power of these methods in uncovering social structures and relationships within bipartite networks. The comparative study of different clustering algorithms reveals their strengths and limitations in analyzing this classic dataset.

## References

[1] Davis, A., Gardner, B. B., & Gardner, M. R. (1941). Deep South: A Social Anthropological Study of Caste and Class. University of Chicago Press.

[2] Blondel, V. D., Guillaume, J. L., Lambiotte, R., & Lefebvre, E. (2008). Fast unfolding of communities in large networks. Journal of statistical mechanics: theory and experiment, 2008(10), P10008.

[3] Girvan, M., & Newman, M. E. (2002). Community structure in social and biological networks. Proceedings of the national academy of sciences, 99(12), 7821-7826.

[4] Raghavan, U. N., Albert, R., & Kumara, S. (2007). Near linear time algorithm to detect community structures in large-scale networks. Physical review E, 76(3), 036106.

[5] Newman, M. E. (2006). Finding community structure in networks using the eigenvectors of matrices. Physical review E, 74(3), 036104.

[6] Von Luxburg, U. (2007). A tutorial on spectral clustering. Statistics and computing, 17(4), 395-416.

[7] MacQueen, J. (1967). Some methods for classification and analysis of multivariate observations. In Proceedings of the fifth Berkeley symposium on mathematical statistics and probability (Vol. 1, No. 14, pp. 281-297).

[8] Kaufman, L., & Rousseeuw, P. J. (2009). Finding groups in data: an introduction to cluster analysis (Vol. 344). John Wiley & Sons.

[9] Yang, R., & Shi, J. (2024). Efficient high-quality clustering for large bipartite graphs. Proceedings of the ACM on Management of Data, 2(1), 1-27.
