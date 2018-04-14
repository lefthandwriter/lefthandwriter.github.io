I plan on documenting here a series of flash-decks that I'd previously made on previous courses I've taken. The reasons are two-fold:

1. Serve as a memory bank to refer to should I ever lose my original files
2. Serve as a case example for the ever-going debate of "how does one study effectively?"

I started doing flash-decks in the Fall of 2016, out of ruthless intent to make sure I could function on recallation and [not fall in the trap of recognition during a test](https://www.scotthyoung.com/blog/2015/06/22/stop-forgetting/) (but more on that next time).

Here, I start with an excerpt of my flash-deck for ECE6254 - Statistical Machine Learning.


## PCA

| How is PCA the same as *classical* MDS? What is the subtle difference? | - Both give the same low-dimensional embedding.￼ - In PCA, we have all the observations.  - In MDS, we only have the distance matrix, D. - PCA also gives A and u, and we have the original x_i.￼ MDS only gives us the mapping A’(x-u)￼ |
|------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| What is “classical” MDS?                                               | When the distance metric used is Euclidean distance.                                                                                                                                                                                     |
| Describe how to perform out-of-sample extension for MDS.               |                                                                                                                                                                                                                                          |
| Why would we kernelize PCA? Describe how you would kernelize PCA.      | - Capture nonlinear structure in the data. - Form Kernel matrix with the centering matrix. - Compute eigen-decomposition of the kernel matrix. - Set theta = first r rows of ￼(*V**Λ*1/2)*T*                                             |
| What is Isomap and how is it different from *classical* MDS?           | - Isomap = Isometric feature mapping:assumes data lives on a low-dimensional manifold - Is given a dataset x1..x entries to compute D using geodesic distance (not Euclidean distance)                                                   |
| How does Isomap estimate the geodesic distance?                        | - Computes the shortest paths in a proximity graph. (Refer: Spectral Clustering and Graph Laplacian).   - The distance matrix, D: set d_ij = length of shortest path from node i to node j in the graph described by W                   |
| What is LLE’s criticism of Isomap?                                     | - LLE = locally linear embedding:points that are far away will have a less accurate geodesic measurement - LLE instead models local pieces of the manifold, and then patches them together.                                              |
| Describe the LLE algorithm.                                            | Given datapoint*x*1..*x**n* - define a local neighbourhood   -solve least squares problem to get W   - fix W and solve for eigenvalues                                                                                                   |


