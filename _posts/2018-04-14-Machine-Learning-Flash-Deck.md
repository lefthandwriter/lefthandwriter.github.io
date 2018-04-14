# Statistical Machine Learning Flash-Deck

I plan on documenting here a series of flash-decks that I'd previously made on previous courses I've taken. The reasons are two-fold:

1. Serve as a memory bank to refer to should I ever lose my original files
2. Serve as a case example for the ever-going debate of "how does one study effectively?"

I started doing flash-decks in the Fall of 2016, out of ruthless intent to make sure I could function on recallation and [not fall in the trap of recognition during a test](https://www.scotthyoung.com/blog/2015/06/22/stop-forgetting/) (but more on that next time).

Here, I start with an excerpt of my flash-deck for ECE6254 - Statistical Machine Learning.


## Bayesian Inference
1. In the Bayes classifier, what is a posteriori class probability? What is the a priori class probability?

 A posteriori class conditional probability: P(Y=k | X=x) i.e. The probability that Y takes on label k, given that X is the feature x.

 A priori class probability: P(Y=k) i.e. The probability of the event that Y = k"

2. What is the Bayes Rule for classification (consider discrete labels and continuous features)

 P(Y=k | X=x) = ( P(Y=k) * fx|y (x | k) ) / ( sum(P(Y=k) * fx|y(x | k) )

3. What is Bayes Classifier?	
  
 Denoted: h*
 
 Satisfies argmax(LHS) or argmax(RHS)"

4. What is the Bayes Risk? I.e. risk of Bayes classifier.

 Denoted: R(*h*<sup>\*</sup>)

 The best (lowest risk), *R*<sup>\*</sup> = R(*h*<sup>\*</sup>) <= R(h)

5. What is the proof that the Bayes classifier is the best classifier (i.e. hypothesis that results in lowest possible risk).

 Start with 1-R(h) = P(h(X) = Y)
 
 apply law of total probability

 apply cdf = integrate(pdf)

 the resulting expression is the numerator in Bayes rule

 now equate it to the remaining terms in Bayes rule: LHS denominator
 
 ask: what maximises that expression?

6. What is the limitation in practicality of the Bayes classifier?

 It requires complete knowledge of the conditional pdf / pmf.  
 
 i.e. P(Y=k | X=x) or a posteriori class probability"

7. What are the assumptions of nearest neighbour classifier?	

 For any x, find the closest xi in the training set and assign x the same label as its nearest neighbour.

8. Show that nearest neighbour risk is at most twice the Bayes Risk, as n approaches infinity.	

9. Is minimising the risk P(h(X) not equal Y) always effective? If no, what are the alternatives?

 No.
Reason 1: misclassifying label 0 may be worse than label 1.
Reason 2: unbalanced datasets - when one class dominates the other. 

 Alternative: assign a weighting factor to penalise the costs differently."

10. What are plugin methods?

 Recall that the limitation of the Bayes Classifier is that we know the conditional pdf / pmf of the class distributions, or joint distributions (X,Y). Plugin methods are different ways to estimate this distribution, and “plug it in” into the Bayes Rule. They are simplistic and parametric.

 For example: we can assume that it has a Gaussian Distribution, and then we try to estimate the parameters (mean and variance).

11. What are some types of Plugin Methods?
 - Naive Bayes
 - Linear Discriminant Analysis (LDA)
 - Quadratic Discriminant Analysis (QDA)
 - Logistic Regression

12. What are the assumptions of Naive Bayes? What does it buy us? What are the two things we need to estimate for Naive Bayes? How do you estimate those two items? Why do we need Laplace smoothing?

 - Given y, features X(1)…X(d) are independent.
 - We can write the conditional pdf of x on y as product of all features.
fx|y (x | k) = product conditional probability of each feature given Y
                 = product from j = 1 to d (fx(j)y (x(j) | k))
 - Prior probabilities pi(k) and conditional probability for each feature given y
 - Count
 - In case we did not observe a certain feature x_j, our probability will not become zero (because of our product terms)."

13. What are the assumptions of LDA?

 - The distribution X|Y is a multivariate Gaussian distribution with mean uk and fixed covariance matrix. (Each class k in Y has different means but the same covariance).

14. What are the three things we need to estimate in LDA? And some funky terms? Why is it a linear classifier?"	

 - Prior probabilities, mean vectors and covariance matrix.
 - Mahalanobis distance
 - The decision boundaries is linear line. (Show line and norm from line)

15. What are QDA assumptions?

 - Same as LDA, only now we allow each class to have its own covariance matrix too.
 - The decision boundaries will be quadratic.

16. What are the weaknesses of LDA? What are some ways to go around it?

 - TOO MANY parameters to estimate!
 - Apply dimensionality reduction techniques so that d is small.
 - Assume a more structured covariance matrix (all values on diagonal are same, everywhere else 0). Results in Euclidean distance instead of Mahalanobis.
 - If n is large and d is small, we can use Hoeffding.

17. What are the assumptions of Logistic Regression?
 - Same as LDA! Distribution X|Y is a multivariate Gaussian with mean uk and fixed covariance matrix. However, we got to be careful. See next question.

18. Then what’s the difference?
 - It applies the full Bayes rule, instead of just the numerator of the RHS.
 - We can simplify it to an equation that looks like a sigmoid function. Sigmoid function crosses x=0 at 1/2.
 - So, since we apply the full Bayes rule, we are essentially making an assumption of eta(k), which is equivalent to making an assumption on Y|X, instead of X|Y.



## PCA

| What is all the intuition you can pull out from PCA?         | - Want to reduce from d dimensions to k dimensions - Want to project the principal components onto a subspace - Want to have high variance along the principal components? Intuition: better for separability - The principal components are the top k eigenvectors (corresponding to the top k eigenvalues) in the eigen-decomposition of S = XX’￼ |
|--------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| In the SVD of X, what do you get from it?                    | - Top k columns of U = principal eigenvectors - Top k rows of *Σ*V’ = principal components - *Σ*: singular values                                                                                                                                                                                                                                   |
| What are practical things you should do before applying PCA? | Make sure the data is centred and scaled (zero mean and unit variance)                                                                                                                                                                                                                                                                              |
| How should we select k (the desired lower dimension)?        | Remember, PCA is reducing dimensions in a way that minimises information loss. To faithfully represent the data as originally as possible, we want to minimize the sum of squares in the reconstruction error.                                                                                                                                      |
| When should we use PCA?                                      | - When the data forms a point cloud in space. - When the data is approximately Gaussian (or some other elliptical distribution). - When the low-rank subspace captures most of the variation.                                                                                                                                                       |


## Multi-Dimensional Scaling (MDS)
| How is PCA the same as *classical* MDS? What is the subtle difference? | - Both give the same low-dimensional embedding.￼ - In PCA, we have all the observations.  - In MDS, we only have the distance matrix, D. - PCA also gives A and u, and we have the original x_i.￼ MDS only gives us the mapping A’(x-u)￼ |
|------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| What is “classical” MDS?                                               | When the distance metric used is Euclidean distance.                                                                                                                                                                                     |
| Describe how to perform out-of-sample extension for MDS.               |                                                                                                                                                                                                                                          |
| Why would we kernelize PCA? Describe how you would kernelize PCA.      | - Capture nonlinear structure in the data. - Form Kernel matrix with the centering matrix. - Compute eigen-decomposition of the kernel matrix. - Set theta = first r rows of ￼(*V**Λ*1/2)*T*                                             |
| What is Isomap and how is it different from *classical* MDS?           | - Isomap = Isometric feature mapping:assumes data lives on a low-dimensional manifold - Is given a dataset x1..x entries to compute D using geodesic distance (not Euclidean distance)                                                   |
| How does Isomap estimate the geodesic distance?                        | - Computes the shortest paths in a proximity graph. (Refer: Spectral Clustering and Graph Laplacian). - The distance matrix, D: set d_ij = length of shortest path from node i to node j in the graph described by W                     |
| What is LLE’s criticism of Isomap?                                     | - LLE = locally linear embedding:points that are far away will have a less accurate geodesic measurement - LLE instead models local pieces of the manifold, and then patches them together.                                              |
| Describe the LLE algorithm.                                            | Given datapoint*x*1..*x**n* - define a local neighbourhood -solve least squares problem to get W - fix W and solve for eigenvalues                                                                                                       |

## Clustering
1. What gave rise to the idea of spectral clustering?	
 - Instead of forming clusters using a spherical or elliptical metric, view data points as a graph.

2. In a graph, what are: vertices, edges, weights?
 - Vertices are formed by the data points x_i.
 - Edges are two connected vertices.
 - Weights allow us to compare which two vertices are close to each other.

3. How would we represent an undirected graph?	
 - The weight matrix, W is symmetric.

4. What are the three common ways of defining adjacency between points?	
 - k-nearest neighbours
 - e-ball
 - complete graph

5. What are some ways of defining the edge weights?
 - Assigning a constant
 - Using a Gaussian measure

6. What is the graph Laplacian?
 L = D - W

7. What is the degree matrix, D?	
 - It is a diagonal matrix, whose diagonal elements are the weighted degree of each node.

8. Why do we perform eigen-decomposition / SVD in Spectral Clustering?	
 - In the graph Laplacian, we want to estimate a basis for the null space of L. This is the eigenspace corresponding to the k smallest eigenvalues of L.

9. What’s the difference between PCA and the eigen-decomposition in Spectral Clustering?	
 -In PCA, we want a basis for our feature space. We take the TOP k eigenvectors.
 - In Spectral Clustering, we want a basis for the null-space of L. We take the SMALLEST k eigenvectors."

10. Out of all the clustering methods discussed in class, which one does not require a priori determination of the number of clusters?
 DBSCAN!

11. What is the assumptions of .. and what are the implications?
 - Kmeans: assumes clusters are spherical in shape
 - GMMs: assumes clusters are elliptical in shape
 - Spectral Clustering: assumes a graph based connected cluster
 - Density based clustering: assumes clusters formed by dense regions, some datapoint may not be labelled, border points may be assigned to multiple clusters, does not require prior setting of number of clusters
 - Hierarchical Clustering: assumes clusters are nested inside larger ones"

12. What is the difference between Agglomerative Clustering and Divisive Clustering?	
 - Agglomerative is bottom up: builds a hierarchy by doing fine-grain and then merging clusters together
 - Divisive is top down: start with the entire dataset belonging to a single cluster; iterative dividing between existing clusters into smaller components


## Structured Matrix Factorization (SMF)
1. What is structured matrix factorisation?

2. How is Non-Negative Matrix Factorisation different from PCA?	
 - It doesn’t assume an orthonormality structure on the low-rank matrix. Instead, it just imposes that the components of B and C be non-negative.

3. What problems do NNMF constraints give us? How do we fix it? What is alternating minimization?
 - NNMF at its base level is intractable because: no closed form solution, is non-convex
 - Use alternating minimization: Fix B and then solve for C. Then, fix C and solve for B. Iterate until some convergence."

4. What is Dictionary Learning?
 - Again factorize X ~ BC, but now with the structure that C is sparse. In our minimization program, we have a target s, where s is the desired on nonzero entries in C.
 - B becomes the basis / dictionary, such that every datapoint x_i can be expressed as a weighted combination of a few columns of B."


5. What problems does Dictionary Learning give us?
 - "It is NP-Hard -> use alternating minimization strategy.
 - If B is orthonormal, then we just need to compute the s largest elements of y = B’x.

6. Talk about Robust PCA.
 - Normal PCA is sensitive to outliers (i.e. corrupted entries). Robust PCA is an algorithm that tries to be *robust* against outliers by trying to separate our desired low-rank matrix from the corrupted data."

7. What are the problems with Robust PCA and Matrix Completion?
 - Both problems are non convex and intractable.
 - To deal with it: Alternating minimization, apply Convex Relaxation.

8. What is Convex Relaxation?
 - Finding effective proxies for our constraints that act as convex constraints.

9. What are some examples for Convex Relaxations?
 - zero norm to 1-norm
 - rank(L) to nuclear norm





## Misc
1. "What is the difference between MLE and MAP?
 - MLE = maximum likelihood estimation.
 - MAP = maximum a posteriori"	"MLE: chooses a parameter that maximises the likelihood function.
 - MAP: maximizes the posteriori probability"

2. "What is the Risk of 1-NN Classifier?
3. What is the Risk of k-NN Classifier?"	

4. "How are LDA and GMM similar?
 - LDA = linear discriminant analysis.
 - GMM = gaussian mixture model.	
 - Both try to estimate the distribution of the datapoint (assumed Gaussian): the means, the covariance matrices.
 - Since GMM assumes the distribution to be a weighted combination of Gaussian pdfs, there is an additional parameter: the weights.
 - LDA: Use Gradient Descent.
 - GMM: Use Expectation-Maximization (EM)."

5. Why do we need EM for GMM?	
 - The derivation was based on knowledge of the clusters, which we don’t actually have (i.e. estimating the means, covariances and weights of the clusters). We have “incomplete data”. So, we first guess theta and compute the expected likelihood. Then, given this expected likelihood, we optimise theta to maximise this likelihood.





