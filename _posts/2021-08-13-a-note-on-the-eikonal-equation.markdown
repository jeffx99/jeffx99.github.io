---
layout: post
title: "On the Eikonal Equation"
date: 2021-08-13
categories: math
---


<div class="theorem">
Suppose $u \in C^3(\R^2)$ satisfies the eikonal equation $\abs{\nabla u} = 1$. Then $\nabla u$ is constant.
</div>
<div class="proof">
By the Bochner formula
\begin{equation}
    \tfrac{1}{2} \Delta \abs{\nabla u}^2 = \inner{\nabla \Delta u, \nabla u} + \abs{\nabla \nabla u}^2 = 0.
\end{equation}
Now we have
\begin{equation}
    \tfrac{1}{2} \big[(\Delta u)^2 - \abs{\nabla \nabla u}^2\big] = \tfrac{1}{2} \big[(\tr \Hess_u)^2 - \abs{\Hess_u}^2\big] = \det \Hess_u,
\end{equation}
since for a $2 \times 2$ matrix $A$ with eigenvalues $\lambda_1, \lambda_2$, we have
\begin{equation}
    \tfrac{1}{2}\big[(\tr A)^2 - \abs{A}^2\big] = \tfrac{1}{2}\big[(\lambda_1 + \lambda_2)^2 - (\lambda_1^2 + \lambda_2^2)\big] = \lambda_1\lambda_2 = \det A.
\end{equation}
Now for any vector field $X$ we have
\begin{equation}
    \Hess_u(X, \nabla u) = \inner{\nabla_X \nabla u, \nabla u} = \nabla_X \abs{\nabla u}^2 = 0,
\end{equation}
so the Hessian is degenerate and thus $\det \Hess_u = 0$. Together, we have $\inner{\nabla \Delta u, \nabla u} + (\Delta u)^2 = 0$. Let $Y = \nabla u$ and $f = \Delta u$, so that we may rephrase this as the differential equation $Yf + f^2 = 0$. Now since $\abs{Y}$ is bounded, $Y$ is a complete vector field. Suppose, for the sake of contradiction, that there exists a point $x_0 \in \R^2$ such that $f(x_0) \neq 0$. Then consider the integral curve $\gamma \colon (-\infty, \infty) \to \R^2$ with $\gamma(0) = x_0$ and $\gamma'(t) = Y_{\gamma(t)}$. One has, letting $g = f \circ \gamma$,
\begin{equation}
    Y_{\gamma(t)}f + f(\gamma(t))^2 = g'(t) + g(t)^2 = 0,
\end{equation}
which by uniqueness of solutions implies
\begin{equation}
    g(t) = \frac{1}{t - t_0}; \quad t_0 = -\frac{1}{g(0)},
\end{equation}
implying $g(t_0) = \infty$, our contradiction. Thus $f = \Delta u \equiv 0$, from which Bochner formula implies that $\nabla \nabla u = 0$. Hence $\nabla u$ is constant.
</div>

Without too much effort, one may extend this result for $n \geq 2$ on $\mathbb{R}^n$ and Riemannian manifolds. There is a geometric intepretation of the theorem described as follows. Consider level sets $\Sigma_{t} = u^{-1}(\{t\})$, and note that
\begin{equation}
    H_{\Sigma_t} = \div_{\R^n}\left(\frac{\nabla u}{\abs{\nabla u}}\right) = \div(\nabla u) = \Delta u.
\end{equation}
Thus the Laplacian measures the mean curvature of level sets, and the content of the theorem is that performing a gradient flow on such level sets will cause an eventual "pinch," blowing up $H$. In fact, the Bochner formula is a Riccati-type formula for this flow. We rephrase the rest of this post in more geometric terms using this Riccati-type formula.

---

## Curvature Blow-up and the Riccati Equation

<div class="lemma">
Let $M^n \cong \Sigma^{n-1} \times \R$ be a Riemannian manifold diffeomorphic to a product of an $(n-1)$-manifold $\Sigma$ with $\R$ such that $\pi^*_\Sigma T\R = \pi^*_{\R}T\Sigma^{\perp}$ as subbundles. Let $\nu = \partial_t$ and suppose that $\abs{\nu} = 1$. Consider the shape operator $S(X) = \nabla_X \nu$; then one has
\begin{equation}
    (\nabla_\nu S)(X) + (S \circ S)(X) = -R(X, \nu)\nu.
\end{equation}
</div>
<div class="proof">
Let $Y \in \Gamma(TM)$ be the pullback of a section of $T\Sigma$ or be equal to $\nu$. Then $\nabla_\nu \inner{\nu, Y} = 0$ and $[Y, \nu] = 0$, so
\begin{equation}
     -\inner{\nabla_\nu \nu, Y} = \inner{[Y, \nu], \nu} + \inner{\nabla_\nu Y, \nu}  = \inner{\nabla_Y \nu, \nu} = \tfrac{1}{2}\nabla_Y \inner{\nu, \nu} = 0,
\end{equation}
implying that $\nabla_\nu \nu = 0$. We then calculate,
\begin{align}
    (\nabla_\nu S)(X) = \nabla_\nu (S(X)) - S(\nabla_\nu X) &= \nabla_\nu \nabla_X \nu - \nabla_{\nabla_\nu X} \nu \\
    &= \big(\nabla_\nu \nabla_X \nu - \nabla_X \nabla_\nu \nu - \nabla_{[\nu, X]} \nu \big) - \nabla_{\nabla_X \nu} \nu \\
    &= R(\nu, X)\nu - (S \circ S)(X),
\end{align}
and rearrange.
</div>

<div class="corollary">
Taking the trace of the Riccati formula yields that for the surfaces $\Sigma_t = \Sigma \times \{t\}$,
\begin{equation}
    \partial_t H + \abs{A}^2 = -\Ric(\nu, \nu),
\end{equation}
where $H = \tr(S)$ and $A(X,Y) = \inner{S(X), Y}$ is the second fundamental form.
</div>

<div class="lemma">
Let $f \colon \mathbb{R} \to \mathbb{R}$ satisfy the differential inequality $f' + \alpha f^2 \leq 0$ everywhere, for some constant $\alpha > 0$. Then $f \equiv 0$.
</div>
<div class="proof">
Assume, for the sake of contradiction, that there exists a point $x_0$ such that $f(x_0) \neq 0$. Since $g(x) = -f(-x)$ also satisfies $g' + \alpha g^2 \leq 0$ everywhere, we may assume without loss of generality that $f(x_0) > 0$. Let $U = f^{-1}(\R \setminus \{0\})$, which contains $x_0$ and is thus an nonempty open set, and let $g = 1/f \colon U \to \R$. Let $a$ be the infimum of all $y$ such that $(y, x_0) \subseteq U$(so $-\infty \leq a < x_0$) and let $I = (a, x_0)$. Then by connectedness, $g$ is positive on $I$. Now let $L(x) = g(x_0) + \alpha(x - x_0)$; one calculates that for $x \in I$,
\begin{equation}
    g'(x) = -\frac{f'(x)}{f(x)^2} \geq \alpha = L'(x).
\end{equation}
Since $L(x_0) = g(x_0)$, we get that $g(x) \leq L(x)$ for $x < x_0$. Then if $a > -\infty$, we have by positivity and continuity $L(a) \geq \lim_{x \to a} g(a) = +\infty$, which is a contradiction. Otherwise, if $a = -\infty$, consider $x_1 = x_0 - \alpha^{-1}g(x_0) \in I$ and note that $g(x_1) \leq L(x_1) = 0$, which contradicts positivity.
</div>

In essence, this is another "blow up" argument. The contradiction, which was that $g$ changed sign across $I$, describes a blow up of $f$. With this we may extend the theorem to general manifolds.

<div class="theorem">
Let $(M^n, g)$ be a complete Riemannian manifold with $n \geq 2$ and $\Ric \geq 0$. Suppose $u \in C^3(M)$ satisfies the eikonal equation $\abs{\nabla u} = 1$. Then $\nabla \nabla u = 0$.
</div>
<div class="proof">
Let $\Sigma_0 = u^{-1}(\{0\})$. Then since $\abs{\nabla u}$ is bounded, and $M$ is complete, the vector field $\nabla u$ is complete, yielding a gradient flow $\Phi \colon \Sigma_0 \times \mathbb{R} \to M$. Let $\Sigma_t = \Phi_t(\Sigma_0)$; then by the Riccati equation and Cauchy-Schwarz,
\begin{equation}
    \partial_t H + \tfrac{1}{n-1} H^2 \leq \partial_t H + \abs{A}^2 = -\Ric(\nabla u, \nabla u) \leq 0
\end{equation}
where $H(x, t)$ and $A(x,t)$ gives the mean curvature and second fundamental form of $\Sigma_t$ at $\Phi(x,t)$. Fixing $x \in \Sigma_0$ and applying the blow-up lemma, we obtain that $H(x, t) \equiv 0$. In particular, substitution back into the inequality yields $\abs{A}^2 \leq 0$, so the second fundamental form $A = \nabla \nabla u$ vanishes.
</div>
<div class="corollary">
Immediate corollaries are that $\Ric(\nabla u, \nabla u) = 0$ and $\Sigma_t$ is totally geodesic. The former implies the nonexistence of solutions for strictly positive Ricci curvature.
</div>

We now show that the second result constrains the structure of $M$ considerably for $n = 2$.

<div class="theorem">
Let $(M^2, g)$ be a complete connected Riemannian $2$-manifold $\Ric \geq 0$. Suppose $u \in C^3(M)$ satisfies the eikonal equation $\abs{\nabla u} = 1$. Then $M$ is either isometric to $\R^2$ or $\mathbb{S}^1 \times \R^1$ with the flat metric.
</div>
<div class="proof">
Let $\Sigma_0 = u^{-1}(\{0\})$; as a complete connected $1$-manifold it isometric to either $\R^1$ or $\mathbb{S}^1$. Now, it follows from our previous discussion that there exists a diffeomorphism $\Phi \colon \Sigma_0 \times \R \to M$ such that $\Sigma_t = \Phi_t(\Sigma_0)$ is totally geodesic. Let $\d x$ and $\d t$ be the volume forms on $\Sigma_0$ and $\R$, and give $\Sigma_0 \times \R$ the flat metric $\delta = \d x \otimes \d x + \d t \otimes \d t$. Let $\d \sigma_t$ be the volume form on $\Sigma_t$; we may write $g = \d \sigma_t \otimes  \d \sigma_t + \d u \otimes \d u$. Now we wish to check that $\Phi^*(g) = \delta$. Clearly $\Phi^*(\d u) = \d t$, and on $\Sigma_0$, we have $\Phi_0^*(\d \sigma_0) = \d x$. Note that $\mathcal{L}_{\partial_t} \d x = 0$. Likewise,
\begin{equation}
    \mathcal{L}_{\nabla u} \d \sigma_t = H_{\Sigma_t} \d \sigma_t = 0.
\end{equation}
Taking the pullback gives $\mathcal{L}_{\partial_t} \Phi^*(\d \sigma_t) = 0$, so $\mathcal{L}_{\partial_t} \Phi^*(\d \sigma_t) = \mathcal{L}_{\partial_t} \d x$. Since the pullback agrees with $\d x$ for $t = 0$, it follows that $\Phi^*(\d \sigma_t) = \d x$ everywhere, from which the conclusion follows.
</div>

In general, $M$ is a foliation of totally geodesic submanifolds.
<div class="question">
Let $(M^n, g)$ be a complete Riemannian manifold with $n \geq 2$ and $\Ric \geq 0$. Suppose $u \in C^3(M)$ satisfies the eikonal equation $\abs{\nabla u} = 1$. Is $M$ isometric to the product $\Sigma_0 \times \R$?
</div>
