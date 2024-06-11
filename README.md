# Blind Source Separation in Neuroscience 

In this project, we brought Polytopic Matrix Factorization (PMF) that provides *identifiable polytopes* to extend feature attributes of latent factors to the neuroscience realm to extract latent vector components associated with distinct subnetworks. Due to the absence of ground truths for the sources expected to be extracted from EEG signals, we used the best-fitted dipole as the ground truth and residual variance as the error metric.

## Mathematical Framework

The framework that PMF considers is a semi-structured data model, in which the input matrix, **X**, is modeled as the product of a full column rank matrix and a matrix containing samples from a polytope as its column vectors:

\[ \mathbf{X} = {\mathbf{W}_g}{\mathbf{H_g}}, {\mathbf{W}_g}\in \mathbb{R}^{M \times r}, {\mathbf{H_g}} \in \mathbb{R}^{r \times N} \]

\[ H_{j} \in \mathcal{P}, \quad j = 1, \ldots, N. \]

where \( r \leq \min \{M,N\} \) and \( r \) denotes the *factorization rank*. The subscript \( g \) denotes the ground truth of the factor matrices, and the convex polytope is defined by

\[ \mathcal{P} = \{ \mathbf{x} \mid \langle \mathbf{a}_i, \mathbf{x} \rangle \leq b_i, \, i = 1, \ldots, f \}, \]

where \( f \) is the number of faces, and vectors \( \mathbf{a}_i \) are the face normals. The choice of the polytope indicates the assumed characteristics of the latent components. PMF aims to factor \( \mathbf{X} \) in the form \( \mathbf{WH} \) such that

\[ \mathbf{W} = {\mathbf{W}_g} \mathbf{\Pi}^T \mathbf{D}^{-1}, \]

\[ \mathbf{H} = \mathbf{D} \mathbf{\Pi} {\mathbf{H_g}}, \]

where \( \boldsymbol{\Pi} \in \mathbb{R}^{r \times r} \) is a permutation matrix that represents the irresolvable ambiguity in obtaining the ordering of the columns of the factor matrices, and \( \mathbf{D} \in \mathbb{R}^{r \times r} \) is a full column rank matrix that represents scaling ambiguity \cite{PMF}. In the literature, it is shown that all polytopes that comply with a specific symmetry restriction qualify for the PMF framework, and they are referred to as identifiable polytopes \cite{PMF}. The availability of an infinite number of polytopes provides flexibility in characterizing latent vector components.

For the identification of factor matrices, *determinant-maximization*, which has been utilized for NMF \cite{SCHACHTNER2011528}, is proposed. Since the determinant of the sample autocorrelation matrix is used as a scattering measure, the problem of extracting sources could be formulated as the following optimization problem:

\[
\begin{aligned}
& \underset{\mathbf{W} \in \mathbb{R}^{M \times r}, \mathbf{H} \in \mathbb{R}^{r \times N}}{\text{maximize}} 
& & \det(\mathbf{H}\mathbf{H}^T) \\
& \text{subject to} & & \mathbf{X} = \mathbf{W}\mathbf{H}, \\ 
& & & \mathbf{H}_{:,j} \in \mathcal{P}, \quad j = 1, \ldots, N.
\end{aligned}
\]

<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
