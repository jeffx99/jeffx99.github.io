---
layout: post
title: "A Geometric Interpretation of Linear Sketching"
date: 2022-08-07
categories: math
---

## The Count Sketch Algorithm

Consider a data stream $\\{q\_i\\}\_{i=1}^{\infty}$ of elements $q\_i$ each belonging to some finite set of outcomes $\mathcal{O} = \\{o\_1, \ldots, o\_N\\}$. Then at each moment $t$, one may define a *count vector* $\mathbf{x}(t) \in \R^N$ defined by
\begin{equation\*}
    x\_n(t) = \abs{\\{i \leq t \mid q\_i = o\_n\\}}.
\end{equation\*}
The <font style="font-variant: small-caps">count sketch</font> structure allows one to produce a good approximation to $\mathbf{x}(t)$, referred to as a *sketch*, using space sublinear in $t$. We describe the structure from a different, but equivalent, perspective than discussed in the [original document](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.95.695&rep=rep1&type=pdf) introducing the sketching algorithm.

### The "Abstract Sketch" Algorithm
Fix an integer $d \geq 0$ and consider the $d$-sphere $\mathbb{S}^d = \\{\mathbf{a} \in \R^{d+1} \mid \abs{\mathbf{a}} = 1\\}$. A map $\mathcal{O} \to \mathbb{S}^d$ may be thought of as a point on the product $X = (\mathbb{S}^d)^N$, which may be endowed with an appropriate measure. Thus, we may speak of choosing a random map $\xi \colon \mathcal{O} \to \mathbb{S}^d$ uniformly from $X$. Furthermore, denote $\xi\_{n} = \xi(o\_n)$, so that we may suppress $o\_n$ in our notation.

<div class="lemma">
$\mathbb{E}[\inner{\xi_n, \xi_m}] = \delta_{n,m}$
</div>
<div class="proof">
If $n = m$, then $\inner{\xi_n, \xi_m} = 1$ and the claim follows. Otherwise, by Fubini's theorem, one may simply integrate over $\mathbb{S}^{d} \times \mathbb{S}^d$ to obtain
\begin{equation}
    \mathbb{E}[\inner{\xi_n, \xi_m}] = \frac{1}{\operatorname{vol}(\mathbb{S}^d \times \mathbb{S}^d)}\int_{\mathbb{S}^{d} \times \mathbb{S}^d} \inner{\xi_n, \xi_m} \, \d \xi_n \d \xi_m,
\end{equation}
where we have made use of the fact that the distribution of $\xi$ is uniform. Now note that the map $(\mathbf{a}^1, \mathbf{a}^2) \mapsto (-\mathbf{a}^1, \mathbf{a}^2)$ on $\mathbb{S}^{d} \times \mathbb{S}^d$ is a measure-preversing bijection which flips the sign of the integrand. Hence $\mathbb{E}[\inner{\xi_n, \xi_m}] = 0$ if $n \neq m$.
</div>
<br>

<div class="lemma">
If $n \neq m$, then $\mathbb{E}[\inner{\xi_n, \xi_m}^2] = \frac{1}{d + 1}$.
</div>
<div class="proof">
By Fubini's theorem, we obtain that
\begin{equation}
    \mathbb{E}[\inner{\xi_n, \xi_m}] = \frac{1}{\operatorname{vol}(\mathbb{S}^d \times \mathbb{S}^d)}\int_{\mathbb{S}^{d} \times \mathbb{S}^d} \inner{\xi_n, \xi_m}^2 \, \d \xi_n \d \xi_m = \frac{1}{\operatorname{vol}(\mathbb{S}^d)^2}\int_{\mathbb{S}^{d}} \left(\int_{\mathbb{S}^d} \inner{\xi_n, \xi_m}^2 \, \d \xi_n \right) \, \d \xi_m.
\end{equation}
Let $\{\mathbf{f}_0, \ldots, \mathbf{f}_d\}$ be an orthonormal basis of $\R^{d+1}$. Consider an isometry $\varphi_j \colon \mathbb{S}^d \to \mathbb{S}^d$ which takes $\xi_m \to \mathbf{f}_j$. Since $\varphi_j$ is a measure-preversing bijection on $\mathbb{S}^d$,
\begin{equation}
    \int_{\mathbb{S}^{d}} \left(\int_{\mathbb{S}^d} \inner{\varphi_j(\xi_n), \mathbf{f}_j}^2 \, \d \xi_n \right) \, \d \xi_m = \int_{\mathbb{S}^{d}} \left(\int_{\mathbb{S}^d} \inner{\varphi_j(\xi_n), \mathbf{f}_j}^2 \, \d \xi_n \right) \, \d \xi_m = \int_{\mathbb{S}^{d}} \left(\int_{\mathbb{S}^d} \inner{\xi_n, \mathbf{f}_j}^2 \, \d \xi_n \right) \, \d \xi_m.
\end{equation}
It follows that
\begin{equation}
    \mathbb{E}[\inner{\xi_n, \xi_m}] = \frac{1}{\operatorname{vol}(\mathbb{S}^d)^2} \int_{\mathbb{S}^{d}} \left(\int_{\mathbb{S}^d} \inner{\xi_n, \mathbf{f}_j}^2 \, \d \xi_n \right) \, \d \xi_m = \frac{1}{\operatorname{vol}(\mathbb{S}^d)} \int_{\mathbb{S}^d} \inner{\xi_n, \mathbf{f}_j}^2 \, \d \xi_n.
\end{equation}
It remains to compute the resulting integral. Since $\{\mathbf{f}_j\}$ form an orthonormal basis, one may sum over $j$ to obtain
\begin{equation}\label{eq:basis_trick}
    (d + 1) \mathbb{E}[\inner{\xi_n, \xi_m}] = \frac{1}{\operatorname{vol}(\mathbb{S}^d)} \int_{\mathbb{S}^d} \sum_{j=0}^{d}\inner{\xi_n, \mathbf{f}_j}^2 \, \d \xi_n = 1.
\end{equation}
The claim follows.
</div>

Given such $\xi$, one defines the *$\xi$-sketch*
\begin{equation}
    S_\xi(\mathbf{x}) \bydef \sum_{n=1}^{N} x_n \xi_n = \sum_{i \leq t} \xi(q_i).
\end{equation}
The original count vector can be recovered in principle from the sketch via the linear map $T\_\xi = \sum\_{n=1}^{N} \inner{\cdot, \xi\_n} \mathbf{e}\_n$. Note that if $\{\xi\_n\}$ form a basis(which is generically true) and $d + 1 \geq N$, then $T\_\xi$ is automatically a left inverse to $S\_\xi$. Thus it is only fruitful to consider when $d < N - 1$, i.e., when the sketch reduces dimensionality.

<div class="theorem">
$S_\xi$ and $T_\xi$ are (right, left) inverses in expectation, i.e., $\mathbb{E}[T_\xi S_\xi] = \id$.
</div>
<div class="proof">
It suffices to show that $\mathbb{E}[T_\xi(S_\xi(\mathbf{x}))] = \mathbf{x}$. One has
\begin{align}
    T_\xi(S_\xi(\mathbf{x})) = \sum_{n=1}^{N} \inner{S_\xi(\mathbf{x}), \xi_n} \mathbf{e}_n &= \sum_{n=1}^{N} \sum_{m =1}^{N} x_m \inner{\xi_m, \xi_n} \mathbf{e}_n \\
    &= \sum_{n=1}^{N} \Bigg[ x_n + \sum_{m \neq n} x_m \inner{\xi_m, \xi_n} \Bigg] \mathbf{e}_n.
\end{align}
 By a previous lemma, one has $\mathbb{E}[\inner{\xi_m, \xi_n}] = 0$ for $m \neq n$. Thus, by linearity of expectation,
\begin{equation}
    \mathbb{E}[T_\xi(S_\xi(\mathbf{x}))] = \sum_{n=1}^{N} \Bigg[ x_n + \sum_{m \neq n} x_m \mathbb{E}\left[\inner{\xi_m, \xi_n}\right] \Bigg] \mathbf{e}_n = \sum_{n=1}^{N} x_n \mathbf{e}_n = \mathbf{x}.
\end{equation}
</div>
<br>

<div class="theorem">
Let $\mathbf{x}^{\xi} = T_\xi(S_\xi(\mathbf{x}))$ be the reconstruction of the $\xi$-sketch of $\mathbf{x}$. Then $\operatorname{Var}(x^\xi_n) = \frac{1}{d + 1} \abs{\Pi_n\mathbf{x}}^2$, where $\Pi_n$ is the projection sending $\mathbf{e}_m \mapsto \mathbf{e}_m$ for $m \neq n$ and $\mathbf{e}_n \mapsto 0$.
</div>
<div class="proof">
Since each $\xi_k$ is an independent random variable, it follows that
\begin{equation}
    \operatorname{Var}(x^\xi_n) = \operatorname{Var} \left( \sum_{m=1}^{N} x_m\inner{\xi_m, \xi_n} \right) = \sum_{m=1}^{N} \operatorname{Var} (x_m\inner{\xi_m, \xi_n}).
\end{equation}
Then  the previous two lemmas yield
\begin{equation}
   \sum_{m=1}^{N} \operatorname{Var} (x_m\inner{\xi_m, \xi_n}) = \sum_{m=1}^{N} x_m^2 \left( \mathbb{E}[\inner{\xi_m, \xi_n}^2] - \mathbb{E}\left[\inner{\xi_m, \xi_n}\right]^2\right) = \frac{1}{d + 1} \sum_{m \neq n} x_m^2,
\end{equation}
proving the claim.
</div>
<br>
These results suggest an algorithm for sketching count vectors, which will later serve as the basis for the actual <font style="font-variant: small-caps">count sketch</font>  algorithm. Such an algorithm is best thought of abstractly without regard to the finite nature of computing, hence the name "<font style="font-variant: small-caps">abstract sketch</font>".

[algorithm]

## Discretization

To realize the abstract sketching algorithm one may *discretize* the sphere, replacing it with a finite set $\mathcal{S}  = \\{s_1, \ldots, s_{\abs{\mathcal{S}}}\\} \subset \mathbb{S}^d$ and then consider all maps $\xi \colon \mathcal{O} \to \mathcal{S}$, denoted by $H(\mathcal{S})$. Since the range of $\xi$ has been restricted to a finite set, we may think of $\xi \in H(\mathcal{S})$ as *hashes*.

<div class="lemma">
Suppose $\mathcal{S} \subseteq \mathbb{S}^d$ is *balanced*, that is, $\sum_{s \in S} s = \mathbf{0}$. Then $\mathbb{E}[\inner{\xi_n, \xi_m}] = 0$ for $n \neq m$, given a uniform distribution on $H(\mathcal{S})$.
</div>
<div class="proof">
One has by definition
\begin{equation}
    \mathbb{E}[\inner{\xi_n, \xi_m}] = \frac{1}{\abs{\mathcal{S}}^2} \sum_{\mathcal{S} \times \mathcal{S}} \inner{s_1, s_2} = \frac{1}{\abs{\mathcal{S}^2}} \big\langle\textstyle\sum_{s_1 \in \mathcal{S}} s_1, \sum_{s_2 \in \mathcal{S}} s_2 \big\rangle = 0.
\end{equation}
</div>
<br>

<div class="theorem">
Let $\mathcal{S}\subseteq \mathbb{S}^d$ be balanced. Then $S_\xi$ and $T_\xi$ are (right, left) inverses in expectation, i.e., $\mathbb{E}[T_\xi S_\xi] = \id$, given a uniform distribution on $H(\mathcal{S})$.
</div>
<div class="proof">
See the continuous case above.
</div>
<br>

Assume a uniform distribution on $H(\mathcal{S})$. Then $\mathbb{E}[\inner{\xi\_m, \xi\_n}^2]$ only depends on $\mathcal{S}$ and the value of $\delta\_{m,n}$. This is due to the fact that a permutation $\rho \colon \mathcal{O} \to \mathcal{O}$ induces a measure-preserving bijection on $H(\mathcal{S})$ which sends $\xi \mapsto \xi \circ \rho$, hence preserving $\mathbb{E}[\inner{\xi\_m, \xi\_n}^2]$. In fact, when $m \neq n$, one has $\mathbb{E}[\inner{\xi\_m, \xi\_n}^2] = \lVert G(\mathcal{S})\rVert^2$, where $G$ is the Gram matrix given by $G\_{jk} = \langle \abs{\mathcal{S}}^{-1/2} s\_j, \abs{\mathcal{S}}^{-1/2} s\_k \rangle$.

<div class="theorem">
Let $\mathcal{S} \subseteq \mathbb{S}^d$ be balanced. Let $\mathbf{x}^{\xi} = T_\xi(S_\xi(\mathbf{x}))$ be the reconstruction of the $\xi$-sketch of $\mathbf{x}$. Then $\operatorname{Var}(x^\xi_n) = \abs{\Pi_n\mathbf{x}}^2 \lVert G(\mathcal{S}) \rVert^2$, given a uniform distribution on $H(\mathcal{S})$.
</div>
<div class="proof">
Since each $\xi_k$ is an independent random variable, it follows that
\begin{equation}
    \operatorname{Var}(x^\xi_n) = \operatorname{Var} \left( \sum_{m=1}^{N} x_m\inner{\xi_m, \xi_n} \right) = \sum_{m=1}^{N} \operatorname{Var} (x_m\inner{\xi_m, \xi_n}).
\end{equation}
Then the previous lemma yields
\begin{equation}
   \sum_{m=1}^{N} \operatorname{Var} (x_m\inner{\xi_m, \xi_n}) = \sum_{m=1}^{N} x_m^2 \left( \mathbb{E}[\inner{\xi_m, \xi_n}^2] - \mathbb{E}\left[\inner{\xi_m, \xi_n}\right]^2\right) = \sum_{m \neq n} x_m^2 \mathbb{E}[\inner{\xi_m, \xi_n}^2],
\end{equation}
proving the claim.
</div>
<br>

Using discretization, we can recover the original <font style="font-variant: small-caps">count sketch</font> algorithm. Specifically, let $\\{\mathbf{f}\_0, \ldots, \mathbf{f}\_{d}\\}$ be the canoncial basis of $\R^{d+1}$, and let $\mathcal{S} = \\{\pm \mathbf{f}\_j\\}$.
<div class="lemma">
$\lVert G(\{\pm \mathbf{f}_j\}) \rVert^2 = \frac{1}{d+1}$.
</div>
<div class="proof">
We calculate
\begin{equation}
    \mathbb{E}[\inner{\xi_m, \xi_n}^2] = \frac{1}{\abs{\mathcal{S}}^2}\sum_{j, k} \inner{\mathbf{f}_j, \mathbf{f}_k}^2  = \frac{1}{(d+1)^2} \sum_{j=k} \inner{\mathbf{f}_j, \mathbf{f}_k}^2  = \frac{1}{d+1}.
\end{equation}
</div>
<br>
Thus the variance of $x^\xi\_n$ using the <font style="font-variant: small-caps">count sketch</font> algorithm with $\mathcal{S} = \\{\pm \mathbf{f}\_j\\}$ is $\frac{1}{d+1}\abs{\Pi\_n \mathbf{x}}^2$, in agreement with the original paper. Two natural questions arise from this development:

1. Do other choices of balanced $\mathcal{S}$ provide lower variance?
2. Can one obtain a lower variance by using a non-uniform distribution on $H(\mathcal{S})$(in which case $\mathcal{S}$ may not be balanced)?

One expects that using $\mathcal{S} = \\{\pm \mathbf{f}\_j\\}$ with a uniform distribution "separates" the hash values as much as possible, reducing the ability for outcomes with higher counts to corrupt estimates of less frequent outcomes. In fact, both questions may be easily answered in the negative. To do this, consider an unbalanced set $\mathcal{S}$, and then assign weights $p \colon \mathcal{S} \to [0,1]$ such that $\sum\_{s \in S} p(s) = 1$ and $\sum\_{s \in S} p(s)s = 0$. We consider distributions on $H(\mathcal{S})$ where each $\xi\_n$ is independent and identically distributed according to the weights $p$. Then one may show in a similar fashion to the previous lemmas that $\mathbb{E}[\inner{\xi_n, \xi_m}] = 0$. Let the corresponding Gram matrix to $\mathcal{S}$ with weights $p$ be given by
\begin{equation}
    G\_{jk}(\mathcal{S}, p) \bydef \big\langle\sqrt{\vphantom{t}p(s\_j)}s\_j, \sqrt{\vphantom{t}p(s\_k)}s\_k\big\rangle = \sqrt{\vphantom{t}p(s\_j)p(s\_k)}\inner{s\_j, s\_k}.
\end{equation}

Now a generalization of the [Welch bound](https://www.wikiwand.com/en/Welch_bounds) yields that
\begin{equation}
    \lVert G(\mathcal{S}, p) \rVert ^2 \leq \frac{1}{d+1}(\tr G(\mathcal{S}, p))^2 = \frac{1}{d+1}\left(\sum\_{s \in S} p(s)\inner{s, s}\right)^2 = \frac{1}{d+1}.
\end{equation}
One can then generalize the variance theorem to see that the variance achieved is in fact optimal among all choices for discretization.

## A Count Sketch Variant
Let us refer to the choice $\mathcal{S}\_{\rm cross} = \\{\pm \mathbf{f}\_j\\}$ as a \say{cross-polytope} discretization of $\mathbb{S}^d$(since the convex hull of $\mathcal{S}\_{\rm cross}$ is a cross-polytope). For all $d \geq 0$ there exists a choice of balanced $\mathcal{S}$ with $\abs{\mathcal{S}} = d+2$, the \textit{simplicial} discretization $\mathcal{S}\_{\rm simp}$. Specifically, $\mathcal{S}\_{\rm simp}$ consists of the vertices of a regular $(d+1)$--simplex inscribed in $\mathbb{S}^d$. By symmetry, one has that for $\inner{s\_j, s\_k}$ is equal to some constant for $j \neq k$. Furthermore,
\begin{equation}
    0 = \sum\_{s \in \mathcal{S}} \inner{s\_j, s} = \inner{s\_j, s\_j} + \sum\_{j \neq k} \inner{s\_j, s\_k},
\end{equation}
which implies that $\inner{s\_j, s\_k} = -\frac{1}{d+1}$ whenever $j \neq k$. Hence $\lVert G(\mathcal{S}_{\rm simp}) \rVert^2 = \frac{1}{d+1}$, yielding optimal variance. This suggests a variant of <font style="font-variant: small-caps">count sketch</font> with a smaller set of hash values.

[algorithm]

It is not hard to see from first principles that this algorithm yields in expectation the correct estimate for a given count, without making use of any of the geometric intuition developed earlier. One of the chief differences from the traditional algorithm is the time complexity for the estimate; when one uses $\mathcal{S}\_{\rm cross}$ estimation is $O(1)$, while with $\mathcal{S}_{\rm simp}$ it is $O(d)$. However, the algorithm in this form builds the *exact* same data structure as the  <font style="font-variant: small-caps">count-min sketch</font> algorithm; hence it may be preferred when one wishes to attempt both sketch estimates.
